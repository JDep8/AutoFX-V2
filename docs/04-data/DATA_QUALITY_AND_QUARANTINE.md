# Data Quality and Quarantine
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (DATA-005, DATA-006), [CANONICAL_DATA_MODEL.md](./CANONICAL_DATA_MODEL.md), [DATA_LINEAGE_AND_VERSIONING.md](./DATA_LINEAGE_AND_VERSIONING.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-007)
- **Approval evidence:** None yet

## Purpose

This document will define how bad data is detected, isolated, and honestly
handled. The governing principle is quarantine-before-repair: suspect data is
never silently fixed in place — it is set aside, the original preserved, and
any repair recorded as a new version with provenance. It also owns the
freshness rules that decide when live inputs are too stale to trade on.

## Scope and decisions this document will own

- The automated check catalogue: missing, duplicate, malformed, stale,
  inconsistent, out-of-order, and suspicious data (DATA-005).
- The quarantine workflow and the rule that repair never overwrites originals.
- Handling of late arrivals, provider corrections, deduplication, and
  reconciliation between sources.
- Freshness SLAs, monitoring, and alerting for all production inputs
  (DATA-006) — SLA numbers themselves are open, not invented here.
- It does **not** own breaker wiring into execution (execution docs) or backup
  (see [BACKUP_RECOVERY_AND_REBUILD.md](./BACKUP_RECOVERY_AND_REBUILD.md)).

## Structure skeleton

### Automated check catalogue
One named check per defect class from DATA-005, each with its detection rule
and severity. Threshold values (e.g. what gap length counts as "missing", what
quote age counts as "stale") are open Round D questions — no numbers appear
until owner-approved.

### Quarantine-before-repair workflow
The lifecycle: detect → quarantine → diagnose → repair as a new version →
release or reject. Originals are immutable; consumers never read quarantined
data. Round D approves the workflow; versioning mechanics live in
[DATA_LINEAGE_AND_VERSIONING.md](./DATA_LINEAGE_AND_VERSIONING.md).

### Late arrivals and provider corrections
How late-arriving records and provider-issued corrections (corrected bars,
revised events) are ingested without rewriting what earlier runs saw. Round D;
point-in-time consequences per
[POINT_IN_TIME_DATA_POLICY.md](./POINT_IN_TIME_DATA_POLICY.md).

### Deduplication and cross-source reconciliation
Duplicate-event detection keys and the reconciliation procedure when two
sources disagree about the same market moment, including which source is
designated truth per field. Round D.

### Known defect scenarios register
The mandatory data-reality cases recorded as named scenarios each check must
cover: missing ticks, stale quotes, duplicate events, corrected bars, DST
transitions, holidays, weekend gaps, broker outages, news-feed outages. All are
open Round D items; news-feed outage handling fails closed per D-007.

### Freshness SLAs, monitoring, and alerting
Per input (prices, news, spreads, commissions, slippage observations): the
staleness definition, the SLA, the monitor, and the alert route. DATA-006
mandates existence; the values and tooling are Round D questions, with
operational wiring in Round N.

## Known inputs (already decided)

- Automated checks for the full defect list with quarantine-before-repair —
  DATA-005 (`PROPOSED`; thresholds and policy approved in Round D).
- Continuous update and monitoring of all production inputs with freshness
  SLAs — DATA-006.
- Safety-critical ambiguity fails closed and becomes a blocking Question
  Register entry — CLAUDE.md evidence-honesty rule.
- Missing news data fails closed — D-007 direction.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Quality thresholds per check (gap, staleness, outlier, inconsistency definitions) | Round D |
| Quarantine workflow approval, including who releases repaired data | Round D |
| Late-arrival and correction ingestion rules per source | Round D |
| Dedup keys and cross-source reconciliation truth designation | Round D |
| Freshness SLA values per input and alerting channels | Round D (values), Round N (operations) |
| Broker-outage and news-feed-outage detection and downstream behaviour | Round D detection; Rounds C/F enforcement (D-007) |
