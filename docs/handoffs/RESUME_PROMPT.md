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
   to Fable and `/effort` must confirm Ultracode. (Verified working on this
   machine 2026-08-18 — MODEL_ROUTING_POLICY.md § Verification record — but
   the per-session check remains mandatory before critical work.)
2. Read, in order: `CLAUDE.md`; `.claude/rules/00-discovery-gate.md`;
   `docs/00-governance/DOCUMENT_INDEX.md`; `docs/handoffs/CURRENT_STATE.md`;
   `docs/handoffs/NEXT_ACTIONS.md`; then only the documents the active task
   needs.
3. Verify git state: working directory `C:\AutoFXV2.0`; report current
   branch (expected `planning/discovery-handoff`), `git status`, and
   `git log --oneline -5`. The recovery reconciliation is committed
   (`d2f0d3a`). If the 2026-08-18 model-governance change set is
   uncommitted, that is expected — Jacob reviews and commits it
   (NEXT_ACTIONS.md § B-1).
4. Restate the no-build gate: implementation is prohibited until Jacob
   explicitly writes
   `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>`
   and wireframes are separately gated behind `AUTHORISE WIREFRAME ONLY`.
   Do not modify V1, write to PostgreSQL, or connect to cTrader. Never
   expose or commit secrets. Per D-015, environment-visible external
   tooling (user/account-scope plugins and connectors) is OUT-OF-SCOPE and
   NOT AUTHORISED FOR AUTOFX USE — never authenticate, invoke, remove, or
   modify it; only project-scoped tools approved in TOOLING_REGISTER.md are
   authorised. Per D-017, the model-governance package
   (`.claude/skills/autofx-model-governor/` + four `autofx-*` agents) is
   `OWNER_APPROVED` (2026-08-18): load the `autofx-model-governor` skill
   BEFORE any delegation or critical acceptance, and follow
   MODEL_ROUTING_POLICY.md. Round A and the V1 audit remain owner-gated —
   do not start them without Jacob's input (B-3/B-5).
5. Do NOT re-ask answered interview questions — answered material is in
   `docs/01-discovery/INTERVIEW_RECORD.md` (Round A batch 1 answered; batch
   2 asked, awaiting answers). Never convert an answered question back to
   OPEN.
6. The terminal recovery audit is COMPLETE and the recovered state
   OWNER_APPROVED (2026-08-18) — do not redo it. The model-governance
   package is `OWNER_APPROVED` (Q-012 RESOLVED) — do not recreate or
   revalidate it. Continue from the first incomplete item in
   NEXT_ACTIONS.md. Items blocked on Jacob (manual commit B-1; Round A
   batch 2 answers B-3; explicit V1-audit go B-5) wait for his input — do
   not start them unprompted.
7. Restate the active phase, round, gate status, last completed checkpoint,
   current objective, and blockers, then proceed only within the authorised
   scope above.

The repository documents are the sole source of truth. Do not reconstruct
anything from prior conversation memory, do not restart discovery, and do not
claim any work is complete beyond what CURRENT_STATE.md records as VERIFIED.

---

No secrets appear in this file or anywhere in the repository.
