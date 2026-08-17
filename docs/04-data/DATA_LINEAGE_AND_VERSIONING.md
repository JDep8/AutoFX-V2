# Data Lineage and Versioning
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (VAL-003, DATA-005), [DATA_QUALITY_AND_QUARANTINE.md](./DATA_QUALITY_AND_QUARANTINE.md), [POINT_IN_TIME_DATA_POLICY.md](./POINT_IN_TIME_DATA_POLICY.md), [BACKUP_RECOVERY_AND_REBUILD.md](./BACKUP_RECOVERY_AND_REBUILD.md)
- **Approval evidence:** None yet

## Purpose

This document will define how every dataset's origin, transformations, and
versions are recorded so that any result can be traced back to exactly the
bytes that produced it. Reproducibility (VAL-003) is impossible without it: a
backtest that cannot name its data version is not evidence. It also owns
rebuildability — the guarantee that derived datasets can be reconstructed from
raw inputs deterministically.

## Scope and decisions this document will own

- The lineage record: source, ingestion time, transformation chain, and
  responsible process for every dataset.
- The versioning scheme for raw and derived data, including how repairs and
  corrections create new versions rather than mutations.
- Hashing: how dataset versions are fingerprinted so runs can prove which data
  they used.
- Rebuildability requirements: which artefacts must be reconstructible from
  which retained inputs.
- It does **not** own physical backup and restore (see
  [BACKUP_RECOVERY_AND_REBUILD.md](./BACKUP_RECOVERY_AND_REBUILD.md)).

## Structure skeleton

### Lineage record schema
The fields every dataset version carries: source reference (per
[DATA_SOURCE_REGISTER.md](./DATA_SOURCE_REGISTER.md)), ingestion timestamp,
transformation identity and code version, parent versions. Schema fixed in
Round D.

### Versioning scheme
How versions are named and ordered for raw feeds, repaired data (from the
quarantine workflow), and derived datasets; immutability of published versions.
Round D. Interacts with revision vintages in
[POINT_IN_TIME_DATA_POLICY.md](./POINT_IN_TIME_DATA_POLICY.md).

### Hashing and fingerprinting
What is hashed (files, partitions, logical datasets), which algorithm family,
and where hashes are recorded so a backtest run can cite them. VAL-003 requires
code/data/config hashes; the mechanism is a Round D/F design question.

### Rebuildability contract
Which derived artefacts must be exactly reconstructible from retained raw data
plus recorded transformations, and how a rebuild is verified (hash match).
Round D defines the contract; restore drills belong to
[BACKUP_RECOVERY_AND_REBUILD.md](./BACKUP_RECOVERY_AND_REBUILD.md).

### Run-to-data binding
How research and backtest runs record the exact dataset versions they consumed,
so the data-period ledger (QUANT-003) and experiment registry (QUANT-001) can
cite them. Design in Rounds D/G/H.

## Known inputs (already decided)

- Deterministic reproducibility with immutable inputs, seeds, and
  code/data/config hashes — VAL-003 (`PROPOSED`).
- Quarantine-before-repair means originals are never overwritten — DATA-005;
  every repair is a new version by construction.
- Point-in-time events are keyed by actual release timestamp and revision
  vintage — DATA-004; vintages are a versioning dimension this document must
  accommodate.
- A data-period ledger must record research vs untouched-testing usage —
  QUANT-003 (depends on D-002).

## Open questions

| Question | Resolved by |
|----------|-------------|
| Lineage schema and where it is stored | Round D |
| Versioning scheme across raw, repaired, and derived data | Round D |
| Hashing granularity and recording mechanism | Rounds D/F (with VAL-003 acceptance) |
| Rebuildability contract scope and verification method | Round D |
| Run-to-data binding format serving the experiment registry and data-period ledger | Rounds D/G/H (QUANT-001, QUANT-003, D-002) |
