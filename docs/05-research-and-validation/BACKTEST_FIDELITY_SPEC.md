# Backtest Fidelity Specification
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (VAL-001..VAL-005), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-009), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-006, D-007), [LEAKAGE_AND_HOLDOUT_POLICY.md](./LEAKAGE_AND_HOLDOUT_POLICY.md)
- **Approval evidence:** None yet

## Purpose

This document specifies how backtests are made honest enough to be trusted as
indicators of live behaviour — the product's first commercial goal (BUS-001).
It defines one deterministic order, fill, and accounting lifecycle shared by
backtest, replay, paper, and live, and the tests that prove they agree. Where
one-minute bars cannot reveal what truly happened inside a minute, the spec
chooses the conservative interpretation explicitly rather than silently.

## Scope and decisions this document will own

- The single shared execution lifecycle (order → fill → accounting) used by
  every environment, so backtest and live cannot diverge by construction
  (addresses D-006 gaps).
- The cost and friction truth model: bid/ask fills (never mid-price),
  time-varying spread, commissions, swaps, slippage, latency, liquidity,
  partial fills, rejections, lot rules, margin, currency conversions, broker
  rules (VAL-002).
- Ambiguity policies: intrabar ordering, gaps, simultaneous levels, stale
  quotes, no-tick bars, disconnects.
- Determinism, reproducibility, and the verification test suite.
- Out of scope: acceptance thresholds for strategies/books (Gates 3/4 docs)
  and statistical inference
  ([STATISTICAL_VALIDATION_PLAN.md](./STATISTICAL_VALIDATION_PLAN.md)).

## Structure skeleton

### 1. Shared deterministic lifecycle
One order/fill/accounting engine used by backtest, replay, paper, and live;
divergence is a defect, not a calibration. Engine boundaries and the parity
test with the live path are settled in Round F (with Round J execution
inputs and D-006 remediation evidence).

### 2. Execution truth model (VAL-002)
Bid/ask execution only — never mid-price. Time-varying spread, commissions,
swaps/financing, slippage, latency, liquidity constraints, partial fills,
rejections, lot rules, margin, and currency conversions, each modelled from
the Round D data contract. Per-class parameters come from measured data
(Gate 1), never invented; Round F approves the model.

### 3. Ambiguity and conservative-policy rules
SL/TP behaviour across gaps; the explicit conservative policy when one-minute
bars cannot reveal the intraminute path (which of stop or target is assumed
hit first); simultaneous-level resolution; weekend gaps; stale quotes; no-tick
bars; disconnects mid-position; rejected stop modifications. Each ambiguity
gets a named, owner-approved rule in Round F; ambiguity without a rule fails
closed.

### 4. Market, news, and calendar replay (VAL-005, D-007)
Deterministic session calendars, news-window exclusion, and forced flattening
(EXEC-006/007) replayed identically in backtest and live logic, with
fail-closed behaviour on missing news data. Rules are decided in Rounds C/F
under D-007.

### 5. Determinism and reproducibility (VAL-003)
Deterministic seeds, immutable inputs, code/data/config hashes, event logs,
and exact reruns of any historical result. Mechanisms confirmed in Round F;
records live in [EXPERIMENT_REGISTRY_SPEC.md](./EXPERIMENT_REGISTRY_SPEC.md).

### 6. Verification suite
Golden scenarios (hand-computed expected outcomes), property-based tests,
metamorphic tests, cross-engine comparison, record/replay of live sessions,
and broker-statement reconciliation (EXEC-009). Suite contents defined in
Round F; nothing here is described as `TESTED` until it actually is.

### 7. Live-vs-backtest degradation tolerance (Q-009)
The measurable definition of "accurate enough": what degradation between
backtest and shadow/paper/live is acceptable before a book fails Gate 6.
Jacob defines the tolerance — Round A continuation refined in Round F. No
number is proposed here.

## Known inputs

- BUS-001 / VAL-001: fidelity is a core pillar with measurable tolerances.
- VAL-002: bid/ask fills, full friction stack — `PROPOSED`, Round F.
- VAL-003: exact reproducibility from recorded versions — `PROPOSED`, Round F.
- VAL-005 / D-007: deterministic news/calendar exclusion, replay-tested,
  fail-closed on missing news.
- D-006: V1 gaps (sizing divergence, polling-vs-bar timing, no reconciliation)
  must be remediated by design, not inherited.
- DATA-002/DATA-003: per-minute detail and captured real costs feed the truth
  model; granularity limits are documented, not hidden.
- EXEC-008: one authoritative sizing engine shared backtest↔live.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Acceptable live-vs-backtest degradation definition and tolerance | Q-009, Round F |
| Conservative intrabar-ordering policy wording | Round F |
| Per-class cost/session/gap model parameters | Rounds C/D → Round F |
| Golden-scenario list and cross-engine comparison design | Round F |
| Parity mechanism between backtest engine and live path (D-006) | Rounds F/J |
| Fail-closed behaviours for stale quotes, no-tick bars, disconnects | Round F |
