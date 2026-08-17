# Point-in-Time Data Policy
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [GLOSSARY.md](../00-governance/GLOSSARY.md) (point-in-time, leakage), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (DATA-004), [MARKET_AND_NEWS_CALENDARS.md](./MARKET_AND_NEWS_CALENDARS.md), [DATA_LINEAGE_AND_VERSIONING.md](./DATA_LINEAGE_AND_VERSIONING.md)
- **Approval evidence:** None yet

## Purpose

This policy will define how macro and news data is stored so that every value
is exactly what was knowable at a given moment — never a later revision quietly
standing in for the original release. Backtests that see revised numbers are a
form of leakage: they trade on information the market did not yet have. The
policy makes point-in-time correctness a structural property of the data model,
not a discipline the researcher must remember.

## Scope and decisions this document will own

- The canonical keying rule for economic events: actual release timestamp plus
  revision vintage, never the economic period alone.
- The mandatory field set for every point-in-time event.
- Revision and vintage handling: how later corrections are stored alongside,
  not over, originals.
- The point-in-time audit that DATA-004's acceptance criterion demands.
- It does **not** own exclusion-window behaviour (see
  [MARKET_AND_NEWS_CALENDARS.md](./MARKET_AND_NEWS_CALENDARS.md)).

## Structure skeleton

### Canonical event key
Events are keyed by actual release timestamp and revision vintage — never only
by economic period (e.g. "July CPI"). This rule is already mandated by
DATA-004 and the Glossary definition; Round D specifies the exact key
composition and collision handling.

### Mandatory event fields
Per DATA-004, each event carries: scheduled time, actual release time,
consensus, previous, revision/vintage identifier, surprise, currency/region,
severity, and provenance. Round D confirms field semantics per provider and
what to do when a provider cannot supply a field (fail-closed candidates).

### Scheduled versus actual time semantics
How the gap between scheduled and actual release time is stored and used —
late releases, early releases, unscheduled events. Round D defines the rules;
downstream exclusion-window behaviour is D-007's territory.

### Revision and vintage storage
Every revision is a new vintage; originals are immutable. How many vintages a
provider actually exposes, and how backfilled history is vintage-stamped, are
Round D provider questions.

### Surprise computation and provenance
Whether "surprise" is provider-supplied or derived (actual minus consensus),
and how consensus provenance is recorded so a fabricated or shifted consensus
cannot corrupt research. Round D.

### Point-in-time audit design
The audit demonstrating that no query executed "as of" a date can return
information released after that date. Design in Round D; the audit itself is
future work and will only ever be described with honest status labels.

## Known inputs (already decided)

- DATA-004 mandates point-in-time macro events with the full field list and
  keying by actual release timestamp + vintage (`PROPOSED`, acceptance = PIT
  audit passes).
- Glossary defines point-in-time as "values keyed by actual release timestamp
  and revision vintage" (canonical sign-off in Round E).
- Leakage definition (Glossary): any path by which unavailable information
  influences a decision or its evaluation.
- Missing news data fails closed — D-007 direction; this policy must make the
  "missing" condition detectable.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Exact event key composition and collision handling (simultaneous releases) | Round D |
| Which providers can actually supply actual-release timestamps and revision vintages, and how far back? | Round D (provider evaluation, incl. DATA-007 for FMP) |
| Field-level fallbacks when a provider lacks consensus, severity, or vintage data | Round D |
| Is surprise provider-supplied or derived, and from whose consensus? | Round D |
| Severity taxonomy (what makes an event high-severity) | Round D; enforcement in Rounds C/F (D-007) |
| Point-in-time audit method and pass criteria | Round D design; acceptance per DATA-004 |
