# Julian - Worked Example

One fully worked example, so you can see Julian on a realistic high-traffic design
task: architecting a system, making the hard calls with their trade-offs spelled out,
choosing a consistency model, planning to scale, naming the risks, and - critically -
laying out how to validate it before it ships. The output is shaped as an Architecture
Decision Record (ADR), which is Julian's primary artifact.

The example uses an invented company, *Tolt*, an event-ticketing platform, with
plausible figures. Julian produces the same structure against your real drivers,
numbers, and constraints.

---

**Ask:** Tolt sells tickets for concerts and sports. Most days are quiet, but when a
big show goes on sale there is a sharp "on-sale spike": tens of thousands of people hit
the same event in the same minute, all trying to buy from the same small, fixed pool of
seats. Today it's a single Rails monolith on one database; every big on-sale either
oversells (two people get seat 14C) or the site falls over. The ask: an architecture
that handles the spike, never sells the same seat twice, and stays honest about what
it's trading away.

---

# ADR-014: Architecture for High-Concurrency Ticket On-Sales

- **Status:** Proposed (pending PoC + load test - see section 10)
- **Date:** 2026-07-25
- **Deciders:** Architecture guild, Platform lead, Payments lead
- **Supersedes:** ADR-003 (single-database inventory)

## 1. Context & Decision Drivers

The behaviour that dominates this design is not average load - it's the **on-sale
spike** against a **fixed, contended inventory**. That combination is what makes ticket
on-sales genuinely hard: it is a run on a limited resource, not a stream of independent
writes.

