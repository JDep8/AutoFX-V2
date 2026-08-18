# Trading Simulation and Certification Specification

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (the three-mode requirement itself is
  `OWNER_APPROVED` via D-034, 2026-08-18, evidence USER-STATED; every
  design detail in this skeleton is Claude-proposed and awaits its owning
  round; no content is implemented or tested)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** BACKTEST_FIDELITY_SPEC.md, CTRADER_INTEGRATION_SPEC.md,
  ORDER_AND_FILL_LIFECYCLE.md, OPEN_TRADE_MONITOR_SPEC.md,
  BROKER_RECONCILIATION.md, RISK_AND_DRAWDOWN_SPEC.md,
  TEST_AND_EVIDENCE_STRATEGY.md, DECISION_LOG.md (D-021, D-023, D-034),
  REQUIREMENTS_CATALOGUE.md (EXEC-012…014, VAL-008)
- **Approval evidence:** D-034 (owner-approved requirement intent,
  2026-08-18); design details: none yet

## Purpose

AutoFX V2 must be able to prove — before any live exposure — that the
exact production trading behaviour (signals, risk sizing, orders,
monitoring, exits, reconciliation) works correctly, first against
history, then against live conditions without orders, then end-to-end
against a designated cTrader **demo** account. This document specifies
the three owner-required modes and keeps the owner-approved intent
strictly separate from Claude-proposed design detail.

Nothing in this document implies profitability: a successful replay,
shadow run, or demo certification is evidence of **mechanical
correctness and fidelity**, never a guarantee of future results
(BUS-004). Demo fills, spread, liquidity, and slippage do **not** equal
live trading conditions, and no text here may be read otherwise.

## Owner-approved intent (D-034 — binding scope; USER-STATED)

### Mode A — accelerated historical execution replay (EXEC-012)

- Run an approved book quickly across a user-selected historical period
  (e.g. the previous year or another defined interval).
- Exercise the intended production signal, risk, order, trade-monitoring,
  exit, and reconciliation behaviour.
- Produce outbound order messages through the **same broker-neutral
  contract intended for cTrader**, routed to an internal simulated-broker
  adapter — never to cTrader.
- Recreate point-in-time market conditions from available historical
  price, spread, commission, slippage, swap/financing, market-hours,
  liquidity, and news-event data.
- Prevent look-ahead, future-data leakage, and any use of data not
  knowable at the simulated decision time (VAL-008; PIT rules).
- Deterministic, reproducible reruns (VAL-003 discipline).
- Painful-detail audit trail: every signal, rejected trade, accepted
  order, fill, price, cost, size, stop-loss, monitoring decision,
  modification, exit, and reconciliation result (FR-004 standard).
- Faster than real time; performance measured, but **fidelity is never
  weakened for speed** (BUS-003).
- Replay **supplements** backtesting; it is not evidence of guaranteed
  future profitability.

### Mode B — live shadow simulation (EXEC-013)

- Consume current price, market-hours, cost, and news inputs through the
  intended live-data interfaces.
- Evaluate the approved book and generate the order instructions that
  would have been sent.
- Route those instructions **only** to the internal simulator; never
  submit an external broker order.
- Compare expected execution behaviour with observable market conditions;
  retain evidence for backtest-to-live degradation monitoring
  (D-021/VAL-006/VAL-007, KPI-04).
- The architecture must make accidental routing from shadow mode to a
  live or demo account **fail closed**.

### Mode C — cTrader demo-account certification (EXEC-014)

- Before a book can become eligible for live approval, a **specifically
  designated cTrader demo account** conducts controlled end-to-end
  certification.
- For every symbol in the approved book, certification must be capable of
  sending a deliberately generated **minimum-risk test trade** (not
  necessarily a trade the strategy would naturally take).
- Each test verifies, at minimum: correct account and environment
  selection; symbol mapping; side/direction; order type; requested vs
  executed price within an approved tolerance; units, lot conversion,
  rounding, pip value, and account-currency conversion; account-specific
  percentage-risk sizing; mandatory stop-loss presence; stop-loss
  distance and placement; broker acceptance or documented rejection;
  current price retrieval; live trade-monitor registration; trade-state
  and modification handling; exit handling; broker-vs-platform
  reconciliation; complete audit evidence; and **proof that no order was
  routed to a live account**.
- Certification tests respect market closures and high-volatility-news
  safeguards, unless a later approved test design establishes a safe,
  isolated way to test those rejection paths without prohibited exposure.
