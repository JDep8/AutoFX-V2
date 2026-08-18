# Next Actions

- **Owner:** Jacob Depares
- **Last updated:** 2026-08-18 (post command-governance research; see
  SESSION_LOG)

Ordered, bounded, acceptance-criterion based. Section A needs no further
authority; Section B waits on Jacob. Nothing anywhere authorises
implementation — the no-build gate stands.

Completed and removed: terminal recovery audit; plugin install (`39e2730`);
reconciliation commit (`d2f0d3a`); model-governance commit (`00ad2cc`);
Round A batch 2 recording + D-018…D-024 (`ad1d1e4`); D-024 execution
(`8bea651`; repo https://github.com/JDep8/AutoFX-V2); Round A
closure-assurance pass 2026-08-18 (completion assessment, KPI framework
`PROPOSED`, ~20-document reconciliation, PUBLIC visibility verified/Q-014,
B–O assurance matrix, coverage check — this checkpoint's commit).

## A — Claude may do without further authority

1. **Register upkeep** after any owner input (Decision/Question/Assumption/
   Traceability/DOCUMENT_INDEX + handoff refresh). Delegation only through
   the `autofx-model-governor` skill per MODEL_ROUTING_POLICY.md.

## B — Requires Jacob's decision or explicit authorisation

1. **Answer the four Round A closure questions** (asked 2026-08-18 in
   chat; recorded in QUESTION_REGISTER and PROJECT_CHARTER):
   a. Q-015 — confirm/amend the success hierarchy
      (PROJECT_CHARTER.md § Success hierarchy).
   b. Q-008 remainder — approve/edit/reduce the 20-KPI framework
      (PROJECT_CHARTER.md § KPI framework).
   c. Q-014 — repository visibility: revert to private / public until a
      named milestone / permanently public with a publication policy
      (TOOLING_REGISTER.md § Repository visibility).
   d. Confirm the Round A completion assessment incl. its COMPLETE-FOR-
      ROUND-A deferrals (DISCOVERY_STATUS.md § Round A completion
      assessment).
   *Then Claude:* record verbatim, update registers, finalise the Round A
   summary for approval.
2. **Approve (or amend) the Round A summary** (INTERVIEW_RECORD.md) —
   *Done when:* approved; Round A closes; summary becomes `OWNER_APPROVED`.
3. **Provision `autofx_v1_readonly`** + secure configuration path outside
   chat/repo (D-022 remainder) — unblocks DB-side V1 audit depth.
4. **Explicit go for the V1 forensic audit, repo-side** (read-only `gh`;
   never clone into V2; never copy code; D-023 makes
   `code/TradingViewBridge.cs` + `PriceBridge.cs` primary targets incl. the
   per-symbol weighting verification). *Done when:* V1_AUDIT.md findings
   populated with evidence labels; V1_REUSE_REGISTER.md classifications
   proposed with evidence + risk.
5. **Q-011** (rules-file naming) and **Q-013** (status-vocabulary scope) —
   non-blocking conventions.
6. **Optional:** extend committed `.claude/settings.json` allowlist to the
   D-024 git model (currently read-only/V1-scope; per-session approvals in
   use).
7. **Approve/amend the Claude Code command policies** —
   CLAUDE_CODE_COMMAND_RUNBOOK.md § 7–8 (all `PROPOSED`; researched
   2026-08-18 against v2.1.234). Non-blocking: until approved, Claude
   operates to the runbook's most conservative reading (mutating/
   installing/connecting/cloud commands treated as owner-gated).
8. Later gates (unchanged): per-round domain approvals → `AUTHORISE
   WIREFRAME ONLY` (Round O) → Discovery Exit Review → the implementation
   authorisation phrase.

## Files to read first (fresh session)

`CLAUDE.md` → `.claude/rules/00-discovery-gate.md` →
`docs/00-governance/DOCUMENT_INDEX.md` → `docs/handoffs/CURRENT_STATE.md` →
this file → `DECISION_LOG.md` (D-018…D-024), `QUESTION_REGISTER.md`
(Q-013…Q-015), `docs/01-discovery/DISCOVERY_STATUS.md` (completion
assessment + B–O matrix), `docs/00-governance/PROJECT_CHARTER.md` (KPI
framework), `docs/01-discovery/INTERVIEW_RECORD.md`.
