# Candidate Screening Scorecard — Senior Backend Engineer (Meridian Cloud Systems)

**Screened against:** Screening Criteria Rubric, 2026-07-14
**Screener:** Alex
**Batch:** Requisition #MCS-ENG-2291, first-pass review of 3 of 47 applications

## Summary Table

| Candidate | Verdict | Must-haves | Should-have score | Top reason |
|---|---|---|---|---|
| Dana Okafor | **Advance** | 5/5 pass | 11/12 | Direct billing-system ownership with strong metrics |
| MarcusVille | **Hold** | 5/5 pass | 5/12 | Solid generalist backend background, but no metering/billing or event-streaming evidence |
| Renata Solis | **No** | 4/5 pass | — | Missing distributed-systems ownership; scope reads mid-level despite "Senior" title |

---

## Dana Okafor — Advance

**Current role:** Senior Software Engineer, Northbridge Payments (3 yrs)
**Prior:** Backend Engineer, Fennick Logistics (2.5 yrs)
**Total relevant experience:** 6.5 years

**Must-haves:** All 5 pass.
- 6.5 years backend, all production IC roles
- Node.js at Northbridge (payment reconciliation service), Go at Fennick (routing engine)
- Owns the settlement microservice at Northbridge — clear service-boundary language
- Named as primary on-call responder, references 4 postmortems authored
- US-based, no sponsorship flag

**Should-haves:** 11/12
- Usage-based billing/metering: **2** — resume states "rebuilt the usage-metering
  pipeline that calculates per-transaction fees for 12,000 merchant accounts,
  cutting reconciliation discrepancies from 1.8% to 0.04%"
- Kubernetes production: **2** — "migrated settlement service from EC2 to EKS,
  wrote the rollout runbook still in use"
- Kafka/event streaming: **2** — "consumer group redesign to eliminate duplicate
  charge events during broker failover"
- PostgreSQL at scale: **2** — mentions partitioning a 400M-row ledger table
- Mentoring: **2** — "onboarded and mentored 2 junior engineers, one promoted to mid-level"
- Open-source contribution: **1** — one merged PR to a Kafka client library, not a maintainer

**Top 3 reasons to advance:**
1. Direct, metric-backed experience in exactly the problem domain (usage-based billing accuracy)
2. Owns incident response, not just participates — postmortem authorship is a strong signal
3. Mentoring evidence suggests senior-level judgement, not just senior-level tenure

**Red flags to explore in screen (not disqualifying):** One 7-month gap between
Fennick and Northbridge, undocumented — worth a neutral "tell me about this period" question.

**Recommended next step:** Move to technical screen call. Prioritize — this is
the strongest resume in the batch so far.

---

## Marcus Village — Hold

**Current role:** Backend Engineer, Coastline Retail Tech (2 yrs)
**Prior:** Software Engineer, two prior roles of ~1.5 yrs each

**Must-haves:** All 5 pass, but thinly.
- 5.5 years combined, meets the floor
- Go experience at Coastline (inventory sync service)
- Some microservices language, but described at a feature level, not a systems-ownership level
- Mentions being "part of the on-call rotation" — no postmortem authorship named
- No visa flag

**Should-haves:** 5/12
- Usage-based billing/metering: **0** — no mention
- Kubernetes production: **1** — "deployed services to Kubernetes clusters managed by platform team" (used it, didn't own the infra decisions)
- Kafka: **0** — no mention
- PostgreSQL at scale: **2** — clear query-tuning example with a specific slow-query fix
- Mentoring: **1** — "helped onboard new hires" — vague
- Open source: **1** — minor doc contributions to an internal-facing tool, not really open source; scored partial for initiative

**Top 3 reasons for hold, not advance or no:**
1. Meets every must-have and has one genuinely strong data point (query tuning), so not a "no"
2. Zero evidence of the domain-specific differentiator (billing/metering) or event-streaming — the two highest-weighted should-haves
3. On-call language is passive ("part of rotation") versus Dana's active ownership language — needs clarification, not assumption

**Recommended next step:** Hold pending a short screen call focused specifically
on: (1) actual ownership scope on the inventory sync service, (2) any exposure to
event-driven architecture even outside Kafka specifically, (3) what "helped onboard"
concretely involved. Do not schedule a full technical interview yet.

---

## Renata Solis — No

**Current role:** Senior Backend Developer, Priya Retail Solutions (1 yr), title changed from "Backend Developer" after 6 months
**Prior:** Backend Developer, two short stints (11 months, 8 months)

**Must-haves:** 4/5 pass — fails on distributed systems / microservices ownership.
- 4 years experience total — below the 5-year floor, but close enough Alex flagged
  it as borderline rather than an instant fail per must-have judgement calls
- Node.js only, no Go — acceptable, rubric says Node.js OR Go
- **Fails:** No microservices or service-boundary language anywhere in the resume.
  All descriptions are of features built within a single monolithic Rails-adjacent
  Node app ("added new endpoints," "built the reporting module") — this reads as
  mid-level scope regardless of title
- On-call mentioned once, no ownership or postmortem language
- No visa flag

**Why this is a No, not a Hold:** The rubric treats distributed-systems ownership
as a hard eliminator for this specific requisition because the role requires
service-boundary design decisions from day one — there is no ramp-up runway
built into the headcount plan. A title bump six months into a one-year tenure,
paired with monolith-only scope, reads as title inflation rather than a
judgement-call gap worth exploring on a screen.

**Green flag worth noting for future roles:** Clean, quantified feature-delivery
metrics ("reduced page load on reporting dashboard from 4.2s to 900ms") — this is
a legitimately strong mid-level or Node-focused generalist candidate. Worth
keeping on file for a Backend Engineer II requisition, not this one.

**Recommended next step:** Send standard rejection; flag profile for future
mid-level Node.js openings rather than discarding entirely.
