# Delivery Roadmap
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-009, D-010), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (BUS-005, BUS-006, DATA-008), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-007), [WORK_BREAKDOWN_AND_DEPENDENCIES.md](./WORK_BREAKDOWN_AND_DEPENDENCIES.md), [IMPLEMENTATION_READINESS_REVIEW.md](./IMPLEMENTATION_READINESS_REVIEW.md)
- **Approval evidence:** None yet

## Purpose

This document is the single staged roadmap for AutoFX V2: what discovery work
is done, what implementation work is approved to be planned, what is deferred,
and what has been rejected or superseded — without erasing any of that history.
It sequences the Priority 1 MVP and the FX-first asset rollout, and it records
delivery estimates only as ranges once the facts needed to estimate exist.
Nothing on this roadmap authorises building; the no-build gate in `CLAUDE.md`
holds until Jacob issues the explicit implementation authorisation.

## Scope and decisions this document will own

- The roadmap ledger: the four permanent categories every work item lives in
  (completed discovery, approved implementation backlog, deferred/future
  backlog, rejected/superseded) and the rule that items move between
  categories but are never deleted.
- Stage boundaries and ordering for the P1 implementation MVP (D-010).
- The per-class rollout sequence within D-009's FX-first phasing.
- The estimate-range discipline (no point estimates, no invented numbers).
- Out of scope: task-level breakdown and dependencies
  ([WORK_BREAKDOWN_AND_DEPENDENCIES.md](./WORK_BREAKDOWN_AND_DEPENDENCIES.md))
  and the exit-review checklist
  ([IMPLEMENTATION_READINESS_REVIEW.md](./IMPLEMENTATION_READINESS_REVIEW.md)).

## Structure skeleton

### 1. Roadmap ledger (four categories, history preserved)
Every roadmap item is recorded as: completed discovery work, approved
implementation backlog, deferred/future backlog, or rejected/superseded work.
Rejections and supersessions are marked with their status label and the
decision that caused them (mirroring
[DECISION_LOG.md](../00-governance/DECISION_LOG.md) practice) — never removed.
The ledger format is fixed here; items populate continuously as Rounds B–O
close.

### 2. Discovery completion track (Rounds A–O)
The remaining interview rounds and their target artefacts, ending in the
Discovery Exit Review. Round A is partially complete (D-001 direction, D-008,
D-009, D-010 approved); Rounds B–O each unblock sections across the document
set. Sequencing between rounds is settled in Round N.

### 3. Priority 1 implementation MVP staging (D-010)
The full P1 platform — data → research → backtest → books → approval →
cTrader execution → monitoring → ledger → risk controls — staged into
implementation increments. Stage boundaries, and which stages may proceed in
parallel, are decided in Round N and only enter the approved backlog after
the Exit Review and Jacob's explicit `AUTHORISE AUTOFX V2 IMPLEMENTATION`
statement.

### 4. Phased asset rollout (D-009)
FX first; the remaining seven CFD classes (Indices, Metals, Crypto,
Agriculture, Equities, Cash, Commodities) enter implementation only when
their data contract passes Gate 1 (data eligible). Architecture, data model,
and calendars are designed for all eight from day one. Per-class ordering
beyond FX-first, symbol lists, and brokers come from Rounds C/D.

### 5. Priority 2 and 3 planning-only tracks
Research Centre (P2) and Content business (P3) remain
planning-and-architecture only until P1 is `LIVE_VALIDATED` (D-010,
BUS-006). This section holds their planning milestones (Rounds L and M) and
the explicit trigger condition for reconsidering their implementation.

### 6. Estimates and delivery horizon (ranges only)
All effort and duration estimates are expressed as ranges with stated
assumptions. **No estimates exist yet**: Q-007 (budget, horizon, weekly
availability, team capability, infrastructure constraints) blocks any
realistic estimation and remains open. This section stays empty of numbers
until Q-007 is answered in the Round A continuation and refined in Round N.

### 7. Gate alignment and review cadence
How roadmap stages align to Gates 1–8, and how Gate 8 outcomes
(continue/reduce/pause/retire) feed back into the ledger — a retired book or
class returns work to the deferred or rejected category rather than
disappearing. Cadence for roadmap review is agreed in Round N.

## Known inputs

- D-010 / BUS-006: implementation MVP is the full Priority 1 platform; P2/P3
  planning-only until P1 live-validated — `OWNER_APPROVED`.
- D-009 / DATA-008: eight-class universe designed-for from day one; phased
  rollout FX-first, each class gated on Gate 1 — `OWNER_APPROVED`
  (universe and phasing).
- D-008 / BUS-005: sole user is Jacob; no customer-driven deadlines exist —
  `OWNER_APPROVED`.
- BUS-003/BUS-004: evidence and safety standards are never weakened for
  schedule; profitability is never guaranteed, so the roadmap promises
  delivery of capability and evidence, never returns.
- Change history discipline: superseded work is marked, not deleted
  (Decision Log preamble).

## Open questions

| Question | Resolved by |
|----------|-------------|
| Budget, delivery horizon, weekly availability, team capability, infrastructure constraints | Q-007, Round A continuation → Round N |
| Ordering and parallelism of Rounds B–O | Round N |
| P1 stage boundaries and increment definitions | Round N (post-Exit-Review authorisation required to execute) |
| Per-class rollout order after FX; symbol lists and brokers per class | Rounds C/D (D-009 open remainder) |
| Trigger and criteria for starting P2/P3 implementation | D-010 condition (P1 `LIVE_VALIDATED`) + Rounds L/M planning |
| Roadmap review cadence and Gate 8 feedback procedure | Round N |
