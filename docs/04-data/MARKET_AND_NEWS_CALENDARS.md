# Market and News Calendars
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-007, D-009), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (VAL-005, EXEC-006, EXEC-007), [POINT_IN_TIME_DATA_POLICY.md](./POINT_IN_TIME_DATA_POLICY.md)
- **Approval evidence:** None yet

## Purpose

This document will define the platform's model of time and market availability:
when each market is open, when trading is forbidden around news, and when
positions must be flat. These rules must be deterministic — the same inputs
always produce the same allowed/forbidden answer — and replay-testable, because
a calendar that behaves differently in backtest and live silently breaks
fidelity. When news data is missing, the rules fail closed: no data means no
trading, never "assume it is safe".

## Scope and decisions this document will own

- The canonical time model: UTC canon, broker/server time mapping, DST
  handling.
- Per-class session calendars for all eight CFD classes (D-009): holidays,
  early closes, maintenance windows.
- The weekend flattening deadline and forced-flattening behaviour (EXEC-006).
- Deterministic news-exclusion windows, including fail-closed behaviour on
  missing news data (D-007) and their replay tests (VAL-005).
- It does **not** own event storage (see
  [POINT_IN_TIME_DATA_POLICY.md](./POINT_IN_TIME_DATA_POLICY.md)) or live
  enforcement wiring (execution documents, Rounds F/J).

## Structure skeleton

### Canonical time model
UTC as the canonical timeline; how broker/server time is mapped onto it,
including brokers whose server clock shifts with DST. The mapping rules and
their verification are Round C/D questions.

### DST handling
How daylight-saving transitions are represented so no bar is duplicated, lost,
or mislabelled, in history and live. Named as a mandatory data-reality case;
resolved in Rounds C/D with replay evidence later (VAL-005).

### Per-class session models
One model per class — Forex, Indices, Metals, Crypto, Agriculture, Equities,
Cash, Commodities (D-009) — covering sessions, holidays, early closes, and
maintenance windows. Crypto's continuous-but-interrupted sessions
(maintenance, liquidity, gaps) are explicitly modelled per EXEC-006. Rounds
C/D, FX first.

### Holiday and early-close calendars
Source, format, and update cadence for holiday data per market, and what
happens when holiday data is missing or contradicted by observed quotes (a
fail-closed candidate). Round D.

### Weekend flattening deadline
The rule that FX positions are never open while the FX market is closed
(EXEC-006), expressed as a deterministic deadline before the weekend close. The
deadline value and per-class analogues are open Round C/D/F questions — no
time value is proposed here.

### Deterministic news-exclusion windows
Window construction from point-in-time events (which severities, which
currencies/regions map to which symbols, window shape around scheduled vs
actual time). Windows FAIL CLOSED when news data is missing (D-007). Window
parameters are Round C/F decisions; determinism is non-negotiable.

### Replay-test specification
The tests demonstrating that calendar and exclusion rules produce identical
decisions in backtest and replay, including fail-closed cases (news feed
absent, holiday data missing). Specified in Rounds C/F per VAL-005; execution
of tests is future work and will carry honest status labels.

## Known inputs (already decided)

- Deterministic news/calendar enforcement must be replay-tested; news
  intelligence never substitutes for deterministic exclusion — D-007
  (`PROPOSED`, direction), VAL-005.
- Missing news data fails closed — D-007 and `.claude/rules/data-integrity.md`.
- FX positions never open while the market is closed, including weekends;
  crypto sessions treated explicitly — EXEC-006.
- No trades opened or held through approved high-volatility news windows —
  EXEC-007.
- Eight-class universe with per-class session models designed-for from day
  one — D-009 / DATA-008 (`OWNER_APPROVED`).

## Open questions

| Question | Resolved by |
|----------|-------------|
| Broker/server time mapping and DST verification method | Rounds C/D |
| Per-class session calendars, holidays, early closes, maintenance windows (all eight classes) | Rounds C/D (D-009 open remainder) |
| Weekend flattening deadline value and per-class analogues | Rounds C/D/F |
| News-exclusion window parameters (severity set, symbol mapping, window shape, scheduled-vs-actual anchoring) | Rounds C/F (D-007) |
| Holiday-data source and missing-data behaviour | Round D |
| Replay-test scope and pass criteria | Rounds C/F (VAL-005) |
