# Information Architecture

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [PRODUCT_REQUIREMENTS.md](PRODUCT_REQUIREMENTS.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [USER_ROLES_AND_JOURNEYS.md](../01-discovery/USER_ROLES_AND_JOURNEYS.md), [GLOSSARY.md](../00-governance/GLOSSARY.md)
- **Approval evidence:** None yet

## Purpose

This document defines the page inventory and navigation structure of AutoFX V2
before any screen is drawn. It exists because UX-003 requires the inventory and
end-to-end flows to be approved before wireframe work starts, and because the
safety information mandated by UX-001 must have a guaranteed home on every
page. It is the authority on what pages exist and how they connect — not on
what each page contains (see
[PAGE_AND_WORKFLOW_SPEC.md](PAGE_AND_WORKFLOW_SPEC.md)).

## Scope and decisions this document will own

- The canonical page inventory: which page areas exist, their names (aligned to
  the [Glossary](../00-governance/GLOSSARY.md)), and their grouping.
- The navigation model: how pages are reached, grouped, and cross-linked.
- The placement and persistence rules for the global safety surface (UX-001).
- Demo/live environment separation as an architectural rule.
- It does **not** own per-page content, workflows, or wireframe acceptance.

## Structure skeleton

### 1. Page inventory
The mandated minimum set of page areas to evaluate, each with a one-line
mission statement and governing requirement IDs: Dashboard, Data Health,
Strategy/Experiment Lab, Portfolio Generator, Generation Runs, Candidate
Books, Approved Books, Accounts, Live Execution, Open Trades, Trade Ledger,
Research Centre, Content Studio, Administration, Audit, Incidents. Whether
areas are added, merged, or split is decided in Round O. Research Centre and
Content Studio are architecture placeholders only until P1 is
`LIVE_VALIDATED` (D-010).

### 2. Navigation model
Primary navigation grouping (e.g. research vs live-operations vs
administration clusters), depth rules, and how the single-user context (D-008)
simplifies the model — no role-switching or tenant navigation. Resolved in
Round O.

### 3. Global safety surface (UX-001)
The always-visible elements — demo/live environment, data freshness, broker
connection, active risk, enabled/disabled status, kill-switch state — where
they persist across every page, and the rule that no page may hide them.
Presentation detail belongs to the page spec; the architectural guarantee is
owned here. Resolved in Round O; verified by
[WIREFRAME_REVIEW.md](WIREFRAME_REVIEW.md).

### 4. Entity model and cross-linking
The navigable entities (experiment, strategy, generation run, candidate book,
approved book version, account, trade, ledger event, incident, audit record)
and the cross-links between them — e.g. a trade links back to its book
version, strategy, and generation run (FR-004 provenance). Entity definitions
depend on Rounds G–K; the link map is decided in Round O.

### 5. Environment separation (demo/live)
How demo and live contexts are architecturally separated in navigation so the
active environment is unmistakable (UX-001) and live-marking remains a
separate deliberate act (EXEC-002). Resolved in Round O with input from
Round J.

### 6. Page states
The architectural requirement that every page defines empty, loading, error,
stale-data, and fail-closed states — stale and fail-closed states are
safety-relevant (DATA-005, DATA-006, breaker behaviour). State inventory per
page belongs to the page spec; the rule that states must exist is owned here.
Resolved in Round O.

### 7. Naming conventions
Canonical page and entity naming aligned to the Glossary so documents,
wireframes, and later implementation use identical terms. Finalised alongside
Glossary sign-off (Round E for accounting terms; Round O for page names).

## Known inputs (already decided)

- Minimum page areas to evaluate are mandated by the owner brief (list in
  section 1) — UX-003.
- Page inventory and flows precede screens; wireframes gated by
  `AUTHORISE WIREFRAME ONLY` — UX-003.
- Single user, no multi-tenancy or client-facing surfaces — BUS-005 / D-008.
- P2 (Research Centre) and P3 (Content Studio) are planning-only areas until
  P1 is live-validated — BUS-006 / D-010.
- Approved books are disabled by default; activation is separate and
  version-specific — EXEC-002, FR-001.
- Kill switches exist at global/environment/account/book/strategy/symbol
  scope and must be reachable — EXEC-010.

## Open questions

- Final page inventory: additions, merges, splits of the mandated minimum →
  Round O.
- Navigation grouping and depth rules → Round O.
- Exact composition of the global safety surface and its behaviour when data
  is stale or a breaker has tripped → Round O (informed by Rounds D and J).
- How the demo/live separation is expressed navigationally (switch, parallel
  trees, or other) → Round O with Round J input.
- Entity cross-link map once entity definitions land → Rounds G–K, then
  Round O.
- Whether Administration, Audit, and Incidents are distinct pages or one
  administrative cluster → Round O.
