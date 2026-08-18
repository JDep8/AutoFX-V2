# Next Actions

- **Owner:** Jacob Depares
- **Last updated:** 2026-08-18 (post-recovery reconciliation + D-017 gate)

Ordered, bounded, acceptance-criterion based. Section A needs no further
authority; Section B waits on Jacob. Nothing anywhere authorises
implementation — the no-build gate stands.

**Sequencing rule (D-017, OWNER_APPROVED 2026-08-18):** after the B-1
commit, the model-governance package (B-2) precedes everything else. Until
it is `OWNER_APPROVED`: no Round A resumption, no V1 forensic audit, no
subagent use, no acceptance of any critical discovery artifact.

Completed and removed from this list: terminal recovery audit (recovered
state OWNER_APPROVED 2026-08-18) and plugin installation (three D-013
plugins INSTALLED 2026-08-18, commit `39e2730`, recorded in
TOOLING_REGISTER.md).

## A — Claude may do without further authority

1. **Register upkeep** after any owner input this list triggers
   (Decision/Question/Assumption/Traceability/DOCUMENT_INDEX + handoff
   refresh per `.claude/rules/20-session-continuity.md`). Open no new
   discovery work and use no subagents (D-017) without Jacob's instruction.

## B — Requires Jacob's decision or explicit authorisation

1. **Review and commit the recovery-reconciliation change set** (owner
   instruction: no automatic commit). Proposed commands (PowerShell-safe,
   run separately):
   `git add -A`
   then
   `git commit -m "docs: terminal recovery - reconcile handoff state (fcde457/39e2730 confirmed), record plugin install + Fable/Ultracode verification, add D-015..D-017 rulings and model-governance gate"`
   Optional at the same time: rename the default branch with
   `git branch -m master main` (this repo's default is currently `master`).
2. **Model-governance package (D-017) — the single first work item after
   the B-1 commit.** Jacob supplies the migration-runbook Prompt 6A
   specification (Q-012 — not present in this repository; fails closed
   until supplied); *then Claude* creates and validates the project-local
   AutoFX model-governance package to that specification (documentation and
   project-local governance artefacts only; the no-build gate is
   unaffected). *Done when:* the validated package is `OWNER_APPROVED` by
   Jacob. **Gates B-3…B-5, all subagent use, and acceptance of any critical
   discovery artifact.**
3. **Round A batch 2 answers** (only after B-2 approval) — Q-001 (PostgreSQL
   read-only path), Q-002 (cBot location), Q-006 (jurisdictions/entity),
   Q-007 (budget/horizon/availability/team/infra), Q-008 (KPIs/non-goals),
   Q-009 (accuracy form). *Then Claude:* record verbatim, update registers,
   produce the Round A domain summary. *Done when:* summary
   `OWNER_APPROVED` by Jacob.
4. **Q-011 (D-014):** keep both rule-file sets or consolidate.
5. **Explicit go for the V1 forensic audit, repo-side only** (only after
   B-2 approval; read-only `gh`; never clone into V2; never copy code):
   start with V1's own review docs (ARCHITECTURE.md, DATA_ACCURACY.md,
   PORTFOLIO_GENERATOR_REVIEW*.md, FORWARD_TEST.md, E2E_ANALYSIS.md), then
   the ten audit areas in V1_AUDIT.md § Audit plan. *Done when:*
   V1_AUDIT.md findings populated with evidence labels and
   V1_REUSE_REGISTER.md classifications proposed (each with evidence +
   risk).
6. Later gates (unchanged): per-round domain approvals → `AUTHORISE WIREFRAME
   ONLY` (Round O) → Discovery Exit Review → the implementation authorisation
   phrase.

## Files to read first (fresh session)

`CLAUDE.md` → `.claude/rules/00-discovery-gate.md` →
`docs/00-governance/DOCUMENT_INDEX.md` → `docs/handoffs/CURRENT_STATE.md` →
this file → `DECISION_LOG.md`, `QUESTION_REGISTER.md`,
`docs/01-discovery/INTERVIEW_RECORD.md`.
