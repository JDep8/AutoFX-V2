# Resume Prompt

Copy/paste this into a fresh Claude Code session started in `C:\AutoFXV2.0`:

---

Resume the AutoFX V2.0 discovery engagement. Before acting: verify the
working directory is `C:\AutoFXV2.0` on branch `main`, run `git status` and
`git log --oneline -5`, then read `CLAUDE.md`,
`docs/handoffs/CURRENT_STATE.md`, and `docs/handoffs/NEXT_ACTIONS.md`.
Confirm the no-build gate is still active (it is unless Jacob has written the
exact authorisation phrase recorded in `CLAUDE.md`). Compare the recorded
next action with Jacob's latest instruction, restate phase/checkpoint/
objective/blockers, and continue from the first incomplete completion
criterion in `NEXT_ACTIONS.md`. Do not restart discovery, do not repeat
answered interview questions (see `docs/01-discovery/INTERVIEW_RECORD.md`),
and do not reconstruct state from chat memory — the repository documents are
the source of truth.

---

No secrets appear in this file or anywhere in the repository. Do not claim
any work is complete beyond what `CURRENT_STATE.md` records as verified.
