# Documentation and Traceability Rules

## Document standard

Every document in `docs/` carries a header with: Owner, Status, Version,
Last reviewed, Dependencies, Approval evidence, and a pointer to its open
questions. Status uses only the approved vocabulary (see root `CLAUDE.md`).
Skeleton documents are `PROPOSED` with "no content owner-approved" stated
explicitly. Unknowns are written as open questions — never as plausible filler.

## Requirement records

Prefixes: `BUS` business, `FR` functional, `NFR` non-functional, `DATA` data,
`QUANT` quantitative research, `VAL` validation, `RISK` risk, `EXEC` execution,
`SEC` security, `OPS` operations, `UX` user experience, `RES` research centre,
`CONTENT` content/business.

Every requirement includes: source, rationale, priority, status, owner,
acceptance criterion, dependent decisions, design reference, test/evidence
reference, and implementation phase. TBD fields are shown as TBD with the
round that will resolve them.

## Review structure for material features/decisions

Objective; current problem/evidence; proposed design; alternatives considered;
implementation concept; benefits; risks/failure modes; dependencies;
acceptance evidence; unresolved owner decisions.

## Registers (docs/00-governance/)

- `DECISION_LOG.md` — every material decision, including the seven legacy
  conflicts (D-001…D-007). Decisions affecting leakage, holdout, risk,
  drawdown, sizing, live safety, or compliance require Jacob's explicit
  approval.
- `QUESTION_REGISTER.md` — open/blocking questions; safety-critical ambiguity
  fails closed and lands here.
- `ASSUMPTION_REGISTER.md` — provisional defaults, always `PROPOSED`.
- `TRACEABILITY_MATRIX.md` — requirement → design → test/evidence → status.
- `DOCUMENT_INDEX.md` — navigation map; updated whenever files change.

History is never erased: superseded items are marked `SUPERSEDED`/`REJECTED`
with a pointer to their replacement, not deleted.

## Diagrams

Use diagrams where they reduce ambiguity (Mermaid preferred in-repo). Minimum
set is listed in `DOCUMENT_INDEX.md` § Diagrams; each diagram names its owner
document.

## Handoff protocol (docs/handoffs/)

- `CURRENT_STATE.md` — date/time+TZ, phase and authorisation state, last
  completed atomic task, changed docs/requirements/decisions, verified facts,
  contradictions/blockers, branch+revision+working-tree, checks run with exact
  results, known partial work.
- `NEXT_ACTIONS.md` — one exact next action first, then ordered follow-ups,
  files to read, questions for Jacob, completion criteria.
- `RESUME_PROMPT.md` — short copy/paste prompt for a fresh session; verify
  repo state and read handoffs before acting; no secrets; no unsupported
  completion claims.
- `SESSION_LOG.md` — append-only concise chronology.

Checkpoint triggers: end of any session; ~60–70% context (finish atomic task,
refresh handoffs); ~75–80% (no new domain; checkpoint and compact/restart);
any session/weekly-limit warning (stop opening new work, write the full
checkpoint, record the reset time shown by the usage interface — never guess
it).
