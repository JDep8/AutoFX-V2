# Product Requirements

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md), [GLOSSARY.md](../00-governance/GLOSSARY.md), [USER_ROLES_AND_JOURNEYS.md](../01-discovery/USER_ROLES_AND_JOURNEYS.md), [INFORMATION_ARCHITECTURE.md](INFORMATION_ARCHITECTURE.md)
- **Approval evidence:** None yet

## Purpose

This document consolidates the product-level view of AutoFX V2: what the
product must do for its single user, in what priority order, and to what
acceptance standard. It works entirely by reference — every requirement is
cited by its catalogue ID and is never restated here, so the
[Requirements Catalogue](../01-discovery/REQUIREMENTS_CATALOGUE.md) remains
the single source of requirement text. It gives Round O a stable frame for
turning requirements into an information architecture and page specifications.

## Scope and decisions this document will own

- The product-level grouping and priority ordering of catalogue requirements
  (which IDs constitute the P1 product surface, per D-010).
- Product-level non-goals and explicit exclusions (per D-008: no customers,
  subscribers, or copy-trading).
- The mapping from requirement groups to the page areas defined in
  [INFORMATION_ARCHITECTURE.md](INFORMATION_ARCHITECTURE.md).
- It does **not** own requirement text (catalogue), page layouts
  ([PAGE_AND_WORKFLOW_SPEC.md](PAGE_AND_WORKFLOW_SPEC.md)), or wireframe
  acceptance ([WIREFRAME_REVIEW.md](WIREFRAME_REVIEW.md)).

## Structure skeleton

### 1. Product vision and success measures
Two or three sentences restating the commercial goals by reference to BUS-001
to BUS-004, plus the measurable KPIs and non-goals once defined. Resolved by
Round A continuation (Q-008) and confirmed in Round O.

### 2. User and operating context
The single-user context (BUS-005, D-008) and what it implies for roles,
permissions, and simplification of the product surface. Resolved: D-008 is
`OWNER_APPROVED`; residual role/permission detail belongs to Round N (security)
and Round O (UX).

### 3. Priority map (P1 / P2 / P3)
Table of catalogue IDs against the D-010 boundary: full Priority 1 platform is
the implementation MVP; RES-* and CONTENT-* remain planning-only until P1 is
`LIVE_VALIDATED`. Resolved: D-010 is `OWNER_APPROVED`; per-ID placement is
confirmed in Round O.

### 4. Requirement consolidation by product capability
One subsection per capability (data platform, research/experimentation, book
generation, approval workflow, accounts and execution, monitoring and ledger,
risk controls, administration/audit), each listing the governing catalogue IDs
and the interview round that finalises its acceptance criteria (Rounds C–K as
marked in the catalogue). No requirement text is duplicated.

### 5. Safety-visibility requirements
Product-level statement of UX-001 (environment, freshness, connection, active
risk, enabled/disabled status, kill-switch state impossible to overlook) and
its relationship to EXEC-010 and RISK-006. Concrete presentation rules are
owned by the IA and page spec; acceptance is defined in Round O.

### 6. Book evidence requirements
Product-level statement of UX-002 — the full evidence set a book detail view
must expose — and its dependency on canonical definitions from Round E (Q-005)
and validation frameworks from Round H (D-004). Detailed content layout is
owned by [PAGE_AND_WORKFLOW_SPEC.md](PAGE_AND_WORKFLOW_SPEC.md).

### 7. Explicit non-goals and exclusions
Items the product deliberately will not do (e.g. no multi-tenancy per D-008;
no auto-publishing per CONTENT-001; no research write-path to live
configuration per RES-003). Confirmed in Round O and the Discovery Exit Review.

### 8. Traceability
Cross-reference into
[TRACEABILITY_MATRIX.md](../00-governance/TRACEABILITY_MATRIX.md) showing each
cited ID's design and evidence links. Maintained continuously; verified at
Exit Review.

## Known inputs (already decided)

- Sole user is Jacob, personal capital — BUS-005 / D-008 (`OWNER_APPROVED`).
- MVP boundary is the full Priority 1 platform; P2/P3 planning-only —
  BUS-006 / D-010 (`OWNER_APPROVED`).
- Eight-class CFD universe designed-for from day one, FX-first phased rollout —
  DATA-008 / D-009 (`OWNER_APPROVED`).
- Drawdown direction: realised peak-relative drawdown is the canonical approval
  metric; MTM excursion and heat are separate always-visible live controls —
  RISK-006 / D-001 (`OWNER_APPROVED` direction only).
- Wireframes are gated behind the exact phrase `AUTHORISE WIREFRAME ONLY` —
  UX-003 and the repository no-build gate.

## Open questions

- Measurable business KPIs and explicit non-goals → Q-008 (Round A
  continuation).
- Backtest-vs-live degradation tolerance the owner will accept → Q-009
  (Round A continuation, refined Round F).
- Default drawdown numbers, heat cap survival, translation rule → Q-005
  (Round E).
- Which page areas beyond the mandated minimum (if any) enter the P1 product
  surface → Round O.
- Acceptance criteria for every `→ Round X` item cited from the catalogue →
  the round named per item.
