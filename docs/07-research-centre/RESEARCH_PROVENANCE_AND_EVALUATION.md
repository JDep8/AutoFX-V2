# Research Provenance and Evaluation
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (RES-001, RES-002), [MODEL_AND_PROVIDER_GOVERNANCE.md](MODEL_AND_PROVIDER_GOVERNANCE.md), [KNOWLEDGE_CATALOGUE_SPEC.md](KNOWLEDGE_CATALOGUE_SPEC.md), [DATA_LICENSING_AND_RETENTION.md](../04-data/DATA_LICENSING_AND_RETENTION.md)
- **Approval evidence:** None yet

## Purpose

This document defines what must be recorded about every piece of Research
Centre output so that any finding can be traced back to its sources, prompts,
models and reviewers, and defines how research quality is evaluated before an
output is allowed to influence trading logic. It exists because unverifiable
research is worse than no research: it creates confident-sounding claims with
no evidence trail.

## Scope and decisions this document will own

- The mandatory provenance record for every research output (RES-002).
- The epistemic classification of statements (fact, inference, hypothesis,
  recommendation, owner decision).
- Sourcing standards: primary sources, timestamping, snapshots, citation
  honesty.
- The evaluation regime (benchmark set plus human review) gating any change
  that could alter trading logic.
- It does **not** own catalogue storage/organisation (see
  [KNOWLEDGE_CATALOGUE_SPEC.md](KNOWLEDGE_CATALOGUE_SPEC.md)).

## Structure skeleton

### 1. Provenance record — mandatory fields

Per RES-002, every research output records: research question; decision
served; research plan; prompt and prompt version; model, provider and version;
tool calls made; source metadata; citations; retrieval date; artefacts
produced; reviewer; conflicts of interest or conflicting evidence; confidence;
cost; approval status (repository status vocabulary only). Field formats and
storage are resolved in Round L.

### 2. Epistemic classification

Every statement in a research output is labelled as exactly one of: fact
(sourced), inference (derived, with reasoning shown), hypothesis (untested),
recommendation (proposed action), or owner decision (Jacob's recorded choice).
Labelling rules and enforcement resolved in Round L.

### 3. Sourcing standards

Primary sources are used where possible; time-sensitive claims are
timestamped; source snapshots and content hashes are retained where licensing
permits (see
[DATA_LICENSING_AND_RETENTION.md](../04-data/DATA_LICENSING_AND_RETENTION.md)).
Citations are never fabricated — a claim without a verifiable source is
labelled inference or hypothesis, never fact. Snapshot/licensing detail
resolved in Round L.

### 4. Independent challenge pass

Per RES-001, every consequential finding receives an independent challenge
before acceptance; model agreement is never treated as verification. What
qualifies as "consequential" and who/what performs the challenge is resolved
in Round L, consistent with
[MODEL_AND_PROVIDER_GOVERNANCE.md](MODEL_AND_PROVIDER_GOVERNANCE.md).

### 5. Confidence and uncertainty reporting

How confidence is expressed and what evidence must accompany each level.
Consistent with BUS-004: uncertainty is always reported and profitability is
never guaranteed. Scale and rubric resolved in Round L.

### 6. Benchmark set and evaluation regime

A benchmark set of research questions with known-good answers, run before any
change (model, provider, prompt, orchestration) whose output could alter
trading logic, plus mandatory human review of the comparison. Benchmark
composition, pass criteria and review procedure are resolved in Round L; no
thresholds are proposed here.

### 7. Cost and effort accounting

Per-output recording of monetary and time cost so the Research Centre's
budgets ([RESEARCH_CENTRE_PRODUCT_SPEC.md](RESEARCH_CENTRE_PRODUCT_SPEC.md))
can be enforced. Granularity resolved in Round L.

### 8. Retention, audit and reproducibility

How long provenance records are kept, how they are audited, and what "rerun
this research" means given that external sources and models change over time.
Resolved in Round L, aligned with VAL-003's reproducibility discipline where
applicable.

## Known inputs

- RES-002 (`PROPOSED`): the full provenance field list above is mandated by
  the owner brief; no catalogue entry may omit it.
- RES-001 (`PROPOSED`): source evidence plus independent challenge pass on
  every consequential finding.
- BUS-004 (`PROPOSED`): uncertainty always reported; profitability never
  guaranteed.
- D-010 (`OWNER_APPROVED`): planning-only until P1 is live-validated.
- Repository rule (CLAUDE.md): never fabricate citations or evidence;
  ambiguity fails closed into the Question Register.

## Open questions

- Storage format and location of provenance records? → Round L.
- Definition of "consequential finding" triggering the challenge pass? →
  Round L.
- Benchmark set composition, ownership and pass criteria? → Round L.
- Confidence rubric and its calibration review? → Round L.
- Which sources may be snapshotted/hashed under their licences? → Round L,
  with [DATA_LICENSING_AND_RETENTION.md](../04-data/DATA_LICENSING_AND_RETENTION.md);
  YouTube-specific limits → Q-004.