Measured / target drivers (numbers to confirm in load test - see section 10; [FILL IN] are
Tolt's to supply):

| Driver | Value | Why it matters |
|---|---|---|
| Peak concurrent buyers | ~50,000 in the first 60s of a marquee on-sale | Determines front-door and queue capacity |
| Peak write contention | ~5,000 seat-reservation attempts/sec against **one** event's seat map | The real bottleneck - many writers, one hot resource |
| Inventory size per event | 5,000-60,000 seats | Small enough that oversell is catastrophic and visible |
| Correctness requirement | **Zero oversell.** A seat is sold at most once. | Non-negotiable; a double-sell means a customer turned away at the door |
| Latency target | Reserve action p99 < 500 ms | Perceived responsiveness under load |
| Availability SLO | 99.9% for browse; on-sale must degrade gracefully, not crash | Browsing can tolerate a blip; the on-sale must never oversell even while failing |
| Payment | External PSP (Stripe), 1-5 s, can fail/time out | An unreliable dependency in the critical path |
| Team | ~12 engineers, 3 squads | Small enough that full microservices would be a tax, not a gift |

**Dominant quality attributes:** (1) **correctness under contention** (no oversell),
(2) **write scalability during the spike**, (3) **graceful degradation**. Global strong
consistency across *everything* is explicitly **not** a goal - only the seat-inventory
write path needs to be strongly consistent.

## 2. The Central Trade-off

Two forces pull in opposite directions:

- **Zero oversell** wants a single source of truth per seat and a strongly consistent,
  serialized decision - "is this seat free? then it's yours" must be atomic.
- **50k concurrent buyers** want massive horizontal scale, which pushes toward
  distribution, caching, and eventual consistency.

Naively serving both leads to either (a) a distributed system that eventually-consistently
oversells, or (b) a single hot row that everyone contends on and that topples under load.

Julian's resolution: **do not make the whole system strongly consistent - make only the
seat-hold decision strongly consistent, and shrink the population that reaches it.** We
achieve scale by *reducing contention* (a virtual waiting room + partitioning inventory
by event) rather than by relaxing correctness.

## 3. Options Considered

### Option A - Keep the monolith, scale the database vertically
- **How:** Bigger DB instance, row-level `SELECT ... FOR UPDATE` on seats.
- **Trade-off:** Simplest, no new moving parts. But 5,000 lock attempts/sec on one
  event's rows serialize into a queue *inside* the database; the DB becomes the single
  contended chokepoint and vertical scaling has a hard ceiling. Correct, but it falls
  over - which is today's problem. **Rejected** as the load target.

### Option B - Full microservices, event-sourced inventory, eventual consistency
- **How:** Split into ~8 services; inventory as an event-sourced aggregate; reserve via
  async events; reconcile.
- **Trade-off:** Maximally scalable and auditable. But eventual consistency on a
  *contended finite resource* means two reservations can both be accepted before the
  read model converges -> **oversell**, then compensations that cancel a customer's
  already-confirmed seat. It also imposes a distributed system, sagas everywhere, and an
  event-sourcing learning curve on a 12-person team. The complexity buys audit and
  scale we can get more cheaply, and the eventual consistency actively fights our #1
  requirement. **Rejected** - this is the "reach for the trendy pattern" trap.

### Option C (chosen) - Modular monolith + a dedicated inventory service, virtual
### waiting room, per-event partitioned strong consistency, async fulfilment
- **How:** Keep most of the product as a **modular monolith** (catalog, accounts,
  browsing - one deploy, clear internal modules). Carve out **one** service, the
  **Inventory/Seat-Hold service**, because it has a genuinely different scaling and
  consistency profile. Put a **virtual waiting room** in front of on-sales to convert a
  stampede into a throttled stream. Make the seat-hold decision **strongly consistent
  but partitioned by event**, so contention is bounded per event, not global. Do
  payment and ticket issuance **asynchronously** off the hot path via the **transactional
  outbox** pattern.
- **Trade-off:** More moving parts than Option A and eventual consistency *between* the
  hold and the final confirmed ticket (the customer sees "reserved, finalising..."). But
  the one place that must be exactly right - the seat hold - stays strongly consistent,
  and everything expensive or flaky (payment) is moved off the critical decision. We
  accept mild latency and a "pending" state in exchange for correctness and scale.

## 4. Decision

Adopt **Option C**. Concretely:

```
   50k buyers --> CDN --> +------------------------------+
                          |  Virtual Waiting Room (queue)|  admits N buyers/sec
                          +---------------+--------------+
                                          | signed entry token
                                          v
                     +----------------------------------------+
                     |  API Gateway (authn, rate limit, WAF)   |
                     +------+--------------------------+-------+
                            | browse (read)            | reserve (write)
                            v                          v
              +------------------------+   +------------------------------+
              |  Modular Monolith      |   |  Inventory / Seat-Hold svc   |
              |  (catalog, accounts,   |   |  strongly consistent,        |
              |   read replicas + CDN) |   |  PARTITIONED BY event_id     |
              +------------------------+   |  Redis hold + DB commit      |
                                           +---------------+--------------+
                                                           | writes hold + outbox row
                                                           v   (same DB txn)
                                               +-----------------------+
                                               |  Outbox -> Kafka topic|
                                               +-----------+-----------+
                                        +------------------+------------------+
                                        v                                     v
                            +----------------------+          +----------------------+
                            |  Payment consumer    |          |  Ticketing consumer  |
                            |  (Stripe, saga)      |          |  (issue PDF/QR,      |
                            |                      |          |   email, wallet)     |
                            +----------------------+          +----------------------+
```

**Boundaries chosen:**
- **Modular monolith** owns catalog, search, accounts, order history. One deploy unit,
  internal module boundaries, read-scaled with replicas + CDN. We resist splitting these
  because there is no driver forcing it - the team is small and they share a lot of data.
- **Inventory/Seat-Hold** is the *only* extracted service, justified by a concrete
  driver: it scales and must be consistent on a different axis than everything else, and
  it is the failure domain we most need to isolate (a bulkhead).
- **Payment** and **Ticketing** are asynchronous consumers, decoupled from the hold so
  a slow PSP never blocks the seat decision.

## 5. Data Consistency Approach

This is the crux, so it gets named explicitly.

- **Seat hold = strong consistency, per-event partition.** Each event's seat map lives
  in one partition (Redis for the hot hold + the authoritative relational row as the
  durable record). Acquiring a hold is an **atomic compare-and-set**: a seat moves
  `available -> held(user, ttl)` only if it is currently `available`. Two racing buyers
  hit the same atomic operation on the same partition; exactly one wins. Because we
  partition by `event_id`, event A's contention never touches event B - we get
  serialization *where correctness needs it* without a global lock.
- **Holds expire (TTL, e.g. 8 minutes).** A hold is a *temporary* reservation, not a
  sale. If the buyer abandons or payment fails, the TTL releases the seat back to
  `available`. This is what makes finite inventory tolerate an unreliable payment step.
- **Dual-write problem, solved with the outbox.** When a hold is confirmed, the
  Inventory service writes the seat state change **and** an event row into an `outbox`
  table **in the same local database transaction**. A relay publishes outbox rows to
  Kafka. This guarantees "seat committed <=> event published" atomically - we never
  commit a sale without emitting the event, and never emit an event for a sale that
  rolled back. No distributed transaction required.
- **Fulfilment = eventual consistency + saga.** Payment -> ticket issuance -> email runs
  as an **orchestrated saga** off the Kafka event. Each step is **idempotent** (keyed by
  `hold_id`) so at-least-once delivery and retries can't double-charge or double-issue.
  Compensating action: if payment ultimately fails, the saga releases the hold (or lets
  the TTL do it) and notifies the buyer. The customer briefly sees "reserved,
  finalising your tickets" - an honest, correct eventual-consistency window.
- **CAP posture:** under a partition, the seat-hold path chooses **consistency over
  availability** (better to reject a reservation than to oversell); the browse path
  chooses **availability** (stale seat-count is fine). Different paths, different
  choices, stated on purpose.

## 6. Scalability Approach

- **Shrink the herd before it arrives - the virtual waiting room.** The single most
  effective scaling lever here isn't more servers, it's admitting fewer people at once.
  The waiting room holds the 50k arrivals and releases them at a rate the inventory
  service is *proven* (by load test) to handle - e.g. 2,000 buyers/sec. The stampede
  becomes a throttled stream; the rest of the system is sized for the admitted rate, not
  the arrival rate. This is load shedding done kindly.
- **Partition inventory by event.** Contention is bounded per event, so ten simultaneous
  on-sales scale horizontally across partitions/shards instead of fighting over one DB.
- **Stateless services + horizontal scale.** Gateway, monolith, and inventory nodes hold
  no session state (entry tokens are signed/JWT), so we add instances behind an L7 load
  balancer freely and autoscale on the admitted rate.
- **Cache the read path aggressively.** Event listings, seat *maps* (layout, not live
  status), and static assets are cache-aside in Redis + CDN. Live seat *availability* is
  served as a near-real-time, deliberately-approximate count (it's fine if "312 seats
  left" is a second stale) - the authoritative check happens only at hold time. This
  keeps the strongly-consistent path small and everything else cheap.
- **Async fulfilment absorbs PSP latency.** Because payment is off the hot path, a slow
  Stripe doesn't consume inventory-service capacity; Kafka buffers the backlog.

## 7. Resilience Approach

Every remote call assumes the callee will fail:

- **Timeouts everywhere.** Hold operation, Stripe call, and DB calls all have explicit
  timeouts; nothing waits forever.
- **Retries with backoff + jitter**, but only on idempotent operations (hold acquisition
  and every saga step are idempotent by `hold_id`), so retries never double-book or
  double-charge.
- **Circuit breaker around Stripe.** If the PSP degrades, the breaker opens: new orders
  stay in "reserved" (holds intact) and the saga drains when Stripe recovers, instead of
  hammering a dying dependency.
- **Bulkhead: inventory is its own service and datastore.** A catalog-side outage or a
  bad deploy to the monolith cannot take down the on-sale, and vice versa. The failure
  domains are isolated by design.
- **Backpressure / load shedding** is the waiting room itself, plus rate limits at the
  gateway per entry token to blunt bots and scripts.
- **Graceful degradation:** if live availability counts fail, browsing falls back to
  "seats available / limited / sold out" buckets rather than erroring - but the
  authoritative hold check never degrades. We degrade the nice-to-have, never the
  correctness guarantee.
- **Redundancy:** multi-AZ for inventory DB and Kafka; RPO ~ 0 for committed sales via
  synchronous replication of the inventory store; RTO target [FILL IN].

## 8. Security & Observability by Design

- **Security:** OAuth2/OIDC for buyers; **signed, short-lived entry tokens** from the
  waiting room prevent skipping the queue; mTLS for service-to-service; least-privilege
  DB creds per service; PCI scope kept minimal by never touching raw card data (Stripe
  Elements tokenises client-side); rate limiting + WAF at the gateway against the bot
  armies that target on-sales. STRIDE threat model run as a design step, not a launch
  gate.
- **Observability:** structured logs with a `correlation_id`/`hold_id` threaded from the
  waiting room through the gateway, the hold, and *across the async Kafka hop* into the
  saga, so one buyer's journey is traceable end to end. RED metrics (rate, errors,
  duration) on the hold endpoint; USE metrics on the inventory datastore; distributed
  traces across the async boundary. SLIs: hold-success rate, hold p99, oversell count
  (must be 0), fulfilment lag. Error budget on the 99.9% browse SLO.

## 9. Consequences

**Positive**
- Zero-oversell is structurally guaranteed by the atomic per-event hold, not by hope.
- The spike is handled by *reducing contention* (waiting room + partitioning), which
  scales far better and cheaper than brute-forcing one hot database.
- Flaky, slow payment is off the critical path; the PSP can wobble without blocking sales.
- We extracted exactly **one** service - the team keeps a modular monolith for everything
  else and avoids paying the full microservices tax.

**Negative (the honest bill)**
- New operational surface: Redis, Kafka, a waiting room, and a saga to run and monitor.
- An eventual-consistency window between "seat held" and "ticket issued" - the UX must
  communicate "finalising" clearly, and support must understand the "reserved but not yet
  confirmed" state.
- Saga + idempotency logic is more code and more careful reasoning than a single DB
  transaction; the team must genuinely understand it (a training/docs cost).
- The waiting room admit-rate is a tuned parameter: set too low, buyers wait
  unnecessarily; too high, we melt the inventory service. It must be derived from the
  load test, not guessed - see section 10.

## 10. Validation & Rollout Plan  *(mandatory - this design is NOT production-ready until this passes)*

**This architecture is a proposal. It does not become the production design until the
proof of concept and load test below pass and the team has reviewed the results.**

**Proof of concept (non-production environment):**
1. Build a thin vertical slice: waiting room -> gateway -> inventory hold (atomic CAS in
   Redis + DB commit + outbox) -> Kafka -> a stub payment consumer.
2. Prove the two claims that carry the whole design:
   - **Correctness:** under deliberate race conditions, a seat is held at most once
     (fire thousands of concurrent holds at the same seat; assert exactly one success).
   - **Outbox atomicity:** kill the process between DB commit and Kafka publish; assert
     no lost or phantom events after recovery.

**Load test (non-production, production-shaped data):**
- Simulate a marquee on-sale: 50,000 virtual users arriving within 60s against a single
  20,000-seat event, with the waiting room admitting at a candidate rate.
- **Pass/fail thresholds:** oversell count = **0** (hard gate); hold p99 < 500 ms at the
  admitted rate; no unbounded queue growth in Kafka; inventory DB CPU < 70% at target
  admit rate; graceful behaviour when Stripe is fault-injected (breaker opens, holds
  survive, saga drains on recovery).
- **Derive the admit rate empirically** - find the admitted-buyers/sec at which p99 and
  DB utilisation stay within budget, and set the waiting room there with headroom.

**Document & review:**
- Record the measured numbers, the chosen admit rate, and any surprises back into this
  ADR (it is append-only; superseding decisions get their own ADR).
- **Review with the team** (architecture guild + platform + payments) before promoting.
  The design ships only after sign-off.

**Phased rollout:**
1. Ship behind a feature flag; run one *small* real on-sale through the new path (low-risk
   event) with the old monolith path as fallback.
2. **Canary:** route a fraction of a mid-size on-sale, watch oversell (0), hold p99, and
   fulfilment lag against the old path.
3. Progressively raise the share across on-sales; keep the monolith reservation path as a
   documented rollback until the new path has cleared several marquee on-sales.
4. Only then retire ADR-003's single-database inventory path.

---

*This example uses an invented company and plausible figures to show format and depth.
Julian produces the same decision-led, trade-off-explicit ADR - with the same mandatory
PoC, load test, and team review before any production commitment - against your real
drivers, numbers, and constraints.*
