# Scope and Priorities

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (priority structure OWNER_APPROVED via D-010; details pending rounds)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** PROJECT_CHARTER.md, DECISION_LOG.md (D-008/D-009/D-010)
- **Approval evidence:** Round A 2026-08-17

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

## Non-goals

Pending Q-008 (Round A batch 2). Known so far: no customers/subscribers/
copy-trading (D-008); no implementation of any kind before the authorisation
phrase.
