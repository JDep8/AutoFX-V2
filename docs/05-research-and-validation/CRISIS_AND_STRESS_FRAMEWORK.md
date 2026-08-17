# Crisis and Stress Framework
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-004), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (VAL-004), [BACKTEST_FIDELITY_SPEC.md](./BACKTEST_FIDELITY_SPEC.md), [BOOK_ACCEPTANCE_CRITERIA.md](./BOOK_ACCEPTANCE_CRITERIA.md)
- **Approval evidence:** None yet

## Purpose

This document defines how strategies and books are tested against the worst
the market has actually done — and against synthetic degradations of the
conditions they depend on. Measured historical episodes are chosen before
candidate outcomes are seen, so crisis testing can never become a curve-fit.
Synthetic stresses complement measured episodes; they never replace them
(D-004).

## Scope and decisions this document will own

- The criteria for selecting measured historical crisis episodes, and the rule
  that selection happens **before** seeing candidate outcomes.
- Per-strategy crisis scores and the portfolio resilience score, and how both
  integrate into book approval (Gate 4).
- The synthetic stress catalogue and its complementary (never substitute) role.
- The worst-period servicing process for every strategy and book.
- Out of scope: pass thresholds (pre-registered via the acceptance-criteria
  documents) and episode-specific data sourcing (Round D contracts).

## Structure skeleton

### 1. Measured historical episodes (D-004)
The episode-selection criteria (severity, mechanism diversity, data
availability, relevance to the traded universe) and the governance rule that
the episode list is fixed and owner-approved before any candidate outcome is
observed. Episode list and criteria are decided in Round H; no episodes are
named here to avoid pre-empting that decision.

### 2. Per-strategy crisis scores
How each strategy's behaviour across the fixed episodes is summarised into a
crisis score with full-cost reproduction via
[BACKTEST_FIDELITY_SPEC.md](./BACKTEST_FIDELITY_SPEC.md). Scoring definition is
a Round H decision.

### 3. Portfolio resilience score
The book-level aggregation — including correlation behaviour under stress —
and its formal place in Gate 4 approval evidence
([BOOK_ACCEPTANCE_CRITERIA.md](./BOOK_ACCEPTANCE_CRITERIA.md)). Round H defines
the aggregation; Round I integrates it into book rules.

### 4. Synthetic stress catalogue
Complementary synthetic stresses: spread widening, slippage inflation, price
gaps, correlation convergence, volatility shocks, missing data, latency
spikes, outages, broker rejection storms. Each stress states what real-world
failure it proxies. Catalogue contents fixed in Round H; parameters come from
measured data where possible, never invented.

### 5. Worst-period servicing process
For every strategy and book: identify the worst rolling and peak-to-trough
periods, reproduce them with full costs, explain the failure mode in plain
language, test whether the conditions could recur, define remediation or
retirement, and monitor the same signatures in paper/live. Process template is
approved in Round H and consumed by Gate 8 monitoring.

### 6. Regime coverage without exclusion
Recent structural shifts and older regimes are both tested; no regime is
excluded merely because it is inconvenient or "different now". Any exclusion
requires an owner-approved, recorded justification. Rules set in Round H with
[LEAKAGE_AND_HOLDOUT_POLICY.md](./LEAKAGE_AND_HOLDOUT_POLICY.md) segmentation.

### 7. Interaction with the data-period ledger
Stress design consumes data periods; those dates are recorded in the ledger
(QUANT-003) so stress construction cannot silently contaminate holdout data.
Round H.

## Known inputs

- D-004 (`PROPOSED`, open): recommendation is retention of the V1-era crisis
  framework with episodes chosen before outcomes are seen — Jacob decides in
  Round H.
- VAL-004: measured episodes with explicit criteria; synthetic complements
  never replace; per-strategy and portfolio scores required.
- UX-002: crisis and regime evidence must be visible on the book detail page.
- BUS-004: crisis results are reported with uncertainty, never as guarantees.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Retain/replace/supersede the V1-era crisis framework | D-004, Round H |
| Episode-selection criteria and the fixed episode list | Round H (before outcomes seen) |
| Crisis-score and resilience-score definitions | Round H |
| Synthetic stress parameterisation from measured data | Round H with Round D inputs |
| Worst-period servicing template and its Gate 8 monitoring hooks | Round H → Round K |
| How resilience scores gate book approval | Round I, [BOOK_ACCEPTANCE_CRITERIA.md](./BOOK_ACCEPTANCE_CRITERIA.md) |
