# Execution and Risk Rules

## Canonical risk definitions (direction approved 2026-08-17; numbers pending Round E)

- Drawdown cap is a **user input per book**; USD 100,000 / 1% risk per trade is
  the standard comparison configuration.
- **Realised peak-relative drawdown** is the canonical approval metric:
  `realised_peak_t = max(realised_equity_0 … realised_equity_t)`;
  `realised_drawdown_t = (realised_peak_t − realised_equity_t) / realised_peak_t`.
- Mark-to-market excursion and open-risk (**heat**) are separate, always-visible
  live safety controls — closed-only drawdown is never treated as sufficient
  for live safety.
- Position risk compounds from current portfolio size based on closed
  positions. Portfolio drawdown is measured from the prior portfolio peak.
- The book-level cap applies to the whole book; a constituent strategy may
  exceed it alone only if the book stays within cap — prominently flagged and
  separately risk-assessed.

## Live-safety invariants

- Every trade has a stop loss. If protection cannot be attached atomically,
  a fail-closed compensating sequence applies with a maximum unprotected
  interval, including immediate closure when protection cannot be confirmed.
- Approved books are **disabled by default**. Live activation is a separate,
  explicit, version-specific approval by Jacob.
- FX positions are never open while the FX market is closed (incl. weekends).
  Crypto session rules differ but maintenance, liquidity, and gap risks get
  explicit treatment.
- No entries or holds through approved high-volatility news exclusion windows.
- Broker truth is authoritative for live positions, orders, fills, balance,
  and margin; continuous reconciliation with defined discrepancy handling.
- Kill switches exist at global, environment, account, book, strategy, and
  symbol level and must be demonstrably reachable at runtime.
- Data-stale, news-unavailable, disconnect, latency, drawdown, heat, margin,
  reconciliation, abnormal-slippage, and repeated-rejection breakers all
  **fail closed**.
- One authoritative sizing engine (AutoFX or the cBot, decided in Round J);
  never two divergent formulas.
- Backtest, replay, paper, and live share one deterministic
  order/fill/accounting lifecycle as closely as practical; bid/ask execution,
  never mid-price fills.

## Fidelity

Backtest-to-live fidelity is a core pillar. Acceptable live-vs-backtest
degradation and minimum shadow/paper evidence are defined before any live
approval (Gates 6–7 in the acceptance-gate architecture). A live book never
self-modifies from research output without a separately tested and approved
version.
