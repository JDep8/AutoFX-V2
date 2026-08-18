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
5. Round A: batches 1 AND 2 are fully answered (batch 2 verbatim in
   `docs/01-discovery/INTERVIEW_RECORD.md` § Batch 2 answers, 2026-08-18;
   decisions D-018…D-024). Do NOT re-ask any of it. **Round A is NOT
   closed** (owner direction 2026-08-18): the completion assessment
   (DISCOVERY_STATUS.md) found two INCOMPLETE topics — success hierarchy
   (Q-015) and KPI-framework approval (Q-008 remainder, framework
   `PROPOSED` in PROJECT_CHARTER.md). Four closure questions await Jacob
   (NEXT_ACTIONS § B-1); the Round A summary stays `PROPOSED` until he
   approves it.
6. Repository visibility is **PUBLIC** (verified 2026-08-18; Jacob's
   change; Q-014 pending — temporary or permanent). Never change
   visibility; treat sensitive-material placement as a standing
   consideration until Q-014 is decided.
7. Items blocked on Jacob (NEXT_ACTIONS § B): the four closure questions;
   Round A summary approval; `autofx_v1_readonly` provisioning (D-022);
   explicit V1-audit go; Q-011; Q-013. Do not start them unprompted. The V1
   forensic audit has NOT started.
8. Restate the active phase, round, gate status, last completed checkpoint,
   current objective, and blockers, then proceed only within the authorised
   scope above.

The repository documents are the sole source of truth. Do not reconstruct
anything from prior conversation memory, do not restart discovery, and do
not claim any work is complete beyond what CURRENT_STATE.md records as
VERIFIED.

---

No secrets appear in this file or anywhere in the repository.
