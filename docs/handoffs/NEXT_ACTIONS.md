# Next Actions

- **Owner:** Jacob Depares
- **Last updated:** 2026-08-17

## Exact next action (do this first)

Draft the 44 missing domain skeletons in `docs/04-data` … `docs/09-delivery`
per the saved workflow script (or inline if agent limits persist), then run
the completeness-critic verification over docs/02–09.

Completion criteria: all 53 files of folders 02–09 exist with compliant
headers; critic reports zero missing files, zero overclaims; issues fixed.

## Then, in order

1. Write `docs/00-governance/DOCUMENT_INDEX.md` listing every file (navigation
   map + planned diagrams list).
2. Update `DISCOVERY_STATUS.md` (Phase 0 → complete) and refresh handoffs.
3. Documentation-only checkpoint commit (verify no secrets first; never push).
4. Ask Jacob Round A batch 2 (≤8 questions): jurisdictions/legal entity
   (Q-006); budget/horizon/availability/team/infrastructure (Q-007); KPIs +
   non-goals (Q-008); measurable backtest-"accuracy" definition (Q-009);
   secure PostgreSQL read-only access path (Q-001); cBot location (Q-002).
5. On answers: update INTERVIEW_RECORD, QUESTION_REGISTER, PROJECT_CHARTER,
   REQUIREMENTS_CATALOGUE, DECISION_LOG; produce Round A summary for Jacob's
   domain approval.
6. Begin Phase 1 V1 forensic audit (repo-side via read-only `gh`; DB waits on
   Q-001) → populate V1_AUDIT.md / V1_REUSE_REGISTER.md; then Round B.

## Files to read first (fresh session)

`CLAUDE.md` → `docs/00-governance/DOCUMENT_INDEX.md` (if present) →
`docs/handoffs/CURRENT_STATE.md` → this file →
`docs/00-governance/DECISION_LOG.md`, `QUESTION_REGISTER.md`.

## Questions for Jacob (open)

Q-001, Q-002, Q-006, Q-007, Q-008, Q-009 (see QUESTION_REGISTER.md).
