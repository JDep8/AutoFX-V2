# Resume Prompt

First terminal command (run in a terminal, not inside Claude):

```bash
cd C:\AutoFXV2.0 && claude --model best --effort ultracode
```

Then paste the prompt below into the fresh Claude Code session verbatim:

---

Resume the AutoFX V2.0 discovery engagement (terminal is the primary
workspace, per D-011). Before doing anything else:

1. Verify the model configuration per D-012: `/status` must resolve `best`
   to Fable and `/effort` must confirm Ultracode.
2. Read, in order: `CLAUDE.md`; `.claude/rules/00-discovery-gate.md`;
   `docs/00-governance/DOCUMENT_INDEX.md`; `docs/handoffs/CURRENT_STATE.md`;
   `docs/handoffs/NEXT_ACTIONS.md`; then only the documents the active task
   needs.
3. Verify git state: working directory `C:\AutoFXV2.0`; report current
   branch (expected `planning/discovery-handoff`), `git status`,
   `git log --oneline -5`, and `git remote -v` (expected: `origin` =
   https://github.com/JDep8/AutoFX-V2, private, default `main`; executed
   and VERIFIED 2026-08-18, SESSION_LOG.md Session 5). If the remote is
   unexpectedly absent, investigate via SESSION_LOG before any git action.
   Never force-push; never merge into `main` without Jacob's explicit
   approval; never touch `JDep8/AutoFX` (V1).
4. Restate the no-build gate: implementation is prohibited until Jacob
   explicitly writes
   `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>`
   and wireframes are separately gated behind `AUTHORISE WIREFRAME ONLY`.
   Do not modify V1, write to PostgreSQL, or connect to cTrader. Never
   expose or commit secrets. Per D-015, environment-visible external
   tooling is OUT-OF-SCOPE and NOT AUTHORISED. Per D-017, load the
   `autofx-model-governor` skill BEFORE any delegation or critical
   acceptance. Per D-019/D-022, the autonomous operating model and database
   model are approved but do NOT open the implementation gate.
5. **Round A is CLOSED — `OWNER_APPROVED` 2026-08-18 (D-036).** All
   Round A decisions (D-001 direction, D-008…D-010, D-018…D-036) stand;
   do NOT re-ask or reopen any of them absent genuine new conflict.
   Round B is NOT started. The D-037 roadmap is fully live: issues
   #1–#52 plus PRIVATE GitHub Project #1
   (https://github.com/users/JDep8/projects/1, fields populated) —
   reconcile both at the end of every substantive task per
   docs/09-delivery/GITHUB_PROJECT_OPERATING_MODEL.md.
6. Repository visibility is **PUBLIC by owner decision D-033**
   (temporarily, for external review; return-to-private only on Jacob's
   explicit authorisation). Never change visibility. Apply the D-033
   sensitivity stop-rule before every push.
7. Items waiting on Jacob (NEXT_ACTIONS § B, one at a time):
   command-runbook v0.2.0 policies (issue #19; NOT approved);
   `autofx_v1_readonly` provisioning (#20); explicit V1-audit go (#21);
   optional UI-only Project views (register § Views). Do not start them
   unprompted. The V1 forensic audit has NOT started. Standing rules
   D-025 (one at a time), D-026 (repository output +
   validate/commit/push), and D-037 (roadmap reconciliation) apply to
   every substantive task.
8. Restate the active phase, round, gate status, last completed checkpoint,
   current objective, and blockers, then proceed only within the authorised
   scope above.

The repository documents are the sole source of truth. Do not reconstruct
anything from prior conversation memory, do not restart discovery, and do
not claim any work is complete beyond what CURRENT_STATE.md records as
VERIFIED.

---

No secrets appear in this file or anywhere in the repository.
