# Glossary

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (definitions seeded; canonical sign-off in Round E)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** DECISION_LOG.md (D-001), RISK_AND_DRAWDOWN_SPEC.md
- **Approval evidence:** None yet

Plain language first; exact technical definition second. Terms marked (E) get
their final canonical formula in Round E.

| Term | Plain meaning | Technical definition |
|------|---------------|----------------------|
| Book | A portfolio of strategies traded together | Versioned set of strategy configurations spanning multiple symbols/timeframes with shared risk limits |
| Closed balance (E) | Cash after all closed trades | Account balance reflecting only settled, closed positions |
| Realised equity (E) | Account value counting only finished trades | Closed balance; excludes floating P&L of open positions |
| Mark-to-market equity (E) | What the account is worth right now | Realised equity + floating P&L of open positions at current bid/ask |
| Realised peak (E) | The best the realised curve has ever been | `realised_peak_t = max(realised_equity_0 … realised_equity_t)` |
| Realised drawdown (E) | How far below the best point we are, counting closed trades only | `(realised_peak_t − realised_equity_t) / realised_peak_t` |
| Mark-to-market excursion | The worst the account *looked* while trades were open | Peak-relative decline of mark-to-market equity; live monitoring/breaker input, not the approval metric |
| Heat / open risk (E) | Total loss if every open trade hit its stop right now | Sum of open-position stop-distances × sizes, currency-converted |
| Drawdown cap | The maximum drawdown a book is allowed | User input per book (D-001); applies to the whole book |
| Holdout | Data kept untouched to test honestly at the end | Locked, selection-untouched period tested once, after pre-registration of book + thresholds |
| Leakage | The future contaminating the past | Any path by which information unavailable at decision time influences a decision or its evaluation |
| Point-in-time | Data as it was actually knowable then | Values keyed by actual release timestamp and revision vintage |
| No-suitable-book | An honest "nothing qualifies" result | First-class outcome of generation; never forced into producing a book |
| Truncation | Cutting candidates early by a rule | Explicit, owner-approved elimination policy (D-003); never hidden in implementation |
| Kill switch | The big red stop | Runtime control that halts entries/exits new risk at global/environment/account/book/strategy/symbol scope; must be demonstrably reachable |
| Breaker | Automatic trip on a bad signal | Fail-closed automatic control (data-stale, news-missing, disconnect, drawdown, heat, margin, reconciliation, slippage, rejection) |
| Fail closed | When unsure, don't trade | On missing/ambiguous safety-relevant input: no new entries; controlled-exit policy applies |
| Gate 1–8 | The quality checkpoints | Acceptance-gate architecture: data eligible → experiment valid → strategy eligible → book eligible → approved-but-disabled → shadow/paper → live → continue/reduce/pause/retire |
| Standard comparison configuration | The common yardstick | USD 100,000 starting capital, 1% risk per trade (D-001) |
| Approved Books | Books Jacob signed off — still off by default | Register of `OWNER_APPROVED`, version-specific books; disabled until separate live approval |
