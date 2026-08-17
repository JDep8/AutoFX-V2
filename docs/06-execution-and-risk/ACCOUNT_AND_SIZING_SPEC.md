# Account and Sizing Specification

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md), [CTRADER_INTEGRATION_SPEC.md](CTRADER_INTEGRATION_SPEC.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-006), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-002), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md)
- **Approval evidence:** None yet

## Purpose

This document will define how each trading account is configured and how every
position's size is calculated — by exactly one engine, with one formula, shared
by backtest and live. V1 suffered backtest/live sizing divergence (D-006); V2
prevents a repeat by designating a single authoritative sizing engine and
proving parity. Account structure, per-account risk, and the USD-first currency
stance are specified here.

## Scope and decisions this document will own

- The single authoritative sizing engine decision: AutoFX or Jacob's existing
  cTrader cBot (EXEC-008, Q-002 → Round J).
- The canonical sizing formula, including compounding behaviour (RISK-003).
- Per-account risk percentages and account-level configuration (RISK-007).
- Account-currency handling: USD first, documented multi-currency path
  (RISK-008).

Out of scope: canonical accounting definitions (owned by
[RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md)); connection and
account-discovery mechanics (owned by
[CTRADER_INTEGRATION_SPEC.md](CTRADER_INTEGRATION_SPEC.md)).

## Structure skeleton

### 1. Account model
What an "account" is in AutoFX V2: demo/live designation, base currency,
linked books, per-account risk percentage, enable/disable state. Populated in
Round J from the account-management requirement (FR-005).

### 2. Per-account risk configuration
Each account carries its own position-risk percentage (RISK-007); every live
configuration (account x book x overlay) is separately revalidated before
activation. Validation workflow detail decided in Round J.

### 3. Single authoritative sizing engine
The EXEC-008 decision: whether AutoFX computes sizes and sends fully sized
orders, or Jacob's cBot sizes locally from AutoFX signals. Round J reviews the
cBot code (blocked on Q-002) and decides. This section will also record how
the design prevents double-sizing and divergent formulas — one implementation,
one owner, parity-tested backtest-to-live.

### 4. Canonical sizing formula
The formula itself, including the RISK-003 rule that position risk compounds
from current portfolio size based on closed positions (not floating P&L).
Exact formula terms depend on Round E accounting definitions; the formula is
approved in Rounds E/J together.

### 5. Currency handling
USD accounts first; the multi-currency path is documented and preserved, never
blocked (RISK-008). Conversion rules defer to
[RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md) section 2.

### 6. Broker constraints on size
Lot steps, minimum/maximum volumes, margin requirements, and how the sizing
engine rounds and validates against them. Facts gathered in Round J from
cTrader/broker documentation; rounding direction is a safety decision (never
round risk upward) to be confirmed by Jacob in Round J.

### 7. Sizing parity evidence plan
How backtest and live sizing are proven identical: shared implementation or
golden-scenario parity tests (EXEC-008 acceptance criterion). Test design in
Round J; execution only after implementation authorisation.

## Known inputs

- RISK-003: position risk compounds from current portfolio size based on
  closed positions.
- RISK-007: each account has its own position-risk percentage.
- RISK-008: USD accounts initially; multi-currency path documented and
  preserved.
- EXEC-008: one authoritative sizing engine; no double-sizing or divergent
  formulas; parity test backtest-to-live.
- D-006 (open): V1 backtest/live sizing divergence is a documented gap V2 must
  remediate by design.
- D-001: user inputs include risk per trade; USD 100k/1% standard comparison
  configuration.

## Open questions

- Q-002: location/access for Jacob's cTrader cBot code — blocks the Round J
  sizing-engine review.
- Which engine is authoritative (AutoFX vs cBot) → Round J decision by Jacob.
- Exact canonical sizing formula and its interaction with Round E accounting
  definitions → Rounds E/J.
- Rounding and lot-constraint policy → Round J.
- Per-account overlay revalidation workflow → Round J.
