# Research Protocol
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [EXPERIMENT_REGISTRY_SPEC.md](./EXPERIMENT_REGISTRY_SPEC.md), [LEAKAGE_AND_HOLDOUT_POLICY.md](./LEAKAGE_AND_HOLDOUT_POLICY.md), [STRATEGY_TAXONOMY.md](./STRATEGY_TAXONOMY.md)
- **Approval evidence:** None yet

## Purpose

This document defines how strategy research is conducted in AutoFX V2 so that
every result can be trusted. It makes hypothesis-first registration mandatory,
requires an economic or microstructure rationale before any fitting begins, and
ensures that every configuration ever attempted is tracked. It exists so that
research breadth can never be hidden and apparent results can never be
cherry-picked.

## Scope and decisions this document will own

- The mandatory research lifecycle: hypothesis registration → rationale review
  → baseline → experiment → registry record → gate evaluation.
- The rule that transparent, simple baselines are established before any
  machine-learning approach is attempted.
- What counts as a "registered hypothesis" and when a hypothesis may be revised
  versus when a new registration is required.
- Interfaces to the experiment registry, leakage policy, and Gate 2
  (experiment valid) / Gate 3 (strategy eligible).
- Out of scope: acceptance thresholds (see
  [STRATEGY_ACCEPTANCE_CRITERIA.md](./STRATEGY_ACCEPTANCE_CRITERIA.md)) and
  statistical machinery (see
  [STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md)).

## Structure skeleton

### 1. Hypothesis-first registration
What a registration must contain (hypothesis statement, target instruments and
timeframes, expected behaviour, falsification condition) and when it must be
recorded — always before fitting. Registration format and required fields are
decided in Round G.

### 2. Economic and microstructure rationale (QUANT-002)
Each strategy must record why the edge should exist (behavioural, structural,
flow-based, session-based, or cost-based reasoning), not only that a pattern
was discovered. The review standard and who signs the rationale at Gate 3 are
settled in Round G.

### 3. Transparent baselines before ML
The requirement that a simple, explainable rules-based baseline is measured on
the same data before any statistical or ML variant, so uplift is attributable.
Which baseline classes are mandatory per strategy family is a Round G decision,
informed by [STRATEGY_TAXONOMY.md](./STRATEGY_TAXONOMY.md).

### 4. Full research-breadth tracking (QUANT-001)
Every configuration attempted — including abandoned, truncated, and failed runs
— is recorded in the experiment registry so multiple-testing risk is auditable.
Record structure is owned by
[EXPERIMENT_REGISTRY_SPEC.md](./EXPERIMENT_REGISTRY_SPEC.md); the protocol here
states that no run may execute without a registry entry. Enforcement mechanism
is a Round G decision.

### 5. Data-use discipline
Which data periods a researcher may touch at each lifecycle stage, deferring
entirely to [LEAKAGE_AND_HOLDOUT_POLICY.md](./LEAKAGE_AND_HOLDOUT_POLICY.md)
and D-002. Round H resolves the period split.

### 6. Truncation interaction (D-003)
How early-elimination rules are declared inside a research plan so truncation
is visible, not implicit. Policy content is owned by D-003 (Rounds G/H).

### 7. Roles, review, and record-keeping
Who reviews registrations and rationales (Jacob is sole user per D-008), how
reviews are evidenced, and how the protocol links to the Traceability Matrix.
Round G defines the review cadence.

## Known inputs

- QUANT-001: every configuration attempted is tracked (`PROPOSED`, Round G).
- QUANT-002: economic/microstructure rationale required (`PROPOSED`, Round G).
- QUANT-004 / D-003: truncation must be an explicit, owner-approved policy.
- BUS-003: evidence standards are hard constraints, never weakened for results.
- BUS-004: profitability is never guaranteed; uncertainty is always reported.
- D-008: Jacob is the sole user; the protocol serves one researcher-owner.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Exact registration fields and the revision-vs-new-registration rule | Round G |
| Which baseline classes are mandatory before ML per family | Round G |
| How registry enforcement is made non-bypassable | Round G |
| Rationale review standard and Gate 3 evidence format | Round G |
| Truncation policy content and effect measurement | D-003, Rounds G/H |
| Data-period split governing what research may touch | D-002, Q-010, Round H |
