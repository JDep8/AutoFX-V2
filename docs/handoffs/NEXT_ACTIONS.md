# Next Actions

- **Owner:** Jacob Depares
- **Last updated:** 2026-08-18 (post-recovery reconciliation + D-017 gate)

Ordered, bounded, acceptance-criterion based. Section A needs no further
authority; Section B waits on Jacob. Nothing anywhere authorises
implementation — the no-build gate stands.

**Sequencing rule (D-017): SATISFIED 2026-08-18** — the model-governance
package and its validation results are `OWNER_APPROVED` by Jacob. All
delegation and critical acceptance route through the
`autofx-model-governor` skill per MODEL_ROUTING_POLICY.md. Round A
resumption (B-3) and the V1 audit (B-5) remain separately owner-gated.

Completed and removed from this list: terminal recovery audit (recovered
state OWNER_APPROVED 2026-08-18); plugin installation (three D-013 plugins
INSTALLED 2026-08-18, commit `39e2730`, recorded in TOOLING_REGISTER.md);
recovery-reconciliation commit (`d2f0d3a`, 2026-08-18 01:22 UTC — presumed
Jacob's execution of the previous B-1; confirmation requested).

## A — Claude may do without further authority

1. **Register upkeep** after any owner input this list triggers
   (Decision/Question/Assumption/Traceability/DOCUMENT_INDEX + handoff
   refresh per `.claude/rules/20-session-continuity.md`). Open no new
   discovery work and use no subagents (D-017) without Jacob's instruction.

## B — Requires Jacob's decision or explicit authorisation

1. **Commit the model-governance change set manually** (owner instruction
   2026-08-18: Jacob creates the commit himself; no automatic commit;
   package already approved). Proposed commands (PowerShell-safe, run
   separately):
   `git add -A`
   then
   `git commit -m "config: add AutoFX model-governance package (D-017) - governor skill + 4 read-only plan-mode agents, validated vs Claude Code 2.1.234, Q-012 resolved, registers and handoffs updated"`
   Optional at the same time: rename the default branch with
   `git branch -m master main` (this repo's default is currently `master`).
2. **Approve the model-governance package (D-017) — COMPLETE 2026-08-18.**
   Package and validation results `OWNER_APPROVED` by Jacob (spec supplied
   in-session, Q-012 RESOLVED; validated vs Claude Code 2.1.234). Kept in
   place to preserve numbering; no action remains.
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
