# Order and Fill Lifecycle

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [CTRADER_INTEGRATION_SPEC.md](CTRADER_INTEGRATION_SPEC.md), [ACCOUNT_AND_SIZING_SPEC.md](ACCOUNT_AND_SIZING_SPEC.md), [OPEN_TRADE_MONITOR_SPEC.md](OPEN_TRADE_MONITOR_SPEC.md), [BROKER_RECONCILIATION.md](BROKER_RECONCILIATION.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (EXEC-004, FR-004)
- **Approval evidence:** None yet

## Purpose

This document will define the full life of an order: from a sized, gated
decision, through submission, acknowledgement, fills (including partial),
amendments, rejections, and retries, to a closed position with realised costs.
Its central safety rule is EXEC-004: every trade has a stop loss, and a
position that cannot be confirmed protected is closed. It also owns the
trade-ledger evidence model (FR-004) that records every step.

## Scope and decisions this document will own

- Order types, time-in-force, and amendment rules AutoFX V2 will use.
- Stop-loss attachment mechanics and the fail-closed protection sequence
  (EXEC-004).
- Partial-fill, rejection, retry, and duplicate-prevention policy.
- The event-sourced trade-ledger evidence model (FR-004).

Out of scope: transport, authentication, and message-level idempotency
mechanics (owned by [CTRADER_INTEGRATION_SPEC.md](CTRADER_INTEGRATION_SPEC.md));
in-flight monitoring after entry (owned by
[OPEN_TRADE_MONITOR_SPEC.md](OPEN_TRADE_MONITOR_SPEC.md)).

## Structure skeleton

### 1. Order types and time-in-force
Which cTrader order types and time-in-force options are used, and which are
deliberately excluded. Facts researched and decided in Round J.

### 2. Stop-loss attachment (EXEC-004)
Every trade has a stop loss. Round J researches whether the selected cTrader
flow attaches protection atomically with entry. If it does not, this section
defines the fail-closed compensating sequence: the maximum permitted
unprotected interval, and immediate closure whenever protection cannot be
confirmed within it. The interval value is a Round J owner decision — never a
default invented here.

### 3. Take-profit handling
How TP is attached, amended, and interacts with the monitor's authority to
exit earlier (EXEC-005). Mechanics in Round J; monitor precedence in Round K.

### 4. Amendments
Which amendments are permitted (SL/TP moves, size changes), their preconditions
and confirmation requirements. Decided in Round J.

### 5. Partial fills
Position and protection state after a partial fill; whether remainders rest,
amend, or cancel; how sizing and heat account for partials. Decided in Round J,
consistent with backtest fidelity assumptions
([BACKTEST_FIDELITY_SPEC.md](../05-research-and-validation/BACKTEST_FIDELITY_SPEC.md)).

### 6. Rejections and retries
Classification of rejection reasons, what is retryable, retry limits, and the
repeated-rejection breaker hand-off to
[CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md).
Policy decided in Round J.

### 7. Duplicate prevention
Client order IDs, idempotent submission, and recovery-time duplicate checks so
a reconnect or restart can never double-submit. Mechanics live in the cTrader
spec; the lifecycle-level invariants are stated here (Round J).

### 8. Broker-side protection
Which protections (SL/TP) are held broker-side versus engine-side, and why —
so protection survives AutoFX outages. Researched and decided in Round J.

### 9. Order/position state machine
The named states and legal transitions from decision to closed, giving the
ledger and reconciliation an unambiguous vocabulary. Drafted in Round J.

### 10. Trade-ledger evidence model (FR-004)
The event-sourced record per trade: strategy/model version, features, data
version, signal, expected price/cost/risk, decision gates passed, order
messages, acknowledgements, fills, broker state, SL/TP, monitor observations,
amendments, exit, realised costs/P&L, and reconciliation snapshots. Two views:
a human-readable explanation and machine-reproducible evidence. Post-trade
attribution decomposes outcomes (signal quality, timing, spread, slippage,
latency, sizing, monitoring, regime, execution error). Retention, privacy,
access control, immutability, correction workflow, and export are all Round K
decisions.

## Known inputs

- EXEC-004: every trade has a stop loss; non-atomic protection requires a
  fail-closed compensating sequence with a maximum unprotected interval,
  including immediate closure.
- FR-004: the trade ledger documents every trade in painful detail; any trade
  decision must be reproducible.
- EXEC-005: the monitor may exit any open trade earlier than its TP.
- EXEC-009: broker truth is authoritative — lifecycle state defers to
  reconciliation on conflict.
- VAL-002: partial fills, rejections, and latency are part of the backtest
  truth model, so live lifecycle semantics must match it.

## Open questions

- Does the selected cTrader flow attach SL atomically with entry? → Round J
  research.
- Maximum unprotected interval (if non-atomic) → Round J owner decision.
- Permitted order types, time-in-force, and amendment set → Round J.
- Partial-fill remainder policy → Round J.
- Retry classification and limits → Round J.
- Ledger retention, privacy, access control, immutability, correction
  workflow, and export formats → Round K.
