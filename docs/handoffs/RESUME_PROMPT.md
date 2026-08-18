# Resume Prompt

First terminal command (run in a terminal, not inside Claude):

```bash
cd C:\AutoFXV2.0 && claude --model best --effort ultracode
```

Then paste the prompt below into the fresh Claude Code session verbatim:

---

Resume the AutoFX V2.0 discovery engagement (terminal is now the primary
workspace, per D-011). Before doing anything else:

1. Verify the model configuration: `/status` must resolve `best` to Fable and
   `/effort` must confirm Ultracode. If either fails, report it and record the
   actual behaviour in docs/00-governance/MODEL_ROUTING_POLICY.md before
   critical work (Recovery item 1 in CURRENT_STATE.md).
2. Read, in order: `CLAUDE.md`; `.claude/rules/00-discovery-gate.md`;
   `docs/00-governance/DOCUMENT_INDEX.md`; `docs/handoffs/CURRENT_STATE.md`;
   `docs/handoffs/NEXT_ACTIONS.md`; then only the documents the active task
   needs.
3. Verify git state: working directory `C:\AutoFXV2.0`; report current branch
   (expected `planning/discovery-handoff`), `git status`, and
   `git log --oneline -5`. If the handoff change set is uncommitted, that is
   expected — Jacob commits it after review (Section B of NEXT_ACTIONS.md).
4. Restate the no-build gate: implementation is prohibited until Jacob
   explicitly writes
   `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>`
   and wireframes are separately gated behind `AUTHORISE WIREFRAME ONLY`.
   Do not modify V1, write to PostgreSQL, or connect to cTrader. Never
   expose or commit secrets.
5. Do NOT re-ask answered interview questions — answered material is in
   `docs/01-discovery/INTERVIEW_RECORD.md` (Round A batch 1 answered; batch 2
   asked, awaiting answers). Never convert an answered question back to OPEN.
6. Perform a recovery audit: work through CURRENT_STATE.md § Recovery
   Required; confirm registers agree on phase (Phase 0 complete), round
   (Round A in progress), and gate (ACTIVE); note any contradiction as a
   CONFLICT rather than silently fixing it.
7. Present the recovered state (phase, round, gate, git, decisions, open
   questions, recovery findings) to Jacob and **stop — continue only after
   Jacob approves the recovered state**.

The repository documents are the sole source of truth. Do not reconstruct
anything from prior conversation memory, do not restart discovery, and do not
claim any work is complete beyond what CURRENT_STATE.md records as VERIFIED.

---

No secrets appear in this file or anywhere in the repository.
