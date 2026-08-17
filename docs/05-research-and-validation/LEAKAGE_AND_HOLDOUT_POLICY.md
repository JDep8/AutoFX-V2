# Leakage and Holdout Policy
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-002), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-010), [EXPERIMENT_REGISTRY_SPEC.md](./EXPERIMENT_REGISTRY_SPEC.md), [STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md)
- **Approval evidence:** None yet

## Purpose

This document keeps the future out of the past. It defines how every data
period is assigned a single role, how the final holdout stays locked and
selection-untouched, and what happens if honest analysis shows no credible
untouched holdout remains. Leakage here would invalidate all downstream
evidence, so this policy fails closed.

## Scope and decisions this document will own

- The data-period ledger: which dates served research, feature engineering,
  fitting, validation, selection, portfolio construction, stress design, and
  final testing (QUANT-003).
- The final-holdout lock: tested only once, after the book and its thresholds
  are pre-registered.
- The "no credible holdout" escape route: honest declaration plus prospective
  shadow/paper validation design (D-002, Q-010).
- Purging/embargo, walk-forward, and regime-segmentation rules for time-aware
  splits.
- Out of scope: statistical tests run on splits
  ([STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md)) and
  execution realism ([BACKTEST_FIDELITY_SPEC.md](./BACKTEST_FIDELITY_SPEC.md)).

## Structure skeleton

### 1. Data-period ledger (QUANT-003)
The ledger schema: every date range per symbol carries exactly one role —
research / features / fitting / validation / selection / portfolio
construction / stress design / final testing — and a period never serves both
development and untouched testing. Schema and custody are settled in Round H.

### 2. Build/test split decision (D-002)
The actual period assignment. Blocked on V1 audit evidence of what data
genuinely influenced V1 selection (Q-010); Jacob decides the split in Round H.
No dates are proposed here — proposing them now would be plausible filler.

### 3. Final holdout lock
The holdout is locked before selection begins, is touched by no research
activity, and is tested exactly once — after the candidate book and its
acceptance thresholds are pre-registered in writing. Lock mechanics and
pre-registration format are Round H decisions.

### 4. No-credible-holdout declaration
If the V1 audit shows all candidate holdout periods were already touched by
selection, this policy requires saying so plainly and designing prospective
shadow/paper validation as the honest substitute (D-002, Q-010, Gate 6).
Design of that prospective protocol belongs to Round H with Round F fidelity
inputs.

### 5. Purging and embargo
How overlapping labels and serial correlation are handled at split boundaries
(purging) and how post-split gaps (embargo) are applied. Parameters are Round H
decisions; none are invented here.

### 6. Walk-forward and regime segmentation
Walk-forward evaluation structure and how regimes are segmented for reporting
without arbitrary exclusion of uncomfortable periods (aligned with
[CRISIS_AND_STRESS_FRAMEWORK.md](./CRISIS_AND_STRESS_FRAMEWORK.md)). Round H.

### 7. Leakage vectors beyond price data
Point-in-time discipline for news/macro events (DATA-004), revision vintages,
feature stores, and normalisation statistics computed across split boundaries.
Controls specified in Round H with Round D data-contract inputs.

### 8. Breach handling
Any discovered leakage fails closed: affected experiments are marked in the
registry, results are quarantined from evidence, and a blocking entry is
raised in the Question Register. Procedure confirmed in Round H.

## Known inputs

- D-002 (`PROPOSED`, open): each period serves development/selection **or**
  untouched testing, never both; decision requires V1 audit evidence.
- Q-010 (OPEN): whether historical data was already consumed by V1 selection.
- QUANT-003: the ledger is a hard requirement with Gate-level acceptance.
- DATA-001: at least five years of history targeted (ten preferred) — the
  split must respect whatever depth Gate 1 certifies; no dates assumed.
- Glossary: canonical definitions of Holdout, Leakage, Point-in-time.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Which dates served V1 selection (holdout eligibility) | Q-010, V1 audit |
| Final build/test period assignment | D-002, Round H (Jacob) |
| Purge/embargo parameters and walk-forward structure | Round H |
| Pre-registration format for book + thresholds before holdout touch | Round H |
| Prospective shadow/paper design if no credible holdout remains | Round H, Gate 6 |
| Regime segmentation boundaries without arbitrary exclusion | Round H |
