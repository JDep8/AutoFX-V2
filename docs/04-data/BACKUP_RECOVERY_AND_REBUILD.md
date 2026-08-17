# Backup, Recovery and Rebuild
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (OPS-002, OPS-003), [DATA_LINEAGE_AND_VERSIONING.md](./DATA_LINEAGE_AND_VERSIONING.md), [DATA_LICENSING_AND_RETENTION.md](./DATA_LICENSING_AND_RETENTION.md)
- **Approval evidence:** None yet

## Purpose

This document will define how the data platform survives loss: what is backed
up, how fast it must be recoverable, and how the whole platform could be
rebuilt after a disaster. A backup that has never been restored is a hope, not
a control — so restore tests are part of the objective, not an afterthought.
All recovery-point and recovery-time objectives are open questions until Jacob
approves them; no numbers are proposed here.

## Scope and decisions this document will own

- Backup scope: which datasets, registers, and configuration artefacts are
  covered, at what cadence.
- Recovery objectives (RPO/RTO) per artefact class — values to be
  owner-approved per OPS-002.
- The disaster-rebuild plan: reconstructing the platform from backups plus
  rebuildable derived data.
- Restore-test requirements and evidence.
- It does **not** own logical rebuildability of derived datasets (see
  [DATA_LINEAGE_AND_VERSIONING.md](./DATA_LINEAGE_AND_VERSIONING.md)) — this
  document covers the physical survival of what that contract needs.

## Structure skeleton

### Backup scope and tiers
Inventory of what must be backed up: raw immutable data, lineage and version
records, quarantine state, calendars, registers and governance documents,
configuration. Tiering (what is irreplaceable vs rebuildable vs re-downloadable
subject to licence) is a Round D question informed by
[DATA_LICENSING_AND_RETENTION.md](./DATA_LICENSING_AND_RETENTION.md).

### Recovery objectives (RPO/RTO)
Per tier: how much data loss is tolerable and how quickly service must return.
OPS-002's acceptance criterion is owner-approved RPO/RTO with a demonstrated
restore — the values are decided in Rounds D/N, never assumed.

### Backup mechanics and storage
Cadence, medium, location separation, encryption, and integrity verification of
backups (hash checks tie into
[DATA_LINEAGE_AND_VERSIONING.md](./DATA_LINEAGE_AND_VERSIONING.md)). Design in
Rounds D/N; security constraints per SEC-003 (Round N).

### Disaster-rebuild plan
The ordered procedure for rebuilding from nothing but backups: restore raw
data, verify hashes, replay transformations, verify derived datasets match
recorded fingerprints. Round D defines dependencies; Round N the operational
runbook.

### Restore-test regime
What a restore test covers, how often it runs, and what evidence it produces.
OPS-002 requires demonstration; OPS-003's resume-drill discipline applies.
Designed in Round N; any test result will carry honest status labels — nothing
is described as tested until it is.

### Failure scenarios register
Named scenarios the plan must cover: storage loss, corruption discovered late,
provider unavailability during rebuild (licence-dependent re-download),
partial-restore situations. Round D/N.

## Known inputs (already decided)

- Backup, recovery, and disaster-rebuild objectives with restore tests are a
  must-have requirement — OPS-002 (`PROPOSED`; RPO/RTO approved in Rounds D/N).
- Failure recovery and resumability for all long-running jobs — OPS-003.
- Originals are immutable (quarantine-before-repair, DATA-005) and derived data
  must be rebuildable (VAL-003 via
  [DATA_LINEAGE_AND_VERSIONING.md](./DATA_LINEAGE_AND_VERSIONING.md)) — both
  shape what backup must physically preserve.
- No credentials or secrets in backups' documentation or repo — SEC-001.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Backup scope inventory and tiering (irreplaceable vs rebuildable vs re-downloadable) | Round D |
| RPO/RTO values per tier | Rounds D/N (OPS-002 acceptance) |
| Backup cadence, medium, off-site strategy, encryption approach | Rounds D/N (with SEC-003) |
| Whether licences permit re-download as a recovery path per provider | Round D ([DATA_LICENSING_AND_RETENTION.md](./DATA_LICENSING_AND_RETENTION.md)) |
| Restore-test frequency, scope, and evidence format | Round N |
| Disaster-rebuild runbook ownership and drill schedule | Round N |
