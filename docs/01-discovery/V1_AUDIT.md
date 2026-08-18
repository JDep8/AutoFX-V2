# V1 Forensic Audit (read-only)

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — audit not started; repo access verified; DB provisioning pending; start gated on Jacob's explicit go, NEXT_ACTIONS § B)
- **Version:** 0.1.1
- **Last reviewed:** 2026-08-18
- **Dependencies:** V1_REUSE_REGISTER.md, `.claude/rules/security-and-secrets.md`, DECISION_LOG.md (D-022, D-023)
- **Approval evidence:** None yet

V1 is inspected for **lessons, not authority**. This document keeps three
things strictly separate: **what exists**, **what is proven**, and **what is
recommended**. Existing V1 tests are never treated as proof of correctness —
only what each test actually demonstrates is recorded.

## Access state (verified 2026-08-17)

| Asset | State |
|-------|-------|
| Repository `JDep8/AutoFX` | Private; read-only access verified via authenticated `gh` CLI (account JDep8). Python; branch `main`; updated 2026-07-30; 247 tree entries. No clone into V2 workspace; no code copying. |
| PostgreSQL database | Access **model approved 2026-08-18** (Q-001 → D-022): dedicated read-only role `autofx_v1_readonly`; autonomous SELECT-only inspection once configured; V1 permanently read-only. **Provisioning by Jacob still pending** — no connection exists yet. Schema/catalogue inspection first; bounded queries, statement timeouts, sampling; never write/lock. |
| cBot / execution bridge | **Located 2026-08-18** (Q-002 → D-023): V1 `code/TradingViewBridge.cs` (primary audit candidate) + related `code/PriceBridge.cs`. Audit must verify and document its per-symbol percentage weighting (not carried into V2, EXEC-011) and its sizing behaviour for the Round J engine decision. Not yet inspected. |
| Broker statements / logs / backtest reports | To be requested in Round B. |

## Security flags (recorded, contents never read)

- `101005649.rdp` committed at V1 repo root — remote-desktop connection file
  in version control. Never open or echo; recommend Jacob rotates any
  credentials it may embed and removes it from V1 history at his discretion.

## Observed structure (top level, 2026-08-17 — existence only, nothing verified)

Root-level Python modules (data feeds/health/prep/audit, dukascopy backfill &
import, slippage estimation, cost calc, cTrader OpenAPI, portfolio generator
watchdog, alerting) plus extensive Markdown reviews: ARCHITECTURE.md,
DATA_ACCURACY.md, DATA_AND_GENERATOR_REVIEW.md, PORTFOLIO_GENERATOR_REVIEW
(+_2).md, E2E_ANALYSIS.md, FORWARD_TEST.md, TEST_PLAN.md, TESTING_GUIDE.md,
LIVE_SETUP.md, HOSTING.md, ROADMAP.md, SPRINTS.md. These reviews are prime
audit inputs — V1 documented several of its own failure modes.

## Audit plan (what V1 can teach V2)

1. Canonical definitions (drawdown, sizing, equity) as actually implemented — feeds D-001/Round E; includes the located execution bridge (`code/TradingViewBridge.cs` + `PriceBridge.cs`, D-023) and its per-symbol weighting behaviour (EXEC-011)
2. Data sources and gaps; point-in-time correctness and leakage — feeds D-002/Q-010
3. Backtest/live execution divergence — feeds D-006/Round F
4. Strategy and experiment provenance; truncation behaviour — feeds D-003
5. Holdout contamination: which periods selection actually touched — feeds D-002/Q-010
6. Performance/scaling bottlenecks (multi-day generation) — feeds Round I/N
7. Failure recovery and resumability — feeds OPS-003
8. User journeys and UI pain points — feeds Round O
9. Security and operational risks (starting with the `.rdp` flag) — feeds Round N
10. What each existing test actually demonstrates — feeds TEST_AND_EVIDENCE_STRATEGY.md

## Findings

*None yet — audit not started.*