- A successful demo test proves **integration wiring and calculations**;
  it does not prove that demo fills, spread, liquidity, or slippage equal
  live trading.
- Book approval must **not** itself trigger a demo order. Actual demo
  testing requires the later implementation authorisation, approved
  credentials/account configuration, and the applicable execution gate.

## Claude-proposed design concepts (`PROPOSED`; owned by later rounds)

- **One broker-neutral order contract, three routers.** The production
  order pipeline emits messages against a single broker-neutral contract;
  the only difference between backtest replay, shadow, demo
  certification, and (eventually) live is the adapter bound at the end:
  simulated-broker adapter (Modes A/B), demo cTrader adapter (Mode C),
  live cTrader adapter (Gate 7 only). Design owned by Rounds F/J with
  D-006 parity remediation.
- **Fail-closed routing design (Mode B/C):** environment identity is a
  typed, non-defaultable property; the simulator adapter is the default
  binding; demo/live adapters require explicit, logged, gate-checked
  activation; any ambiguity in environment resolution refuses to route
  (consistent with EXEC-002 and kill-switch design). Round J.
- **PIT data feed for Mode A** reuses the Round D point-in-time data
  contract; replay clock and event ordering rules come from
  BACKTEST_FIDELITY_SPEC (intrabar/ambiguity policies, Round F).
- **Mode C test-order generator:** minimum-risk parameterisation
  (smallest broker-valid size consistent with the account's risk
  configuration), per-symbol pass/fail record, and a certification
  register per book version. Round J.
- **Evidence storage:** replay/shadow/certification outputs are
  first-class evidence artefacts in the Gate 5/6/7 evidence packs
  (TEST_AND_EVIDENCE_STRATEGY).

## Measures (headline / supporting; numeric targets owned by later rounds)

Headline (roll up into KPI-21/KPI-22, PROJECT_CHARTER § KPI framework):

- **KPI-21 — Simulation fidelity and reproducibility** (guardrail):
  accelerated-replay reproducibility (identical rerun ⇒ identical
  results); replay fidelity vs the Round F truth model; processing
  performance (measured, never traded against fidelity).
- **KPI-22 — Certification coverage and execution correctness**
  (guardrail): order-message parity between simulation and intended
  cTrader routing; symbol-certification coverage per approved book;
  risk-sizing correctness; mandatory-SL correctness; entry-price
  tolerance adherence; monitoring and reconciliation correctness;
  **zero unintended external orders** (absolute); certification failure
  and remediation status.

Supporting diagnostics sit under these two headline measures per the
D-028 headline/supporting organisation. Numeric targets: Round F (replay
fidelity/reproducibility), Round J (certification tolerances, coverage,
remediation), Gates 5–7 application.

## Unresolved design matters (recorded, NOT decided here)

| Matter | Owning round |
|--------|--------------|
| Exact requested-vs-executed price tolerance | Round J (values), with Round F cost model |
| Minimum test-trade size rule per symbol/broker constraints | Round J |
| Certification expiry (how long a pass stays valid) and retest triggers (symbol/book/broker/config changes) | Round J |
| Failure remediation and re-certification procedure | Round J |
| Evidence-retention period for certification artefacts | Rounds K/N (with OPS-002 retention policy) |
| Safe isolated testing of closure/news rejection paths | Round J test design (owner-approved before use) |
| Replay performance measurement definition | Round F |
| Simulated-broker fill model (how simulator fills against PIT spread/liquidity) | Round F (truth model) |

## Traceability

- Requirements: EXEC-012 (Mode A), EXEC-013 (Mode B), EXEC-014 (Mode C),
  VAL-008 (simulation evidence integrity) — REQUIREMENTS_CATALOGUE.md.
- Decision: D-034. Priority: **P1** (part of the D-010 full-P1 platform:
  backtest→approval→execution→monitoring pipeline; no conflict with any
  existing owner-approved priority rule).
- Gates: Mode A/B evidence feeds Gates 5–6; Mode C certification is a
  precondition inside Gate 6→7 promotion; nothing here alters Gate 7's
  separate explicit live approval.
- Round ownership: Round F (replay truth/fidelity + simulator fill
  model), Round J (routing, certification, tolerances, fail-closed
  design), Round K (monitor/ledger integration), Round N (environments,
  retention), per DISCOVERY_STATUS.md assurance matrix.
