# Research Centre Product Specification
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-008, D-010), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (RES-001..RES-004), [MODEL_AND_PROVIDER_GOVERNANCE.md](MODEL_AND_PROVIDER_GOVERNANCE.md), [RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md), [KNOWLEDGE_CATALOGUE_SPEC.md](KNOWLEDGE_CATALOGUE_SPEC.md)
- **Approval evidence:** None yet

## Purpose

This document defines what the Deep Research Centre (Priority 2) is as a
product: who uses it, how research work enters, is approved, prioritised,
budgeted and measured, and which specialist roles perform it. It exists so the
Research Centre can be planned honestly now and built only after Priority 1 is
live-validated (D-010). It is a planning artefact — nothing in it authorises
implementation.

## Scope and decisions this document will own

- The Research Centre's user model, intake workflow, approval workflow,
  prioritisation model, budgets, SLAs, and success metrics.
- The definition and responsibilities of the specialist research roles.
- The governance of the approval-gated ideas backlog.
- It does **not** own model/provider selection (see
  [MODEL_AND_PROVIDER_GOVERNANCE.md](MODEL_AND_PROVIDER_GOVERNANCE.md)),
  provenance/evaluation standards (see
  [RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md)),
  or the trade-review process (see
  [TRADE_REVIEW_WORKFLOW.md](TRADE_REVIEW_WORKFLOW.md)).

## Structure skeleton

### 1. Users and access

Who interacts with the Research Centre and with what permissions. D-008 fixes
the sole human user as Jacob; this section records how specialist roles (human
and/or AI-agent) relate to that single-owner model. Resolved in Round L.

### 2. Research request intake

How a research question enters the system: required fields (question, decision
served, urgency, constraints), who may raise requests, and how duplicates are
detected against the knowledge catalogue. Resolved in Round L.

### 3. Approval workflow

The gate between "idea raised" and "work started": what Jacob approves, what
evidence accompanies a request, and what states a request may occupy (using
only the repository status vocabulary). Resolved in Round L.

### 4. Prioritisation model

How competing approved requests are ordered — the criteria (decision impact,
cost, urgency, dependency on P1 evidence) and who applies them. The concrete
scheme is an open Round L decision; no ranking formula is assumed here.

### 5. Budgets and cost controls

How research spend (model/API usage, data purchases, human time) is budgeted,
tracked per request, and capped. Budget context is now decided: the D-019
operating ceiling (AUD 400/month, every expense pre-approved by Jacob);
per-request research allocations within it are set by Jacob in Round L.

### 6. SLAs and turnaround expectations

What response and completion expectations apply per request class. No
durations are proposed here; Round L defines them once the operating model
(human effort vs automated effort) is decided.

### 7. Success metrics

How the Research Centre itself is judged — decision usefulness, provenance
completeness (RES-002), challenge-pass coverage (RES-001), and cost per
answered question. Metric definitions resolved in Round L; profitability of
any resulting strategy is never a guaranteed outcome (BUS-004).

### 8. Specialist roles

Definition, inputs, outputs and independence rules for each role: orchestrator,
primary researcher, sceptical verifier, quantitative reviewer, execution
reviewer, compliance reviewer, librarian. Whether each role is a human
activity, an AI agent, or a hybrid — and which model/provider constraints
apply — is resolved in Round L under
[MODEL_AND_PROVIDER_GOVERNANCE.md](MODEL_AND_PROVIDER_GOVERNANCE.md).

### 9. Approval-gated ideas backlog

A single backlog of research ideas across five lanes: strategies, data,
validation, execution, and product improvements. Each idea is approval-gated
before any work or spend; backlog states, lane definitions and pruning rules
are resolved in Round L.

### 10. Interfaces with the Priority 1 platform

Read-only touchpoints with the experiment registry, trade ledger and knowledge
catalogue, and the hard boundary that research output can never write to live
configuration (RES-003). Interface detail follows the P1 architecture work
(Rounds F–K) and is confirmed in Round L.

### 11. Non-goals and boundaries

Explicit exclusions: no direct modification of live strategies or books
(RES-003), no headless automation of paid consumer AI UIs while Q-003 is
BLOCKED (RES-004), no customer-facing research product (D-008).

## Known inputs

- D-008 (`OWNER_APPROVED`): Jacob is the sole user; no customers or clients.
- D-010 / BUS-006 (`OWNER_APPROVED`): Priority 2 is planning-and-architecture
  only until Priority 1 is live-validated.
- RES-001 (`PROPOSED`): multi-model orchestration only where it materially
  improves quality; agreement never equated with truth.
- RES-002 (`PROPOSED`): full provenance on every research output.
- RES-003 (`PROPOSED`): trade review may recommend experiments, never modify
  live strategies or books.
- RES-004 (`PROPOSED`): headless consumer-AI automation is BLOCKED pending
  Q-003 resolution.

## Open questions

- Which specialist roles are human, AI-agent, or hybrid, and how is role
  independence preserved? → Round L.
- Intake fields, approval states and backlog lane rules? → Round L.
- Prioritisation criteria and who applies them? → Round L.
- Research budgets and cost caps? → Round L, within the D-019 ceiling
  (AUD 400/month, per-expense approval).
- SLA classes and turnaround expectations? → Round L.
- Success metric definitions and reporting cadence? → Round L.
- Does any Research Centre capability depend on consumer-UI automation, and if
  so what is the fallback? → Q-003 / Round L.
