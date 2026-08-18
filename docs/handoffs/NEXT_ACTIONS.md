# Next Actions

- **Owner:** Jacob Depares
- **Last updated:** 2026-08-18

Ordered, bounded, acceptance-criterion based. Section A needs no further
authority; Section B waits on Jacob. Nothing anywhere authorises
implementation — the no-build gate stands.

## A — Claude may do without further authority

1. **Terminal recovery audit** (first action, from RESUME_PROMPT.md).
   *Done when:* source-of-truth files read; git state verified; gate restated;
   recovered state presented to Jacob — then STOP for his approval.
2. **Install the three approved plugins** (D-013): product-management,
   claude-md-management, session-report. *Done when:* installed, recorded in
   TOOLING_REGISTER.md with date; no other plugin touched.
3. **V1 forensic audit, repo-side only** (read-only `gh`; never clone into
   V2; never copy code): start with V1's own review docs (ARCHITECTURE.md,
   DATA_ACCURACY.md, PORTFOLIO_GENERATOR_REVIEW*.md, FORWARD_TEST.md,
   E2E_ANALYSIS.md), then the ten audit areas in V1_AUDIT.md § Audit plan.
   *Done when:* V1_AUDIT.md findings populated with evidence labels and
   V1_REUSE_REGISTER.md classifications proposed (each with evidence + risk).
4. **Register upkeep** after any of the above (Decision/Question/Assumption/
   Traceability/DOCUMENT_INDEX + handoff refresh per
   `.claude/rules/20-session-continuity.md`).

## B — Requires Jacob's decision or explicit authorisation

1. **Review and commit this handoff change set** (owner instruction: no
   automatic commit). Proposed commands (PowerShell-safe, run separately):
   `git add -A`
   then
   `git commit -m "docs: terminal handoff - settings, numbered rule entry points, tooling/model policies, refreshed handoffs (D-011..D-014)"`
   Optional at the same time: rename the default branch with
   `git branch -m master main` (this repo's default is currently `master`).
2. **Round A batch 2 answers** — Q-001 (PostgreSQL read-only path), Q-002
   (cBot location), Q-006 (jurisdictions/entity), Q-007 (budget/horizon/
   availability/team/infra), Q-008 (KPIs/non-goals), Q-009 (accuracy form).
   *Then Claude:* record verbatim, update registers, produce the Round A
   domain summary. *Done when:* summary `OWNER_APPROVED` by Jacob.
3. **Q-011 (D-014):** keep both rule-file sets or consolidate.
4. **Approve recovered state** after the terminal recovery audit (A-1).
5. Later gates (unchanged): per-round domain approvals → `AUTHORISE WIREFRAME
   ONLY` (Round O) → Discovery Exit Review → the implementation authorisation
   phrase.

## Files to read first (fresh session)

`CLAUDE.md` → `.claude/rules/00-discovery-gate.md` →
`docs/00-governance/DOCUMENT_INDEX.md` → `docs/handoffs/CURRENT_STATE.md` →
this file → `DECISION_LOG.md`, `QUESTION_REGISTER.md`,
`docs/01-discovery/INTERVIEW_RECORD.md`.
