# Service and Event Catalogue

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [LOGICAL_ARCHITECTURE.md](LOGICAL_ARCHITECTURE.md), [INTEGRATION_CONTRACTS.md](INTEGRATION_CONTRACTS.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md)
- **Approval evidence:** None yet

## Purpose

This catalogue will be the single reference for what each service does, what
it owns, and every event that crosses a service boundary. It exists so that
the trade ledger and audit trail can be designed against a complete, named
event vocabulary rather than discovering events during implementation. It
stays a skeleton until the module boundaries are settled in Round N.

## Scope and decisions this document will own

- One catalogue entry per service: responsibility, owned data, consumed and
  emitted events, failure posture (fail-closed obligations).
- The canonical event vocabulary: event names, ownership, ordering and
  idempotency expectations, retention.
- Which events are audit-mandatory (must reach the ledger) versus
  operational-only.
- It does **not** own external interface contracts — those live in
  [INTEGRATION_CONTRACTS.md](INTEGRATION_CONTRACTS.md).

## Structure skeleton

### 1. Service catalogue

One entry per service, using a fixed template (responsibility / owned data /
events in / events out / failure posture). Entries to be drafted after
Round N boundary decisions, informed by the noted domain rounds:

- **Data service** — ingestion, quality checks, quarantine-before-repair,
  freshness monitoring (DATA-005, DATA-006). Detail: Round D.
- **Research service** — experiment registry and multiple-testing
  accounting (QUANT-001), rationale capture (QUANT-002). Detail: Round G.
- **Backtest service** — bid/ask truth model, deterministic reruns
  (VAL-002, VAL-003). Detail: Round F.
- **Portfolio service** — multi-day book generation with checkpoints and
  the first-class no-suitable-book outcome (FR-002, FR-003, D-005).
  Detail: Round I.
- **Approval service** — candidate-book workflow into the Approved Books
  register, disabled by default (FR-001, EXEC-002). Detail: Rounds I/J.
- **Account service** — multi demo/live account management, per-account
  risk overlay (FR-005, RISK-007). Detail: Round J.
- **Execution service** — order lifecycle via cTrader, stop-loss
  protection, reconciliation against broker truth (EXEC-001, EXEC-004,
  EXEC-009). Detail: Round J.
- **Monitoring service** — open-trade monitoring, deterministic exit-reason
  hierarchy, breakers and kill switches (EXEC-005, EXEC-010). Detail:
  Rounds J/K.
- **Ledger service** — event-sourced trade record with full provenance
  (FR-004). Detail: Round K.
- **Research-centre service (P2, planning-only)** — provenance-tracked
  multi-model research; no write-path to live configuration (RES-002,
  RES-003, D-010). Detail: Round L.
- **Content service (P3, planning-only)** — research-led content with human
  approval before publish (CONTENT-001, D-010). Detail: Round M.

### 2. Event catalogue

Will hold the named event table (event / producer / consumers / payload
sketch / ordering / audit-mandatory?). Event families expected to emerge —
names not yet fixed: data-quality/quarantine events (Round D), experiment
lifecycle events (Round G), generation checkpoint events (Round I),
approval/activation events (Rounds I/J), order/fill/reconciliation events
(Round J), breaker/kill-switch events (Rounds J/K), ledger append events
(Round K). No event names are canonical until owner-approved.

### 3. Delivery semantics

Will define ordering, idempotency, replay, and retention rules per event
family, consistent with deterministic reproducibility (VAL-003) and
replay-tested enforcement (VAL-005). Technology-independent rules first;
technology mapping follows the Round N queue decision.

### 4. Audit-mandatory events

Will list which events must reach the ledger for a trade decision to be
reproducible in "painful detail" (FR-004), and the fail-closed behaviour
when an audit-mandatory event cannot be recorded. Rounds K/N.

## Known inputs

- The P1 service chain and its ordering — D-010 (`OWNER_APPROVED`).
- Ledger must document every trade with entry/exit reasons, monitor
  observations, all order/fill events, and reproducible provenance — FR-004.
- Broker truth is authoritative; reconciliation discrepancies alert and fail
  closed — EXEC-009.
- Kill switches operate at global/environment/account/book/strategy/symbol
  scope and must be demonstrably reachable — EXEC-010.
- Safety-relevant ambiguity fails closed (Glossary: "Fail closed"; D-007
  direction for missing news data).

## Open questions

- Final service boundaries (which merge, which split)? → Round N.
- Event transport and delivery guarantees (at-least-once vs exactly-once
  handling, ordering keys)? → Round N.
- Which events are audit-mandatory, and what happens when the ledger is
  unreachable? → Rounds K/N.
- Deterministic exit-reason hierarchy contents? → Round K (EXEC-005).
- How do generation checkpoint events support kill/resume with identical
  results? → Round I (FR-002).
- Do the P2/P3 services define events now (names reserved) or at their own
  phase start? → Rounds L/M (D-010).
