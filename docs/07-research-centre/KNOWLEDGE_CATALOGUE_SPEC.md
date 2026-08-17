# Knowledge Catalogue Specification
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md), [RESEARCH_CENTRE_PRODUCT_SPEC.md](RESEARCH_CENTRE_PRODUCT_SPEC.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (RES-002), [GLOSSARY.md](../00-governance/GLOSSARY.md)
- **Approval evidence:** None yet

## Purpose

This document specifies the durable catalogue in which every Research Centre
finding lives, with its provenance and status, so that knowledge accumulates
instead of evaporating between sessions. The catalogue is the Research
Centre's long-term memory: it prevents repeated research, exposes conflicting
findings, and makes every claim's evidence trail findable years later.

## Scope and decisions this document will own

- The catalogue entry model: what a "finding" is and what fields it carries.
- Lifecycle states, versioning and supersession of entries.
- Organisation, search and duplicate detection.
- The librarian role's responsibilities over the catalogue.
- It does **not** own the provenance field definitions themselves (see
  [RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md))
  or the P1 experiment registry
  ([EXPERIMENT_REGISTRY_SPEC.md](../05-research-and-validation/EXPERIMENT_REGISTRY_SPEC.md)),
  which remains the system of record for quantitative experiments.

## Structure skeleton

### 1. Entry model

What one catalogue entry contains: the finding itself, its epistemic class
(fact/inference/hypothesis/recommendation/owner decision), full provenance
per RES-002, links to the originating request and any trade review, and its
status drawn only from the repository status vocabulary (`PROPOSED`,
`OWNER_APPROVED`, `REJECTED`, `SUPERSEDED`, etc. — never invented labels).
Field-level schema resolved in Round L.

### 2. Lifecycle and status transitions

How an entry moves between statuses, who may transition it (Jacob for any
owner-approval), and the rule that history is never erased — superseded
entries are marked, not deleted, mirroring the Decision Log discipline.
Transition rules resolved in Round L.

### 3. Versioning and supersession

How a finding is updated when new evidence arrives: new version linked to the
old, with the conflict recorded rather than silently overwritten. Mechanics
resolved in Round L.

### 4. Organisation and taxonomy

How entries are grouped and tagged — by decision served, asset class, strategy
family ([STRATEGY_TAXONOMY.md](../05-research-and-validation/STRATEGY_TAXONOMY.md)),
and backlog lane — so related knowledge is discoverable. Taxonomy resolved in
Round L.

### 5. Search and duplicate detection

How intake checks the catalogue before new research is approved, preventing
paid re-answering of answered questions. Required capability; mechanism
resolved in Round L.

### 6. Conflict surfacing

How contradictory findings are detected, linked and flagged for the sceptical
verifier and, where consequential, for Jacob. Procedure resolved in Round L.

### 7. Librarian role responsibilities

The librarian role ([RESEARCH_CENTRE_PRODUCT_SPEC.md](RESEARCH_CENTRE_PRODUCT_SPEC.md))
curates the catalogue: entry quality, taxonomy hygiene, supersession
housekeeping, and periodic review of stale entries. Whether human or
AI-agent-assisted is resolved in Round L.

### 8. Access, retention and audit

Read/write permissions (single-owner model per D-008), retention of entries
and their source snapshots (licensing limits per
[VIDEO_AND_EXTERNAL_CONTENT_POLICY.md](VIDEO_AND_EXTERNAL_CONTENT_POLICY.md)
and [DATA_LICENSING_AND_RETENTION.md](../04-data/DATA_LICENSING_AND_RETENTION.md)),
and audit of catalogue integrity. Resolved in Round L / Round N (security).

## Known inputs

- RES-002 (`PROPOSED`): every entry carries full provenance; no fabricated
  citations.
- D-008 (`OWNER_APPROVED`): single-owner access model; no external users.
- D-010 (`OWNER_APPROVED`): the catalogue is specified now, built only after
  P1 is live-validated.
- Repository rule (CLAUDE.md): documents and registers are the source of
  truth, never conversational memory — the catalogue extends this principle
  to research findings.

## Open questions

- Entry schema, storage technology and format? → Round L (technology choice
  also constrained by Round N security requirements).
- Status transition rules and review cadence for stale entries? → Round L.
- Taxonomy: which dimensions, who maintains them? → Round L.
- Duplicate-detection mechanism at intake? → Round L.
- Relationship and boundary with the P1 experiment registry — what lives
  where? → Round L, after Round G defines the registry.
- Retention limits for snapshots of externally licensed content? → Round L,
  with Q-004 for video content.
