# Broker Reconciliation

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [CTRADER_INTEGRATION_SPEC.md](CTRADER_INTEGRATION_SPEC.md), [ORDER_AND_FILL_LIFECYCLE.md](ORDER_AND_FILL_LIFECYCLE.md), [CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-006), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (EXEC-009)
- **Approval evidence:** None yet

## Purpose

This document will define how AutoFX V2 continuously proves that its internal
picture of live trading matches the broker's. The broker is authoritative for
live positions, orders, fills, balance, and margin (EXEC-009): when the two
disagree, AutoFX adopts broker truth, alerts, and fails closed. V1 had no
broker-truth reconciliation at all (D-006); V2 treats it as a first-class,
always-on control.

## Scope and decisions this document will own

- What is reconciled, how often, and against which broker messages.
- Discrepancy classification, alerting, and fail-closed handling.
- Detection of manual broker-side changes and orphaned positions.
- The resync procedure after outages and its evidence requirements.

Out of scope: transport and recovery mechanics (owned by
[CTRADER_INTEGRATION_SPEC.md](CTRADER_INTEGRATION_SPEC.md)); the breaker that a
reconciliation failure trips (owned by
[CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md)).

## Structure skeleton

### 1. Broker-truth principle
The governing rule: broker state is authoritative for live positions, orders,
fills, balance, and margin; AutoFX's internal state is a hypothesis to be
verified. This section states the principle and its limits (e.g. AutoFX
remains authoritative for its own decisions and intents). Confirmed in Round J.

### 2. Reconciliation scope and sources
Exactly which broker fields are reconciled against which internal records, per
entity (position, order, fill, balance, margin), using which cTrader messages.
Message mapping in Round J.

### 3. Cadence and triggers
Continuous reconciliation cadence, plus event-driven reconciliation (after
every fill, amendment, reconnect, and restart). Cadence values are a Round J
decision — none are assumed here.

### 4. Discrepancy classification
Taxonomy of mismatches (missing fill, unknown position, quantity/price
mismatch, balance drift, margin mismatch) with severity levels and the
response each triggers. Defined in Round J; every discrepancy alerts and fails
closed pending resolution (EXEC-009 acceptance criterion).

### 5. Manual broker-side changes
Detection of changes made outside AutoFX (manual close, manual SL move,
broker adjustment, dividend/swap postings) and how they are absorbed into
internal state and recorded in the trade ledger. Defined in Round J/K.

### 6. Orphaned positions
Detection and handling of broker positions with no matching AutoFX intent —
including whether they are adopted, closed, or quarantined pending manual
decision. The handling policy is a Round J owner decision.

### 7. Resync after outage
The ordered procedure for re-establishing truth after a disconnect or restart:
reconcile first, resume trading only when clean, per the recovery invariants
shared with [CTRADER_INTEGRATION_SPEC.md](CTRADER_INTEGRATION_SPEC.md)
section 6. Defined in Round J.

### 8. Reconciliation evidence in the ledger
What each reconciliation run records (snapshot, diffs, resolutions) so the
trade ledger (FR-004) and post-incident reviews can reproduce exactly what was
known when. Schema in Rounds J/K.

## Known inputs

- EXEC-009: broker truth authoritative for live positions/orders/fills/
  balance/margin; continuous reconciliation with discrepancy handling;
  discrepancies alert and fail closed.
- D-006 (open): absent broker-truth reconciliation is a documented V1 gap the
  V2 architecture must remediate.
- FR-004: reconciliation events form part of each trade's evidence record.
- Fail-closed rule (Glossary): on ambiguous safety-relevant state, no new
  entries; controlled-exit policy applies.

## Open questions

- Reconciliation cadence and event triggers → Round J.
- Full discrepancy taxonomy and per-class response → Round J.
- Orphaned-position policy (adopt/close/quarantine) → Round J owner decision.
- How long trading stays halted after an unresolved discrepancy, and who may
  clear it → Rounds J/E (links to emergency ownership in
  [RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md)).
- Evidence required to demonstrate reconciliation works before Gate 6 → Round
  J with [BACKTEST_FIDELITY_SPEC.md](../05-research-and-validation/BACKTEST_FIDELITY_SPEC.md).
