# Trade Review Workflow
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (RES-003, FR-004), [RESEARCH_CENTRE_PRODUCT_SPEC.md](RESEARCH_CENTRE_PRODUCT_SPEC.md), [RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md), [KNOWLEDGE_CATALOGUE_SPEC.md](KNOWLEDGE_CATALOGUE_SPEC.md)
- **Approval evidence:** None yet

## Purpose

This document defines how the Research Centre reviews actual trades taken by
the live platform: what a review examines, what it may produce, and — most
importantly — what it may never do. A trade review can generate insight and
recommend a research experiment, but it can never directly modify a live
strategy or book (RES-003). The workflow keeps learning from live trading
separated from control of live trading.

## Scope and decisions this document will own

- The trigger conditions, inputs, steps and outputs of a trade review.
- The hard boundary between review output and live configuration (RES-003).
- How review findings become approval-gated research ideas rather than
  direct changes.
- It does **not** own the trade ledger itself (FR-004, a Priority 1 concern)
  or Gate 8 continue/reduce/pause/retire decisions, which remain Jacob's
  platform-side controls.

## Structure skeleton

### 1. Review triggers and cadence

When a trade review starts: scheduled cadence, threshold-based triggers
(e.g. unusual outcomes flagged by the platform), or owner request. Which
triggers exist and their definitions are resolved in Round L; no numeric
thresholds are proposed here.

### 2. Inputs

What a review reads: the trade ledger record (FR-004 — entry/exit reasons,
monitor observations, order/fill events, provenance), the strategy and book
versions involved, and relevant market/news context. All access is read-only.
Input contract detail follows Round K (ledger spec) and is confirmed in
Round L.

### 3. Review procedure and roles

The steps of a review and which specialist roles
([RESEARCH_CENTRE_PRODUCT_SPEC.md](RESEARCH_CENTRE_PRODUCT_SPEC.md)) perform
them — e.g. primary researcher drafts, sceptical verifier challenges,
execution reviewer checks fill/slippage context, compliance reviewer checks
boundary adherence. Role assignment resolved in Round L.

### 4. Permitted outputs

A review may produce: findings (classified per
[RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md)
as fact/inference/hypothesis/recommendation), catalogue entries, and
**recommended research experiments** submitted to the approval-gated ideas
backlog. Output templates resolved in Round L.

### 5. Prohibited outputs — the no-write boundary

Hard rule (RES-003): no write path exists from trade review to any live
strategy, book, parameter, or account configuration. A recommendation only
becomes change through the platform's own experiment → validation → approval
gates, each requiring Jacob's explicit decision. How this boundary is
technically enforced is an architecture question for Round L (design) after
Rounds F–K define the P1 gate machinery.

### 6. Escalation of safety-relevant observations

If a review surfaces something safety-relevant (e.g. suspected execution
defect or reconciliation gap), it is escalated to Jacob and the Question
Register immediately — it does not wait in the backlog. Escalation route
resolved in Round L, consistent with the fail-closed rule in CLAUDE.md.

### 7. Record-keeping

Every review is itself a research output: full provenance (RES-002), reviewer
identity, confidence, cost, and approval status, stored per
[KNOWLEDGE_CATALOGUE_SPEC.md](KNOWLEDGE_CATALOGUE_SPEC.md). Resolved in
Round L.

## Known inputs

- RES-003 (`PROPOSED`): trade review may recommend experiments but can never
  directly modify a live strategy or book; no write path to live
  configuration.
- FR-004 (`PROPOSED`): the trade ledger records every trade in full detail
  with reproducible provenance — the review's primary input.
- RES-002 (`PROPOSED`): reviews carry full research provenance.
- D-010 (`OWNER_APPROVED`): this workflow is planning-only until P1 is
  live-validated.
- Gate 8 (Glossary): continue/reduce/pause/retire decisions belong to the
  platform's gate architecture, not to this workflow.

## Open questions

- Review triggers, cadence and any threshold definitions? → Round L.
- Role assignment and independence within a review? → Round L.
- Output templates and how recommendations enter the ideas backlog? →
  Round L.
- Technical enforcement of the no-write boundary? → Round L, dependent on
  Rounds F–K architecture.
- Escalation route for safety-relevant observations? → Round L.
