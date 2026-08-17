# Project Charter — AutoFX V2.0

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (KPIs, non-goals, constraints pending Round A completion)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** DECISION_LOG.md, SCOPE_AND_PRIORITIES.md
- **Approval evidence:** Round A partial answers 2026-08-17 (see INTERVIEW_RECORD.md)

## Mission

1. Produce backtests whose results are trustworthy indicators of what could
   reasonably be expected under real trading conditions.
2. Find and operate profitable portfolios within explicitly approved risk
   limits.

Profit is an optimisation objective. Data integrity, absence of leakage,
honest out-of-sample evidence, drawdown compliance, execution fidelity, and
live-trading safety are hard constraints. Profitability is never guaranteed.

## Why V2 exists

V1 began implementation before the end-to-end product and evidence model were
sufficiently defined. V2 is a discovery-first engagement under an absolute
no-build gate (root `CLAUDE.md`).

## Owner and users

Jacob Depares is product owner and — per D-008 (`OWNER_APPROVED` 2026-08-17) —
the sole user: personal trading with own capital. No customers, subscribers,
or copy-trading clients.

## Priorities

- **P1 (implementation MVP, per D-010):** data platform, strategy research,
  realistic backtesting, book generation, approval workflow, approved-books
  register (disabled by default), account management, cTrader execution,
  open-trade monitoring, trade ledger, production risk controls.
- **P2 (planning-only until P1 live-validated):** Deep Research Centre.
- **P3 (planning-only until P1 live-validated):** Content and AI-media
  business.

## Asset universe

Eight CFD classes (D-009), phased rollout FX-first, each class gated on its
data contract.

## Open charter items (Round A continuation)

- Target jurisdictions / legal entity (Q-006)
- Budget, horizon, availability, team, infrastructure (Q-007)
- Measurable KPIs and explicit non-goals (Q-008)
- Measurable definition of backtest "accuracy" (Q-009)
