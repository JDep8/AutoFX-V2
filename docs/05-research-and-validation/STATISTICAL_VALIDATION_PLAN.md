# Statistical Validation Plan
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [LEAKAGE_AND_HOLDOUT_POLICY.md](./LEAKAGE_AND_HOLDOUT_POLICY.md), [EXPERIMENT_REGISTRY_SPEC.md](./EXPERIMENT_REGISTRY_SPEC.md), [BACKTEST_FIDELITY_SPEC.md](./BACKTEST_FIDELITY_SPEC.md), [STRATEGY_ACCEPTANCE_CRITERIA.md](./STRATEGY_ACCEPTANCE_CRITERIA.md)
- **Approval evidence:** None yet

## Purpose

This document plans how AutoFX V2 distinguishes genuine edge from luck and
overfitting. It sets out the validation architecture, the robustness checks,
and the candidate statistical methods to be researched — each with its
limitations stated, because no single statistic is a magic gate. Uncertainty is
always reported; profitability is never guaranteed (BUS-004).

## Scope and decisions this document will own

- The nested, time-aware validation architecture applied to every candidate.
- Robustness requirements: parameter stability, perturbation analysis,
  adversarial cost assumptions.
- The multiple-testing adjustment approach, fed by registry trial counts.
- Evidence-sufficiency rules: minimum trades/opportunities, effective sample
  size, confidence intervals, tail metrics, turnover and capacity.
- Retirement criteria triggers for live strategies (consumed by Gate 8 and
  [MODEL_GOVERNANCE.md](./MODEL_GOVERNANCE.md)).
- Out of scope: pass/fail thresholds themselves — those are pre-registered in
  the acceptance-criteria documents after Round H.

## Structure skeleton

### 1. Nested time-aware validation
Outer/inner split structure respecting time order, purging, and embargo as
defined in [LEAKAGE_AND_HOLDOUT_POLICY.md](./LEAKAGE_AND_HOLDOUT_POLICY.md).
Structure decided in Round H.

### 2. Resampling under serial dependence
Block and bootstrap resampling approaches suited to autocorrelated returns,
with their assumptions and failure modes documented. Method selection is a
Round H research task — candidates are researched, not presumed adequate.

### 3. Robustness and stability
Parameter-stability maps (does the edge survive neighbouring parameters?),
input perturbation, and adversarial cost scenarios (widened spreads, worse
slippage) from the fidelity spec's friction stack. Required tests fixed in
Round H.

### 4. Multiple-testing accounting
Trial counts and selection ancestry from
[EXPERIMENT_REGISTRY_SPEC.md](./EXPERIMENT_REGISTRY_SPEC.md) (QUANT-001) feed
explicit adjustment. Candidate methods to research in Round H, **with
limitations recorded for each** — none is a magic gate:

- Probability of Backtest Overfitting (PBO)
- Deflated Sharpe Ratio
- White's Reality Check
- Hansen's Superior Predictive Ability (SPA) test

This section will state each method's assumptions, what it can and cannot
detect, and how methods are combined with judgement rather than worshipped.

### 5. Evidence sufficiency
Minimum trade counts / opportunity counts, effective sample size under
dependence, confidence intervals on all headline metrics, tail metrics, and
turnover/capacity analysis. Minimums are pre-registered in Round H — no
numbers are invented here.

### 6. Regime and crisis interaction
How validation results are reported per regime segment and reconciled with
[CRISIS_AND_STRESS_FRAMEWORK.md](./CRISIS_AND_STRESS_FRAMEWORK.md) scores,
without excluding uncomfortable regimes. Round H.

### 7. Retirement criteria
Statistical signatures that trigger review, reduction, pausing, or retirement
of a live strategy (Gate 8), monitored in paper/live against the same metrics
used at acceptance. Criteria drafted in Round H, revisited at Round K
monitoring design.

## Known inputs

- QUANT-001: full trial counts are available by construction — the registry is
  the input to every adjustment.
- BUS-004: every performance artefact carries uncertainty measures.
- BUS-003: no test is weakened to improve an apparent result.
- D-002/Q-010: what data validation may legitimately use awaits the Round H
  split decision.
- D-003: truncation effects must be measurable inside the validation story.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Validation architecture (splits, purge/embargo, walk-forward shape) | Round H |
| Which resampling and adjustment methods are adopted, with documented limits | Round H |
| Minimum trades, effective-sample, CI, and tail-metric requirements | Round H (pre-registered) |
| Adversarial-cost scenario definitions | Round H with Round F cost model |
| Retirement-trigger signatures for Gate 8 | Round H → Round K |
| How methods combine into a Gate 3 recommendation without a single magic number | Round H |
