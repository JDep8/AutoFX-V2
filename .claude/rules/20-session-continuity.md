# 20 — Session Continuity (entry point)

Detailed handoff protocol: [documentation-and-traceability.md](documentation-and-traceability.md) § Handoff protocol.

## Workspace (D-011, OWNER_APPROVED 2026-08-18)

The **terminal** (Claude Code CLI) is the primary workspace. Claude Desktop
remains available for visual review and wireframes. The repository documents
are the source of truth in both — never chat memory.

## Session start

1. Read root `CLAUDE.md`, then `docs/00-governance/DOCUMENT_INDEX.md`.
2. Read `docs/handoffs/CURRENT_STATE.md`, `NEXT_ACTIONS.md`.
3. Verify git state (branch, last commit, working-tree cleanliness).
4. Restate phase, round, last checkpoint, objective, blockers, and no-build
   status before acting. Never re-ask answered interview questions
   (see `docs/01-discovery/INTERVIEW_RECORD.md`).

## Model discipline (D-012 — see MODEL_ROUTING_POLICY.md)

Main terminal sessions launch with `--model best --effort ultracode`; verify
via `/status` (best → Fable) and `/effort` (Ultracode) **before critical
work**. Routing details:
[MODEL_ROUTING_POLICY.md](../../docs/00-governance/MODEL_ROUTING_POLICY.md).

## Session end / rollover (context or weekly capacity)

**Before** context or weekly capacity becomes constrained:

1. Finish the current atomic task only; open nothing new.
2. Update `CURRENT_STATE.md`, `NEXT_ACTIONS.md`, `RESUME_PROMPT.md`; append
   to `SESSION_LOG.md`.
3. Update every register the session touched.
4. Checkpoint in git (documentation-only; verify no secrets; never push
   without Jacob's explicit instruction).
5. Record the reset time exactly as the usage interface displays it — never
   guess it.

Thresholds: ~60–70% context → finish atomic task + refresh handoffs;
~75–80% → checkpoint and start a fresh session; any limit warning → full
checkpoint immediately.

## Resuming

Use `docs/handoffs/RESUME_PROMPT.md` verbatim in the fresh session. Continue
from the first incomplete acceptance criterion in `NEXT_ACTIONS.md` — never
restart discovery, never reconstruct state from conversation memory.
