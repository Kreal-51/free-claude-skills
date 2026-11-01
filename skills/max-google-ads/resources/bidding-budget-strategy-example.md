# Smart Bidding & Budget Strategy — Harlow Kitchen Supply (E-Commerce)

Fictional client: **Harlow Kitchen Supply**, a mid-market e-commerce brand selling premium cookware, average order value $145. Monthly ad budget: **$42,000**. Account is 14 months old with meaningful conversion history. This is the bidding and budget plan Max would set following the Smart Bidding decision tree from Capability #5.

## Current Account Data (Inputs to the Bidding Decision)

- Trailing 30-day conversions, blended across all campaigns: 612
- Trailing 30-day conversion value: $88,740
- Blended ROAS: 4.2x
- Monthly ad spend: $42,000 (currently underspending budget by ~$3,000 due to impression-share loss)

Because this account clears both the 30-conversion threshold (for Target CPA) and the 50-conversion threshold (for Target ROAS) by a wide margin, and it has reliable transaction-value data flowing from the Shopify integration, it qualifies for value-based bidding rather than volume-based bidding.

## Bidding Strategy by Campaign

| Campaign | Monthly Budget | Bidding Strategy | Target | Rationale |
|---|---|---|---|---|
| Brand Search | $5,000 (12%) | Target ROAS | 8.0x | High-intent branded traffic converts far above account average; protect it, don't throttle it |
| Core Non-Brand Search | $21,000 (50%) | Target ROAS | 4.5x | Slightly above current blended ROAS to push efficiency without collapsing volume |
| Shopping / PMax (product feed) | $12,600 (30%) | Maximize Conversion Value with ROAS target 3.8x | 3.8x | Automation-heavy channel; set target slightly below Search since PMax casts a wider, more prospecting-oriented net |
| Remarketing (via PMax audience signals + a dedicated Display remarketing campaign) | $3,400 (8%) | Target ROAS | 6.5x | Warm audience, historically highest ROAS in the account — protect its share of budget even though it's the smallest line |

Total: $42,000/month, matching the e-commerce allocation rule of thumb (Brand 10–15%, Core non-brand 50–60%, Shopping/PMax 25–35%, Remarketing 5–10%).

## Why Target ROAS Over Target CPA Here

Target CPA optimizes toward a flat cost-per-conversion regardless of order value, which is the wrong objective for a catalog with wide price variance ($35 individual pans up to $450 cookware sets). Target ROAS (and Maximize Conversion Value) lets Smart Bidding chase higher-value carts rather than simply chasing the cheapest conversion, which matters because a $35 sale and a $450 sale currently count as equally "successful" under a CPA-only model.

## Learning Period Governance

- Core Non-Brand Search is moving from a 4.0x to a 4.5x ROAS target this month — this is treated as a new learning period. No further target changes, budget changes, or new ad variants will be introduced in this campaign for **3 weeks** following the change.
- Shopping/PMax's asset groups are stable this month — no changes planned, so no learning disruption risk there.
- Any urgent creative refresh needed during a learning period gets queued and batched in, rather than trickled in one asset at a time, to avoid repeatedly restarting the algorithm.

## Budget Reallocation Note

The account is currently underspending by roughly $3,000/month against its budget cap — investigation shows this is an impression-share-lost-to-rank issue in Core Non-Brand Search (Quality Score dip on 3 of the largest keywords after a recent landing page redesign), not a budget-cap issue. Recommendation: fix Quality Score first (landing page load speed regressed from 1.8s to 3.4s post-redesign — this is a Landing Page Experience problem) before raising any bids, since raising bids on a low-QS keyword just pays more for the same clicks rather than fixing the root cause.

## 90-Day Roadmap

1. **Weeks 1–3:** hold the new Target ROAS on Core Non-Brand Search steady through its learning period; fix landing page speed regression in parallel (does not disrupt Smart Bidding learning, since it's not a bid/target/budget change)
2. **Weeks 4–6:** evaluate whether the 4.5x target is holding volume — if conversion volume has dropped more than 15% versus the prior 4.0x baseline, ease the target back toward 4.2x rather than reverting fully
3. **Weeks 7–12:** layer in enhanced conversions (currently not implemented on this account) to improve Smart Bidding signal quality by an estimated 15–30%, then reassess whether targets can tighten further with better data quality
