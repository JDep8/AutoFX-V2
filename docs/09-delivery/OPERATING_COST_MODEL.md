# Operating Cost Model
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DATA_LICENSING_AND_RETENTION.md](../04-data/DATA_LICENSING_AND_RETENTION.md), [DATA_SOURCE_REGISTER.md](../04-data/DATA_SOURCE_REGISTER.md), [DELIVERY_ROADMAP.md](./DELIVERY_ROADMAP.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-009, D-010), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-007)
- **Approval evidence:** None yet

## Purpose

This document models what it will cost to build and run AutoFX V2: data
licensing, hosting and compute, broker-related costs, and (for later
priorities) research-centre provider and content-production costs. All costs
are expressed as scenario ranges built from quoted or measured figures —
**no numbers are invented, and none exist yet**. The model exists so
affordability is checked against Jacob's actual budget (Q-007) before any
commitment, not after.

## Scope and decisions this document will own

- The cost-category register and the scenario-range format.
- The rule that every figure carries a source (quote, published price list,
  measured usage) and a retrieval date — unsourced figures are not admitted.
- Per-class cost scaling under the D-009 phased rollout.
- Affordability checkpoints tied to roadmap stages.
- Out of scope: licensing terms themselves
  ([DATA_LICENSING_AND_RETENTION.md](../04-data/DATA_LICENSING_AND_RETENTION.md));
  revenue and business-case modelling for the content business (CONTENT-004,
  Round M).

## Structure skeleton

### 1. Cost-category register
The categories tracked: data licensing (prices, news/events, calendars, per
class), hosting and compute (including multi-day book-generation jobs,
FR-002), storage and backup (OPS-002), broker/platform costs, monitoring and
ops tooling, research-centre model/provider costs (P2), and content
production (P3). Category list confirmed in Round N; P2/P3 categories are
planning-only per D-010.

### 2. Scenario-range format
Every category is costed as low/base/high scenarios with the assumptions that
separate them stated explicitly. Format fixed here; **all figures pending** —
data costs from Round D provider evaluations, infrastructure costs from
Round N, both constrained by Q-007. No placeholder numbers are permitted in
any draft.

### 3. Data-cost scaling per asset class (D-009)
How data licensing and storage cost grows as classes beyond FX pass Gate 1
and enter implementation — eight classes are designed-for, but only paid-for
as adopted. Depends on per-class symbol lists and providers from Rounds C/D,
and on the DATA-007 FMP evaluation (adequacy never assumed).

### 4. Cost drivers and sensitivities
Which assumptions move total cost most (history depth per DATA-001,
granularity per DATA-002, class count, backtest compute intensity, retention
policy), so Jacob can see what a scope choice costs before making it.
Populated once Rounds D/N supply the underlying quantities.

### 5. Affordability checkpoints
Where the roadmap checks projected cost against the Q-007 budget: before the
Exit Review, before each class rollout, and before any recurring commitment
(licences, hosting contracts). Checkpoint placement agreed in Round N.

### 6. Review and update cadence
How often figures are refreshed, and the rule that a stale quote is treated
as unknown rather than assumed still valid. Cadence set in Round N.

## Known inputs

- Q-007 (budget, horizon, infrastructure constraints) is OPEN and blocks all
  affordability conclusions.
- D-009: FX-first phasing means near-term cost exposure is FX data plus core
  infrastructure; other classes add cost only after their Gate 1.
- D-010: only P1 costs are implementation-relevant now; P2/P3 categories are
  modelled for planning only.
- DATA-001/DATA-002/DATA-003: history depth, granularity, and cost-field
  requirements set the shape of the data bill — quantities pending Round D.
- DATA-007: FMP is evaluated against the contract, never assumed adequate, so
  fallback providers must also be costed.
- BUS-004: no cost/benefit statement may imply guaranteed profitability.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Budget ceiling and acceptable recurring spend | Q-007, Round A continuation |
| Data provider shortlist, quotes, and licensing terms per class | Round D (with Rounds C/D symbol lists) |
| Hosting/compute approach and its price basis | Round N |
| Storage, backup, and retention cost drivers | Rounds D/N (OPS-002, retention policy) |
| Research-centre provider costs (P2) | Round L (and Q-003 outcome) |
| Content-production costs (P3) | Round M |
