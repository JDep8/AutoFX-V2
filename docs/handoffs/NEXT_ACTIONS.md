# Next Actions

- **Owner:** Jacob Depares
- **Last updated:** 2026-08-18 04:14 UTC (post D-024 execution)

Ordered, bounded, acceptance-criterion based. Section A needs no further
authority; Section B waits on Jacob. Nothing anywhere authorises
implementation — the no-build gate stands (D-019/D-022 restate it).

Completed and removed from this list: terminal recovery audit; plugin
installation (`39e2730`); recovery-reconciliation commit (`d2f0d3a`);
model-governance package commit (`00ad2cc`, by Jacob — old B-1); Round A
batch 2 answers received and recorded verbatim 2026-08-18 with D-018…D-024
captured and all registers updated (old B-3 input received; summary approval
remains below); **D-024 execution COMPLETE 2026-08-18** — commit `ad1d1e4`,
private https://github.com/JDep8/AutoFX-V2 created, `main` default,
`main` + `planning/discovery-handoff` pushed, evidence in SESSION_LOG.md
Session 5.

## A — Claude may do without further authority

1. **Register upkeep** after any owner input (Decision/Question/Assumption/
   Traceability/DOCUMENT_INDEX + handoff refresh). Delegation only through
   the `autofx-model-governor` skill per MODEL_ROUTING_POLICY.md.
2. **Propose measurable KPI candidates** (Q-008 remainder) with the
   PROJECT_CHARTER.md update for Round A closure — candidates only; every
   target/threshold needs Jacob's approval.

## B — Requires Jacob's decision or explicit authorisation

1. **Approve (or amend) the Round A summary** — INTERVIEW_RECORD.md
   § Round A summary (`PROPOSED`). *Done when:* Jacob approves; Round A
   then closes and the summary becomes `OWNER_APPROVED`.
2. **Provision `autofx_v1_readonly`** and the secure configuration path
   outside chat/repo (D-022 remainder) — unblocks the DB-side V1 audit.
3. **Explicit go for the V1 forensic audit, repo-side** (read-only `gh`;
   never clone into V2; never copy code): start with V1's own review docs,
   then the ten audit areas in V1_AUDIT.md § Audit plan; D-023 makes
   `code/TradingViewBridge.cs` (+ `PriceBridge.cs`) a primary target,
   including verifying/documenting the per-symbol weighting behaviour.
   *Done when:* V1_AUDIT.md findings populated with evidence labels and
   V1_REUSE_REGISTER.md classifications proposed (REUSE/ADAPT/REJECT/
   UNKNOWN, each with evidence + risk).
4. **Q-011 (D-014):** keep both rule-file sets or consolidate.
5. **Q-013:** confirm status-vocabulary scope for document-header/progress
   fields (proposed: lifecycle labels govern item status only).
6. **Optional:** extend the committed `.claude/settings.json` allowlist to
   match the D-024 git operating model (currently read-only/V1-scope;
   D-024 operations run under per-session approvals) — separately
   reviewable configuration change.
7. Later gates (unchanged): per-round domain approvals → `AUTHORISE
   WIREFRAME ONLY` (Round O) → Discovery Exit Review → the implementation
   authorisation phrase.

## Files to read first (fresh session)

`CLAUDE.md` → `.claude/rules/00-discovery-gate.md` →
`docs/00-governance/DOCUMENT_INDEX.md` → `docs/handoffs/CURRENT_STATE.md` →
this file → `DECISION_LOG.md` (D-018…D-024), `QUESTION_REGISTER.md`,
`docs/01-discovery/INTERVIEW_RECORD.md` (§ Batch 2 answers + Round A
summary).
