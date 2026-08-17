# Model Governance
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [RESEARCH_PROTOCOL.md](./RESEARCH_PROTOCOL.md), [STRATEGY_TAXONOMY.md](./STRATEGY_TAXONOMY.md), [LEAKAGE_AND_HOLDOUT_POLICY.md](./LEAKAGE_AND_HOLDOUT_POLICY.md), [STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md)
- **Approval evidence:** None yet

## Purpose

This document governs statistical and machine-learning models used inside
strategies: how their features, labels, training, and inference are specified,
monitored, and retired. Its central safety rule is that a live book never
self-modifies from research output — any change ships as a separately tested
and approved version through the same gates as everything else.

## Scope and decisions this document will own

- The model specification record: features, labels, horizons, training data
  lineage, and assumptions.
- Training cadence and retraining rules, including what a retrain is (a new
  version, never an in-place mutation of a live model).
- Inference-time requirements: latency, calibration, missing-data behaviour.
- Drift detection, explainability expectations, and retirement.
- The no-self-modification rule for live books.
- Out of scope: which ML techniques are used (a research outcome under
  [RESEARCH_PROTOCOL.md](./RESEARCH_PROTOCOL.md)) and Research Centre
  multi-model orchestration (RES-001..RES-004, Round L, planning-only).

## Structure skeleton

### 1. Model specification record
Required fields per model: feature definitions with point-in-time discipline
(DATA-004), label construction, prediction horizon, training-period lineage in
the data-period ledger (QUANT-003), and the transparent baseline it must beat
(RESEARCH_PROTOCOL.md section 3). Record format decided in Round G.

### 2. Training cadence and versioning
When and how retraining happens; every retrain produces a new, immutable
model version with its own registry entry and gate evidence — never an edit to
a running model. Cadence policy is a Round G decision, informed by drift
findings.

### 3. Inference requirements
Latency budgets compatible with the execution path (Round J inputs),
calibration checks (do predicted probabilities mean what they say?), and
fail-closed behaviour on missing or stale features — no inference on inputs
that violate the data contract (DATA-005). Requirements set in Rounds G/J.

### 4. Drift detection
Feature drift, label drift, and performance drift monitoring in paper/live,
tied to the same worst-period signatures monitored by
[CRISIS_AND_STRESS_FRAMEWORK.md](./CRISIS_AND_STRESS_FRAMEWORK.md). Detection
approach chosen in Round G; live monitoring design lands in Round K.

### 5. Explainability
What must be explainable about a model's decisions at Gate 3 review and in the
trade ledger (FR-004: entry/exit reasons in painful detail), given QUANT-002's
rationale requirement. Standard set in Round G.

### 6. Retirement
Statistical and operational triggers for retiring a model version, aligned
with the retirement criteria in
[STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md) and Gate 8
outcomes (continue/reduce/pause/retire). Round G/K.

### 7. No self-modification of live books
A live book never ingests research output directly: recommendations flow to
new versions that pass Gates 2–7 independently before any live exposure
(mirrors RES-003's no-write-path rule). Enforcement mechanics decided in
Rounds G/J; this rule itself is not negotiable within this document's scope —
only Jacob could change it via the Decision Log.

## Known inputs

- QUANT-002: models need economic/microstructure rationale, not just fit.
- QUANT-003 / D-002: training data lineage must live in the data-period ledger.
- VAL-003: model training and inference must be exactly reproducible from
  recorded versions, seeds, and hashes.
- RES-003 (`PROPOSED`): research output can recommend experiments but never
  directly modify a live strategy or book.
- EXEC-002: version-specific approval — a new model version means a new
  approval, disabled by default.
- Glossary "Fail closed": missing safety-relevant input means no new entries.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Model record format and mandatory fields | Round G |
| Retraining cadence and what triggers an out-of-cycle retrain | Round G |
| Inference latency budget compatible with execution | Round J |
| Calibration and missing-data policies per model class | Round G |
| Drift metrics and their monitoring home in live operations | Rounds G/K |
| Explainability standard acceptable to Jacob at Gate 3 | Round G |
