# Canonical Data Model
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-009), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (DATA-002, DATA-003), [POINT_IN_TIME_DATA_POLICY.md](./POINT_IN_TIME_DATA_POLICY.md), [DATA_SOURCE_REGISTER.md](./DATA_SOURCE_REGISTER.md)
- **Approval evidence:** None yet

## Purpose

This document will define the canonical shape of every dataset the platform
stores: which raw granularity is kept, which fields every record carries, and
how symbol definitions and costs are represented through time. It is the single
place where "what the backtester is allowed to believe about the market" is
written down. Until Round D resolves granularity and field questions, this is a
skeleton of named decisions, not a schema.

## Scope and decisions this document will own

- Required raw granularity per asset class, and the documented truth lost at
  each coarser level (DATA-002).
- The canonical field sets for prices, costs, execution observations, and
  symbol specifications (DATA-003).
- How symbol and contract specifications change through time without corrupting
  history.
- It does **not** own event data keying (see
  [POINT_IN_TIME_DATA_POLICY.md](./POINT_IN_TIME_DATA_POLICY.md)) or quality
  rules (see [DATA_QUALITY_AND_QUARANTINE.md](./DATA_QUALITY_AND_QUARANTINE.md)).

## Structure skeleton

### Raw granularity per class
Ticks, quotes, market depth, one-minute bars, trade prints, or a layered
combination — this is an **open Round D question**, decided per class, with an
explicit account of what truth is lost at each level (e.g. intrabar sequence,
true spread at fill time). No granularity is assumed here.

### Truth lost at each granularity level
For each candidate level, the specific questions it cannot answer — most
critically whether a stop and a take-profit inside the same bar were hit in an
ambiguous order. Round D documents these losses per class before the
granularity decision is taken.

### Price record fields
Bid/ask (never mid-only, per VAL-002), timestamps, and per-class extensions.
Round D fixes the field list against what selected sources can actually supply.

### Cost and execution-observation fields
Spread history, commission schedules, swaps (including triple-swap days),
financing, rebates, conversion rates, observed slippage, rejected and partial
fills, latency observations. DATA-003 mandates capture; Round D defines each
field, its source (broker truth vs vendor), and its time-variation model.

### Slippage observation model
Slippage measured from actual broker fills, conditioned by symbol, side, time,
volatility, spread, size, order type, and event proximity — recorded here as a
required capability; the conditioning model itself is an open Round D/F
question.

### Symbol and contract specifications through time
Lot rules, tick size/value, margin, trading hours reference, and how
symbol-contract changes (re-denominations, spec changes, delistings) are
versioned so old history remains interpretable. Round D, with per-class
treatment for all eight classes (D-009).

### Per-class model variants
One subsection per CFD class — Forex, Indices, Metals, Crypto, Agriculture,
Equities, Cash, Commodities — noting class-specific fields (e.g. dividend
adjustments, crypto maintenance behaviour). Designed-for from day one per
D-009; populated FX-first.

## Known inputs (already decided)

- Eight-class universe designed-for from day one, FX-first rollout — D-009 /
  DATA-008 (`OWNER_APPROVED`).
- Greatest practical per-minute detail across the target period — DATA-002
  (`PROPOSED`; granularity per class approved in Round D).
- Price plus realistic trading costs captured (spread, commission, slippage,
  swaps/financing, other execution-relevant costs) — DATA-003.
- Bid/ask execution, never mid-price, with time-varying costs — VAL-002.
- ≥5 years history, target 10 — DATA-001.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Required raw granularity per class (ticks/quotes/depth/1-minute bars/trade prints/layered) and truth lost at each level | Round D |
| How ambiguous stop/TP sequences inside a bar are resolved, and what granularity makes them decidable | Round D (model), Round F (backtest rule) |
| Slippage conditioning model (symbol/side/time/volatility/spread/size/order type/event proximity) from actual broker fills | Rounds D/F |
| Swaps, triple swaps, rebates, financing, and conversion-rate representation through time | Round D |
| Symbol-contract change versioning rules | Round D |
| Broker-truth vs vendor field sourcing per cost field, and live calibration | Round D (with [DATA_SOURCE_REGISTER.md](./DATA_SOURCE_REGISTER.md)) |
| Per-class symbol lists that the model must cover first | Rounds C/D (D-009 open remainder) |
