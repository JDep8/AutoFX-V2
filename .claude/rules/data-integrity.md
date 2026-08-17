# Data Integrity Rules

## Contract-first

No data source is assumed adequate (including FMP). Every source is evaluated
against the approved data contract in `docs/04-data/DATA_SOURCE_REGISTER.md`
covering coverage, granularity, history depth, licensing/redistribution,
retention, cost, limits, and fallbacks.

## Point-in-time correctness

- Data is stored as it was knowable at the time. Macro/fundamental events carry
  scheduled time, actual release time, consensus, previous value, revision
  vintage, surprise, currency/region, severity, and source provenance.
- Events are keyed by actual release timestamp and revision vintage, never only
  by economic period.
- Any lookahead path (revised values, corrected bars, back-filled fields
  visible to research as-of an earlier date) is a defect, not a convenience.

## Quality gates

- Automated checks for missing, duplicate, malformed, stale, inconsistent,
  out-of-order, and suspicious data.
- Quarantine before repair; imputed or repaired data remains visibly labelled.
- Late arrivals, corrections, deduplication, and reconciliation follow the
  approved policy in `docs/04-data/DATA_QUALITY_AND_QUARANTINE.md`.

## Lineage and reproducibility

- Dataset versions are immutable; every result must be reproducible from
  immutable code, data, configuration, provider, and random-seed versions.
- Lineage, versioning, and hashing per
  `docs/04-data/DATA_LINEAGE_AND_VERSIONING.md`.

## Calendars and sessions

- UTC canon with explicit broker/server-time and DST treatment.
- Session calendars, holidays, early closes, maintenance windows, and the
  weekend flattening deadline are deterministic, versioned data — not code
  constants.
- News/high-volatility exclusion windows are deterministic and replay-tested.
  News *intelligence* never substitutes for deterministic exclusion rules.
- Missing news or calendar data **fails closed** (no entry, controlled exit
  policy applies).

## Asset-class breadth (Round A decision, 2026-08-17)

The target universe spans eight CFD classes (Forex, Indices, Metals, Crypto,
Agriculture, Equities, Cash, Commodities). Each class has its own session
model, cost model (e.g. dividends on equity/index CFDs, rolls on commodities,
24/7-with-maintenance for crypto), and gap-risk rules. A class enters
implementation only when its data contract passes Gate 1. Rollout is phased,
FX first.
