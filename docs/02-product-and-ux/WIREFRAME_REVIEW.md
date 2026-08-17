# Wireframe Review

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [PAGE_AND_WORKFLOW_SPEC.md](PAGE_AND_WORKFLOW_SPEC.md), [INFORMATION_ARCHITECTURE.md](INFORMATION_ARCHITECTURE.md), [USER_ROLES_AND_JOURNEYS.md](../01-discovery/USER_ROLES_AND_JOURNEYS.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md)
- **Approval evidence:** None yet

## Purpose

This document defines how wireframes — if and when Jacob authorises them — are
reviewed before they can be called done. It sets the visual self-review
checklist and the traceability check proving that every approved user journey
appears in the wireframe. Wireframes are a planning artefact only: they are
gated behind the exact phrase `AUTHORISE WIREFRAME ONLY` and are static or
mock-data prototypes with no backend, database, broker, secrets, publishing,
or live actions.

## Scope and decisions this document will own

- The gate preconditions that must hold before wireframe work may start.
- The visual self-review checklist applied to every wireframed page.
- The journey-traceability method: how approved journeys are mapped to
  wireframe evidence.
- The review record format and its possible outcomes.
- It does **not** own page content obligations
  ([PAGE_AND_WORKFLOW_SPEC.md](PAGE_AND_WORKFLOW_SPEC.md)) or the page
  inventory ([INFORMATION_ARCHITECTURE.md](INFORMATION_ARCHITECTURE.md)).

## Structure skeleton

### 1. Gate preconditions
The conditions that must all hold before any wireframe work begins: the IA is
`OWNER_APPROVED` (UX-003 acceptance criterion), the page and workflow spec
covers the pages to be wireframed, and Jacob has written the exact phrase
`AUTHORISE WIREFRAME ONLY`. Also restates the hard constraints of that gate:
static/mock-data only; no backend, database, broker connection, secrets,
publishing, or live actions. Preconditions are fixed by the repository rules;
confirmed in Round O.

### 2. Safety-visibility checklist (UX-001)
Per-page checks that the demo/live environment, data freshness, broker
connection, active risk, enabled/disabled status, and kill-switch state are
impossible to overlook — including in stale, breaker-tripped, and fail-closed
mock states. The pass/fail wording of each check is drafted in Round O; the
UX-001 acceptance criterion is that this checklist passes on the wireframes.

### 3. Journey traceability matrix
A table mapping every owner-approved user journey (from
[USER_ROLES_AND_JOURNEYS.md](../01-discovery/USER_ROLES_AND_JOURNEYS.md) and
the workflows in [PAGE_AND_WORKFLOW_SPEC.md](PAGE_AND_WORKFLOW_SPEC.md)
section 1) to the wireframe screens that realise it, step by step. A journey
with any unmapped step fails the review. The journey list is frozen at the
Round O sign-off that precedes wireframe authorisation.

### 4. Book detail completeness check (UX-002)
A dedicated check that the wireframed book detail view contains a placeholder
for every UX-002 element: assumptions, constituents, diversification, realised
and mark-to-market drawdown, heat, costs, regimes, crises, sensitivity,
statistical evidence, failures, approval history. Element definitions come
from Rounds E/F/H/I as mapped in the page spec; this check verifies presence,
not content.

### 5. Honesty and mock-data checks
Checks that mock data cannot be mistaken for real evidence: all figures are
clearly labelled as illustrative, no numeric thresholds or performance claims
are invented, uncertainty placeholders are present wherever performance
appears (BUS-004), and nothing in the wireframe implies tested or validated
status. These rules follow directly from the repository honesty rules and
apply regardless of round.

### 6. Review record and outcomes
The format of each review record (date, wireframe version, reviewer, checklist
results, journey matrix result) and the permitted outcomes: pass with evidence
attached, or fail with listed defects. A passing review makes the wireframe
eligible for Jacob's approval; it never implies `OWNER_APPROVED` status by
itself, and never authorises implementation (no-build gate). Format confirmed
in Round O.

## Known inputs (already decided)

- Wireframes require the exact phrase `AUTHORISE WIREFRAME ONLY`; static or
  mock-data only, with no backend, database, broker, secrets, publishing, or
  live actions — UX-003 and the repository no-build gate (CLAUDE.md).
- IA must be approved before any wireframe work starts — UX-003 acceptance
  criterion.
- UX-001 is accepted by this document's visual review checklist passing on
  the wireframes.
- UX-002 is accepted by traceability: every listed element present in the
  page spec and therefore checkable here.
- Approval of a wireframe never authorises implementation — no-build gate,
  `AUTHORISE AUTOFX V2 IMPLEMENTATION` is a separate explicit phrase.

## Open questions

- Exact pass/fail wording of each safety-visibility check → Round O.
- The frozen list of approved journeys the traceability matrix must cover →
  Round O sign-off of [USER_ROLES_AND_JOURNEYS.md](../01-discovery/USER_ROLES_AND_JOURNEYS.md).
- Which pages are in the first wireframe batch (all sixteen areas or a
  P1-critical subset) → Round O, at Jacob's direction.
- Wireframe medium and fidelity (paper-level sketch vs static mock-data
  prototype) → Round O, within the `AUTHORISE WIREFRAME ONLY` constraints.
- Whether the review is repeated per wireframe revision or only at batch
  completion → Round O.
