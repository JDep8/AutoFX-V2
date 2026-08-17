# Data Source Register
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-007, D-009), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (DATA-001..DATA-008), [DATA_LICENSING_AND_RETENTION.md](./DATA_LICENSING_AND_RETENTION.md), [CANONICAL_DATA_MODEL.md](./CANONICAL_DATA_MODEL.md)
- **Approval evidence:** None yet

## Purpose

This register will list every candidate and selected source of market, cost, and
news/macro data for AutoFX V2, one entry per provider per data type. It exists
so that no source is ever assumed adequate: each entry must be evaluated against
the complete data contract before it can supply anything. It also records
fallbacks, so a single provider outage or licensing change never silently stops
the platform.

## Scope and decisions this document will own

- Which providers supply which data types (prices, costs, macro/news events,
  symbol specifications) for each of the eight CFD classes (D-009).
- The evaluation verdict per provider against the data contract, including the
  FMP evaluation mandated by DATA-007.
- The designated fallback per data type and the switch-over criteria.
- It does **not** own licensing terms (see
  [DATA_LICENSING_AND_RETENTION.md](./DATA_LICENSING_AND_RETENTION.md)) or field
  definitions (see [CANONICAL_DATA_MODEL.md](./CANONICAL_DATA_MODEL.md)).

## Structure skeleton

### Register schema
The columns every entry must carry: provider, data type, asset classes covered,
history depth, granularity, delivery mechanism, rate/volume limits, licensing
reference, redistribution position, retention terms, cost, evaluation status,
fallback, decision reference. Column set finalised in Round D.

### Broker-sourced versus vendor-normalised history
For each class: whether history comes from the executing broker's own feed or a
normalised vendor feed, what differs between them, and how live calibration
against broker truth will occur. This is an open Round D question; the
resolution feeds the backtest-fidelity work under VAL-001/VAL-002.

### Per-class source entries (eight CFD classes)
One subsection per class — Forex, Indices, Metals, Crypto, Agriculture,
Equities, Cash, Commodities (D-009) — each listing candidate sources, coverage
gaps, and Gate 1 eligibility status. FX is populated first per the approved
phasing; other classes remain skeleton entries until their Round D pass.

### Macro/news event sources
Candidate sources for point-in-time economic events, evaluated against the
point-in-time contract in
[POINT_IN_TIME_DATA_POLICY.md](./POINT_IN_TIME_DATA_POLICY.md). Round D decides;
fail-closed behaviour on feed absence is governed by D-007.

### FMP evaluation record
A dated evaluation of FMP against the complete data contract with explicit gaps
and fallbacks, per DATA-007. FMP is a candidate to evaluate, never an assumed
choice. Resolved in Round D.

### Fallback and outage posture per data type
For each data type: the fallback source (if any), what happens when both fail,
and which breakers trip (news-feed outage fails closed per D-007). Round D.

## Known inputs (already decided)

- Eight CFD classes designed-for from day one; FX-first phased rollout; each
  class gated on its data contract passing Gate 1 — D-009 / DATA-008
  (`OWNER_APPROVED`).
- FMP must be evaluated against the full contract, never assumed — DATA-007.
- Minimum history: ≥5 years, target 10 — DATA-001 (acceptance depth → Gate 1).
- Missing news data fails closed — D-007 direction and
  `.claude/rules/data-integrity.md`.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Which providers are candidates per class, and what coverage/history/limits do they actually offer? | Round D |
| Broker-specific vs vendor-normalised history per class, and the live-calibration method | Round D |
| Provider cost, licensing, redistribution, and retention terms per candidate | Round D → [DATA_LICENSING_AND_RETENTION.md](./DATA_LICENSING_AND_RETENTION.md) |
| FMP verdict against the complete contract (gaps, fallbacks) | Round D (DATA-007) |
| Fallback designation and switch-over criteria per data type | Round D |
| Per-class symbol lists and brokers (affects which sources are even relevant) | Rounds C/D (D-009 open remainder) |
