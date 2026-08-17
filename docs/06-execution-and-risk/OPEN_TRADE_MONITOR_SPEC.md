# Open Trade Monitor Specification

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [ORDER_AND_FILL_LIFECYCLE.md](ORDER_AND_FILL_LIFECYCLE.md), [RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md), [MARKET_AND_NEWS_CALENDARS.md](../04-data/MARKET_AND_NEWS_CALENDARS.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (EXEC-003, EXEC-005), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-007)
- **Approval evidence:** None yet

## Purpose

This document will define what happens to a trade after it is filled. Every
open trade — including one with a take-profit attached — stays actively
monitored and may need an earlier, controlled exit (EXEC-005). The monitor
consumes live market and news inputs throughout the trade's life (EXEC-003)
and produces deterministic, replayable exit reasons. Round K owns the content
of this document.

## Scope and decisions this document will own

- The set of monitored signals and conditions per open trade.
- Invalidation, risk-change, time-exit, news/session, and trailing rules.
- The deterministic exit-reason hierarchy when several conditions co-occur.
- Manual intervention on open trades and how it is evidenced.
- What the monitor records into the trade ledger (FR-004 observations).

Out of scope: how exits are physically executed (owned by
[ORDER_AND_FILL_LIFECYCLE.md](ORDER_AND_FILL_LIFECYCLE.md)); account-wide
automatic stops (owned by
[CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md)).

## Structure skeleton

### 1. Monitored signals
Which inputs the monitor watches per open trade: price/quote stream, strategy
signal state, news/calendar state, session state, risk metrics. Defined in
Round K; live-input requirement per EXEC-003.

### 2. Invalidation rules
Conditions under which the original trade thesis is considered invalid and the
trade is exited even though neither SL nor TP has been hit. Defined per
strategy family in Round K.

### 3. Risk-change responses
How the monitor reacts when account- or book-level risk changes while a trade
is open (heat rising, drawdown approaching cap, margin tightening). Thresholds
defer to [RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md) (Round E);
responses defined in Round K.

### 4. Time-based exits
Maximum holding periods and time-of-day/weekend rules — including the EXEC-006
rule that FX positions are never open while the FX market is closed.
Defined in Round K against the market calendars (D-007).

### 5. News and session approach
Behaviour approaching approved high-volatility news windows and session
boundaries: no trades opened or held through approved exclusion windows
(EXEC-007); deterministic calendar enforcement with fail-closed behaviour when
news data is unavailable (D-007). Windows themselves are owned by
[MARKET_AND_NEWS_CALENDARS.md](../04-data/MARKET_AND_NEWS_CALENDARS.md).

### 6. Trailing logic
Whether and how stops trail; interaction with broker-side SL amendments.
Defined in Round K; amendment mechanics per
[ORDER_AND_FILL_LIFECYCLE.md](ORDER_AND_FILL_LIFECYCLE.md).

### 7. Manual intervention
How Jacob can intervene on an open trade, what permissions apply, and how the
intervention is recorded so post-trade attribution stays honest. Defined in
Round K; emergency ownership per
[RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md) section 9.

### 8. Deterministic exit-reason hierarchy
When several exit conditions co-occur in the same evaluation, exactly one
reason wins, by a fixed published precedence — so replays of the same inputs
always produce the same recorded reason (EXEC-005 acceptance criterion). The
hierarchy itself is a Round K owner decision.

### 9. Monitor observations in the trade ledger
What the monitor writes to the event-sourced ledger (FR-004): each evaluation,
condition states, decisions taken and not taken, and the winning exit reason.
Schema detail in Round K alongside
[ORDER_AND_FILL_LIFECYCLE.md](ORDER_AND_FILL_LIFECYCLE.md) section 10.

## Known inputs

- EXEC-003: live market and news inputs are used before entry and throughout
  monitoring.
- EXEC-005: every open trade (including with TP) is actively monitored;
  controlled earlier exits are possible; exit reasons must be deterministic in
  replay.
- EXEC-006: FX positions never open while the FX market is closed; crypto
  sessions treated explicitly.
- EXEC-007: no trades opened or held through approved high-volatility news
  exclusion windows.
- D-007 (open): deterministic news/calendar enforcement must be replay-tested;
  news intelligence never substitutes for deterministic exclusion rules;
  missing news data fails closed.
- FR-004: monitor observations are part of the trade ledger.

## Open questions

- Full monitored-signal set per strategy family → Round K.
- Invalidation rule definitions → Round K.
- Risk-change response actions (reduce vs exit vs freeze) → Round K.
- Time-exit rules per class → Round K.
- Trailing policy (and whether it exists in P1) → Round K.
- Exit-reason precedence order → Round K owner decision.
- Monitor evaluation cadence and its parity with backtest assumptions → Rounds
  F/K (relates to D-006 polling-versus-bar gap).
