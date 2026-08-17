# Circuit Breakers and Kill Switches

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md), [BROKER_RECONCILIATION.md](BROKER_RECONCILIATION.md), [INCIDENT_AND_RECOVERY_RUNBOOK.md](INCIDENT_AND_RECOVERY_RUNBOOK.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-006, D-007), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (EXEC-010)
- **Approval evidence:** None yet

## Purpose

This document will define the controls that stop trading: manual kill switches
at every scope, and automatic breakers that trip on bad signals. V1 had no
demonstrably reachable runtime breaker or kill switch (D-006); V2 requires
every switch to be provably reachable at runtime before any live approval
(EXEC-010), and every breaker to fail closed. It also defines who may restart
trading after a stop and what evidence a restart requires.

## Scope and decisions this document will own

- The kill-switch scope hierarchy and its semantics.
- The breaker catalogue: trigger conditions, trip actions, fail-closed rules.
- Which metrics may stop trading automatically.
- Restart authority and required evidence.
- Reachability demonstration requirements (Gate 6).

Out of scope: the metric definitions themselves (owned by
[RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md)); incident procedures
after a stop (owned by
[INCIDENT_AND_RECOVERY_RUNBOOK.md](INCIDENT_AND_RECOVERY_RUNBOOK.md)).

## Structure skeleton

### 1. Kill-switch scope hierarchy
Manual switches at global, environment, account, book, strategy, and symbol
scope (EXEC-010): what each scope halts, how scopes nest, and precedence when
several are active. Semantics defined in Round J.

### 2. Trip semantics
For each switch and breaker: whether it blocks new entries only, also amends,
or also triggers controlled exits of open positions; and how the fail-closed
and controlled-exit policies (Glossary) apply. Defined in Rounds E/J.

### 3. Breaker catalogue
One subsection per automatic breaker, each fail-closed: data-stale,
news-unavailable, broker disconnect, latency, drawdown, heat, margin,
reconciliation failure, abnormal slippage, repeated rejection. Each subsection
will hold the trigger definition, measurement source, trip action, and reset
rule. Trigger thresholds are Round E/J owner decisions — no numbers are
proposed here.

### 4. Automatic-stop metric list
The definitive list of which metrics can stop trading automatically versus
which only alert. This is an explicit Round E/J owner decision recorded here.

### 5. Restart authority and evidence
Who can restart trading after a manual or automatic stop (Jacob only, per the
emergency-ownership model in
[RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md) section 9, unless Round
E decides otherwise), what evidence must be recorded before restart (cause
identified, reconciliation clean, breaker condition cleared), and how the
restart itself is audited. Defined in Rounds E/J/N.

### 6. Runtime reachability demonstration
How "demonstrably reachable at runtime" is proven: the drill that exercises
every switch and breaker in paper trading before any live approval (EXEC-010
acceptance criterion → Gate 6). Drill design in Round J; execution only after
implementation authorisation.

### 7. Breaker observability
How switch and breaker states are surfaced so they are impossible to overlook
(UX-001), and how every trip and reset lands in the audit trail and trade
ledger. Rounds J/O.

## Known inputs

- EXEC-010: kill switches at global/environment/account/book/strategy/symbol
  scope and fail-closed breakers must be demonstrably reachable at runtime;
  reachability demonstrated in paper before any live approval.
- D-001 direction: MTM excursion and heat are separate, always-visible live
  safety controls — inputs to breakers, not approval metrics.
- D-006 (open): the absent V1 breaker/kill switch is a documented gap.
- D-007 (open): missing news data fails closed — the news-unavailable breaker
  is a hard rule per `.claude/rules/data-integrity.md`.
- Glossary: breaker and fail-closed definitions; kill-switch scope list.
- UX-001: kill-switch state must be impossible to overlook.

## Open questions

- Trigger definitions and thresholds for every breaker → Rounds E/J (drawdown,
  heat, margin thresholds depend on Q-005 and Round E definitions).
- Which metrics stop trading automatically versus alert only → Round E/J owner
  decision.
- Trip action per breaker (entries-only vs controlled exit) → Rounds E/J.
- Restart authority, required evidence, and cool-down rules → Rounds E/J/N.
- Latency and slippage measurement definitions feeding their breakers → Round
  F ([BACKTEST_FIDELITY_SPEC.md](../05-research-and-validation/BACKTEST_FIDELITY_SPEC.md))
  and Round J.
