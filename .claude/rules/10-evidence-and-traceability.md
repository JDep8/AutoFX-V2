# 10 — Evidence and Traceability (entry point)

Detailed rules: [quantitative-evidence.md](quantitative-evidence.md) and
[documentation-and-traceability.md](documentation-and-traceability.md).
This file defines the two label systems used across the corpus and how they
differ. Both are mandatory; they answer different questions.

## Lifecycle status (what state is this item in?)

`PROPOSED`, `OWNER_APPROVED`, `IMPLEMENTED`, `TESTED`, `PAPER_VALIDATED`,
`LIVE_VALIDATED`, `REJECTED`, `SUPERSEDED` — and only these, applied to
**governed items** (requirements, decisions, strategies, books,
components, tests, validation evidence). Per D-032, descriptive progress
states are permitted for document headers, rounds, registers, gates, and
workflow status, and never imply a lifecycle status (authoritative rule:
[documentation-and-traceability.md](documentation-and-traceability.md)
§ Document standard). Never describe proposed/implemented work as tested;
never describe a backtest as live-validated.

## Evidence classification (how do we know this?)

| Label | Meaning |
|-------|---------|
| `VERIFIED` | Supported by inspected evidence (command output, file read, cited source) |
| `USER-STATED` | Explicitly supplied by Jacob but not independently verified |
| `INFERRED` | Reasoned conclusion from other facts; the reasoning is recorded |
| `PROPOSED` | Recommendation awaiting acceptance |
| `UNKNOWN` | Missing evidence or unresolved question |
| `CONFLICT` | Two sources disagree; Jacob must resolve |

Notes: `PROPOSED` appears in both systems with the same meaning. A decision
can be `OWNER_APPROVED` (lifecycle) while its underlying facts remain
`USER-STATED` (evidence) — record both when they diverge.

## Conflict rule

When sources disagree, record the conflict and both source locations in the
Decision Log or Question Register. **Never silently choose a winner.**

## Traceability rule

Every material requirement has a unique ID (`BUS` `FR` `NFR` `DATA` `QUANT`
`VAL` `RISK` `EXEC` `SEC` `OPS` `UX` `RES` `CONTENT`) and traces to design,
tests, evidence, status, owner, and decision via
[TRACEABILITY_MATRIX.md](../../docs/00-governance/TRACEABILITY_MATRIX.md).
Profitability is never guaranteed; uncertainty and degradation are always
reported.
