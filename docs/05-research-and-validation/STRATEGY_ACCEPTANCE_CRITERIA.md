# Strategy Acceptance Criteria
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [RESEARCH_PROTOCOL.md](./RESEARCH_PROTOCOL.md), [STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md), [CRISIS_AND_STRESS_FRAMEWORK.md](./CRISIS_AND_STRESS_FRAMEWORK.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-003)
- **Approval evidence:** None yet

## Purpose

This document defines Gate 3 — the checkpoint at which an individual strategy
becomes eligible for book construction. It states what evidence a candidate
must present, how candidates are ranked without hiding failures, and how the
truncation policy stays visible throughout. Passing Gate 3 makes a strategy
*eligible*, never *approved for live*, and never implies profitability.

## Scope and decisions this document will own

- The Gate 3 evidence pack: what a candidate strategy must show, drawn from
  the research protocol, statistical plan, fidelity spec, and crisis
  framework.
- Candidate ranking rules that preserve full research breadth — failed
  candidates and total trial counts are always shown alongside survivors.
- Truncation-policy visibility (D-003): where and how early eliminations are
  disclosed in Gate 3 evidence.
- Out of scope: threshold values (pre-registered after Rounds G/H, approved by
  Jacob) and book-level rules
  ([BOOK_ACCEPTANCE_CRITERIA.md](./BOOK_ACCEPTANCE_CRITERIA.md)).

## Structure skeleton

### 1. Gate 3 evidence pack
The required contents: registered hypothesis and rationale (QUANT-002),
registry ancestry with trial counts (QUANT-001), validation results with
confidence intervals (BUS-004), crisis scores, worst-period analysis, cost
sensitivity, and data-period ledger confirmation of no leakage. Pack contents
fixed in Round G, thresholds in Round H.

### 2. Pre-registered thresholds
All pass/fail thresholds are written down and owner-approved **before**
candidates are evaluated against them, so criteria cannot drift toward
whatever survived. Threshold values are decided in Rounds G/H — none appear in
this skeleton by design.

### 3. Candidate ranking without hidden failures
Ranking views always display research breadth: how many candidates were
attempted, how many were truncated and by which rule, and how many failed each
criterion. A survivor is never presented without its denominator. Reporting
format is a Round G decision with
[EXPERIMENT_REGISTRY_SPEC.md](./EXPERIMENT_REGISTRY_SPEC.md).

### 4. Truncation-policy visibility (D-003)
The truncation policy's text, its owner approval, and its measured effect on
the candidate population are part of every Gate 3 evidence pack — never hidden
inside implementation details. Depends on D-003 resolution (Rounds G/H).

### 5. Eligibility outcome and status handling
What Gate 3 passage means (eligible for book construction only), the status
labels applied (from the approved vocabulary only), and re-evaluation rules
when data, code, or policy versions change. Round G.

### 6. Failure, appeal, and re-entry
How a failed candidate is recorded, whether and how a revised candidate
re-enters (as a new registered hypothesis per
[RESEARCH_PROTOCOL.md](./RESEARCH_PROTOCOL.md)), and how re-entries count in
multiple-testing accounting. Round G.

## Known inputs

- QUANT-001/QUANT-002: breadth tracking and rationale are non-negotiable gate
  inputs (`PROPOSED`, Round G).
- QUANT-004 / D-003: truncation is explicit, owner-approved, and visible.
- BUS-003: criteria are never weakened to admit an attractive candidate.
- BUS-004: eligibility never implies guaranteed profitability; uncertainty is
  reported in every pack.
- Glossary Gate 1–8 architecture: Gate 3 = strategy eligible, distinct from
  book eligibility (Gate 4) and live approval (Gates 5–7).

## Open questions

| Question | Resolved by |
|----------|-------------|
| Evidence-pack contents and format | Round G |
| Threshold values (statistical, crisis, cost-sensitivity) | Rounds G/H, pre-registered, owner-approved |
| Ranking/report format showing full denominators | Round G |
| Truncation policy content and its measured effect display | D-003, Rounds G/H |
| Re-evaluation triggers on version changes | Round G |
| Minimum trades / effective-sample requirements feeding Gate 3 | Round H ([STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md)) |
