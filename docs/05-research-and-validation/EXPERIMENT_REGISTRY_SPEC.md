# Experiment Registry Specification
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [RESEARCH_PROTOCOL.md](./RESEARCH_PROTOCOL.md), [LEAKAGE_AND_HOLDOUT_POLICY.md](./LEAKAGE_AND_HOLDOUT_POLICY.md), [STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-003)
- **Approval evidence:** None yet

## Purpose

This document specifies the registry that records every experiment ever run —
succeeded, failed, abandoned, or truncated — as an immutable record. Its job is
to make multiple-testing risk visible and auditable: if a thousand
configurations were tried, the registry says a thousand, and no selection story
can pretend otherwise.

## Scope and decisions this document will own

- The record schema for an experiment (identity, hypothesis link, data periods
  touched, configuration, code/data/config hashes, seeds, outcome, status).
- Immutability and append-only rules: records are never edited or deleted;
  corrections are new records referencing the old.
- Research-breadth reporting: counts per family, per hypothesis, per period.
- Multiple-testing accounting: how trial counts feed
  [STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md).
- Out of scope: statistical adjustments themselves, and truncation policy
  content (D-003) — the registry records truncation events, it does not define
  them.

## Structure skeleton

### 1. Record schema
The required fields per experiment record, including the registered hypothesis
reference, exact configuration, data periods consumed (cross-referenced to the
data-period ledger in
[LEAKAGE_AND_HOLDOUT_POLICY.md](./LEAKAGE_AND_HOLDOUT_POLICY.md)), and outcome
status using only the approved status vocabulary. Field list is finalised in
Round G.

### 2. Immutability and provenance
Append-only storage, hash-linking of code/data/config versions (aligned with
VAL-003 deterministic reproducibility), and how a record proves an exact rerun
is possible. Storage mechanism is an architecture question resolved after
Round G requirements are fixed.

### 3. Research-breadth accounting (QUANT-001)
How the registry reproduces "how many things were tried" per family, per
symbol, per timeframe, and per hypothesis, so an audit can reproduce the counts
independently. Reporting views are defined in Round G.

### 4. Multiple-testing linkage
The registry supplies trial counts and selection ancestry to the statistical
plan; candidate adjustment methods and their limitations live in
[STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md) (Round H).
This section defines only what the registry must export.

### 5. Truncation events (D-003)
Every early elimination is recorded with the rule that caused it, so the
truncation policy's effect size is measurable. Depends on D-003 policy content
(Rounds G/H).

### 6. Failed and abandoned runs
Explicit statement that failure is a first-class record: crashed runs,
abandoned lines of research, and negative results are registered with the same
rigour as survivors. Round G confirms the minimum evidence per failed run.

### 7. Audit procedure
How an independent audit (or the Discovery Exit Review) verifies registry
completeness against compute logs and the data-period ledger. Procedure agreed
in Round G.

## Known inputs

- QUANT-001 (`PROPOSED`): full research breadth captured; audit reproduces
  counts — this is the registry's acceptance criterion.
- QUANT-003: a data-period ledger must exist; the registry cross-references it.
- QUANT-004 / D-003: truncation is explicit and visible; the registry is where
  its effects become measurable.
- VAL-003: immutable inputs, seeds, and hashes enable exact reruns.
- BUS-003: no record may be weakened or hidden to improve an apparent result.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Final record schema and mandatory fields | Round G |
| Enforcement: how a run is technically prevented without a registry entry | Round G |
| Breadth-report shapes and audit procedure | Round G |
| What the registry must export for multiple-testing adjustment | Round H |
| Truncation-event fields once D-003 policy content exists | D-003, Rounds G/H |
| Whether V1 experiment history can be imported as evidence or only as context | V1 audit, Q-010, Round H |
