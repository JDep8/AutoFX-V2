# Scope and Priorities

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (priority structure OWNER_APPROVED via D-010; non-goals OWNER_APPROVED via D-020; remaining details pending rounds)
- **Version:** 0.2.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** PROJECT_CHARTER.md, DECISION_LOG.md (D-008/D-009/D-010/D-020)
- **Approval evidence:** Round A 2026-08-17 (batch 1) and 2026-08-18 (batch 2, verbatim in INTERVIEW_RECORD.md)

## Priority 1 — Core AutoFX platform (implementation MVP)

- Historical and continuously updated data platform
- Strategy research and experiment management
- Realistic backtesting and independent validation
- Multi-strategy, multi-symbol, multi-timeframe portfolio/book generation
- Candidate-book approval workflow
- Approved-books register, disabled by default
- Trading-account management
- cTrader integration and execution engine
- Open-trade monitoring and controlled exits
- Detailed trade ledger and post-trade evidence
- Production risk controls, reconciliation, observability, incident response,
  kill switches

## Priority 2 — Deep Research Centre (planning-only until P1 live-validated)

Multi-model research orchestration; research of strategies, execution, data
quality, backtest fidelity, live trades, improvements; user-submitted ideas
and strategy videos; evidence/citations/provenance/review/approval/
prioritisation; durable knowledge catalogue.

## Priority 3 — Content and AI-media business (planning-only until P1 live-validated)

Research-led content (YouTube long/shorts, TikTok, Facebook, Instagram);
repeatable AI characters and brand assets; licensed media providers; human
approval, financial-promotion controls, synthetic-media disclosure,
provenance, publishing, analytics; business plan for a trading-platform brand.

## Architectural rule

P2 and P3 are architected and documented during discovery so V1-style
shortcuts do not block them later — but they must not delay the
safety-critical P1 foundation without an approved reason.

## Asset universe (D-009)

Eight CFD classes — Forex, Indices, Metals, Crypto, Agriculture, Equities,
Cash, Commodities — designed-for from day one; phased rollout FX-first; each
class gated on its data contract passing Gate 1.

## Non-goals (D-020, `OWNER_APPROVED` 2026-08-18 — BUS-010)

1. No high-frequency, ultra-low-latency, or latency-arbitrage trading.
2. No routing of manually initiated discretionary trades — AutoFX executes
   approved, versioned books only.
3. No guarantee of profitability or fixed returns.
4. No live trading by default.
5. No autonomous AI decision to enable live trading.
6. No strategy approval based solely on an attractive historical backtest.
7. No weakening of validation, data-quality, or risk gates to meet a
   deadline.
8. No direct reuse of V1 code without evidence-based review.
9. No external customer funds, paid signals, or copy trading in the initial
   scope.
10. No content output that overstates or influences trading-research
    conclusions.
11. No production deployment merely because code or a Git branch is
    complete.
12. No silent acceptance of missing, contaminated, or insufficient evidence.

Standing exclusions from earlier decisions: no customers/subscribers/
copy-trading (D-008); no implementation of any kind before the exact
authorisation phrase (no-build gate).
