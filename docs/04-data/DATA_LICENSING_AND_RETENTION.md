# Data Licensing and Retention
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.1
- **Last reviewed:** 2026-08-18
- **Dependencies:** [DATA_SOURCE_REGISTER.md](./DATA_SOURCE_REGISTER.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-008), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-006)
- **Approval evidence:** None yet

## Purpose

This document will record, per data provider, what AutoFX V2 is legally allowed
to do with the data: store it, keep it after a subscription ends, derive
research from it, and (if ever relevant) show it to anyone else. It exists
because licensing terms silently shape architecture — a provider whose data
cannot be retained cannot anchor a ten-year backtest archive. Nothing here is
resolved yet; every term must come from actual provider documents, dated.

## Scope and decisions this document will own

- The licensing, redistribution, and retention position per provider selected
  or shortlisted in [DATA_SOURCE_REGISTER.md](./DATA_SOURCE_REGISTER.md).
- The retention policy AutoFX applies to each stored dataset (what is kept, for
  how long, and on what legal basis).
- Cost records per provider and the budget consequence of licensing choices.
- It does **not** own provider selection (the register does) or backup
  mechanics (see [BACKUP_RECOVERY_AND_REBUILD.md](./BACKUP_RECOVERY_AND_REBUILD.md)).

## Structure skeleton

### Licensing summary per provider
One entry per provider: licence type, permitted uses, storage rights,
post-termination retention rights, derived-data rights, redistribution
position, dated source of each claim. Populated in Round D from actual terms
documents — never from memory or assumption.

### Redistribution and display boundaries
Whether any output of the platform (charts, published content under Priority 3)
would constitute redistribution under each licence. D-008 confines the platform
to Jacob's personal use, which narrows but does not eliminate this question;
the Priority 3 content business is assessed separately (Round M; D-018
review gate, BUS-008).

### Retention obligations and rights
Per dataset: minimum retention the project needs (backtest reproducibility per
VAL-003 implies long retention) versus maximum retention the licence allows.
Conflicts between the two are blocking questions for Round D.

### Cost register
Recorded subscription and usage costs per provider, once quoted. No figures are
entered until an actual quote or published price is in hand; budget context is
the D-019 ceiling (AUD 400/month; every expense pre-approved). Round D.

### Licence-change and termination handling
What happens to stored history if a provider is dropped or changes terms;
whether rebuild from an alternative source is possible (links to
[DATA_LINEAGE_AND_VERSIONING.md](./DATA_LINEAGE_AND_VERSIONING.md)
rebuildability). Round D.

## Known inputs (already decided)

- Sole user is Jacob, personal capital, no customers — D-008 / BUS-005
  (`OWNER_APPROVED`); this bounds the redistribution analysis.
- FMP terms must be part of its DATA-007 evaluation — nothing about FMP
  licensing is assumed.
- Reproducibility requires immutable retained inputs — VAL-003 (`PROPOSED`),
  which makes retention rights a hard requirement, not a nice-to-have.
- Content business compliance is assessed separately — CONTENT-003, Round M.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Actual licence terms (storage, retention, derived data, redistribution) per candidate provider | Round D, dated terms research |
| Do any licences forbid retention long enough for reproducible backtests (VAL-003)? | Round D |
| Provider costs and their fit within budget | Round D; budget ceiling decided (D-019: AUD 400/month, per-expense approval) |
| Jurisdiction/legal entity that the licences would bind | Decided for now (D-018: Jacob personally, tax-resident Australia); re-examined at the D-018 pre-commercialisation gate if an entity is created |
| Whether Priority 3 content use would be redistribution under any licence | Round M (with Round D terms evidence) |
