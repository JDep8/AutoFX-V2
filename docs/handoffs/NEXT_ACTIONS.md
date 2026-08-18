# Next Actions

- **Owner:** Jacob Depares
- **Last updated:** 2026-08-18 06:08 UTC (post Round A reconciliation +
  simulation requirement + runbook correction)

Ordered, bounded, acceptance-criterion based. Section A needs no further
authority; Section B waits on Jacob — **presented one at a time per
D-025**. Nothing anywhere authorises implementation — the no-build gate
stands.

Completed and removed: terminal recovery audit; plugin install
(`39e2730`); reconciliation commit (`d2f0d3a`); model-governance commit
(`00ad2cc`); Round A batch 2 + D-018…D-024 (`ad1d1e4`); D-024 execution
(`8bea651`); closure-assurance pass (`2167e62`); runbook v0.1.0
(`2e19d9b`; catalogue later REJECTED via D-035); Round A reconciliation
D-025…D-035 + simulation spec + runbook v0.2.0 correction (this
checkpoint's commit). Resolved 2026-08-18: Q-008, Q-011, Q-013, Q-014,
Q-015, Q-016.

## A — Claude may do without further authority

1. **Register upkeep** after any owner input (Decision/Question/
   Assumption/Traceability/DOCUMENT_INDEX + handoff refresh). Delegation
   only through `autofx-model-governor`. Every substantive task ends
   with validation + commit + push to `planning/discovery-handoff`
   (D-026), with the D-033 sensitivity stop-rule checked before each
   push.

## B — Requires Jacob's decision (one at a time, D-025)

1. **Approve or amend the Round A closure candidate** —
   INTERVIEW_RECORD.md § Round A closure candidate. *Done when:* Jacob
   approves; Round A closes; candidate becomes `OWNER_APPROVED`. (This
   is the current single open question.)
2. **Command-runbook v0.2.0 policies** (D-035; B-7 rejected in v0.1.0
   form) — approve one at a time when Jacob chooses; conservative
   reading applies until then.
3. **Provision `autofx_v1_readonly`** + secure configuration path
   outside chat/repo (D-022) — unblocks DB-side V1 audit depth only.
4. **Explicit go for the repo-side V1 forensic audit** (read-only `gh`;
   never clone into V2; never copy code; D-023 bridge files + weighting
   verification are primary targets). *Done when:* V1_AUDIT.md findings
   populated with evidence labels; V1_REUSE_REGISTER.md classifications
   proposed.
5. **Optional:** extend committed `.claude/settings.json` allowlist to
   the D-024 git model (per-session approvals in use meanwhile).
6. Later gates (unchanged): per-round domain approvals → `AUTHORISE
   WIREFRAME ONLY` (Round O) → Discovery Exit Review → the
   implementation authorisation phrase. Return-to-private visibility
   change (D-033) happens only on Jacob's explicit authorisation.

## Files to read first (fresh session)

`CLAUDE.md` → `.claude/rules/00-discovery-gate.md` →
`docs/00-governance/DOCUMENT_INDEX.md` → `docs/handoffs/CURRENT_STATE.md`
→ this file → `DECISION_LOG.md` (D-025…D-035), `QUESTION_REGISTER.md`,
`docs/01-discovery/DISCOVERY_STATUS.md` (assessment + matrix),
`docs/01-discovery/INTERVIEW_RECORD.md` (§ Round A closure candidate),
`docs/00-governance/PROJECT_CHARTER.md`,
`docs/06-execution-and-risk/TRADING_SIMULATION_AND_CERTIFICATION_SPEC.md`,
`docs/00-governance/CLAUDE_CODE_COMMAND_RUNBOOK.md` (v0.2.0 + errata).
