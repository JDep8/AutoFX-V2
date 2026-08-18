# Current State

- **Owner:** Jacob Depares
- **Status:** Living handoff (refreshed every checkpoint)
- **Date/time:** 2026-08-18 01:08 UTC
- **Source session:** first terminal session (Claude Code CLI), session
  `0091f598-1fb5-49ef-a583-c282e5ac0675` — terminal recovery audit +
  owner-approved documentation reconciliation. Prior history: three Desktop
  sessions, 2026-08-17/18 (SESSION_LOG.md).

## Phase, round, gate

- Phase 0 (discovery repository scaffold): **COMPLETE 2026-08-17** (VERIFIED —
  completeness critic: 53 domain skeletons, 0 missing/violations/overclaims).
- Phase 1 (read-only V1 forensic assessment): NOT STARTED — gated behind
  model-governance package approval (D-017) **and** Jacob's explicit go
  (owner instructions 2026-08-18; see NEXT_ACTIONS B-5).
- Round A: IN PROGRESS — batch 1 answered; batch 2 asked 2026-08-17, **no
  answers yet** (VERIFIED against INTERVIEW_RECORD.md). Round A resumption
  is gated behind model-governance package approval (D-017) and Jacob's
  batch 2 answers.
- **No-build gate: ACTIVE.** The exact authorisation phrase is
  `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>` and has NOT been
  given. Wireframe gate `AUTHORISE WIREFRAME ONLY` also not given.
- **Terminal recovery audit: COMPLETE 2026-08-18; recovered state
  OWNER_APPROVED by Jacob** with rulings on findings F-3 → D-015 and
  F-5 → D-016 (DECISION_LOG.md).
- **Model-governance gate (D-017, OWNER_APPROVED 2026-08-18):** after the
  reconciliation commit, the single first next action is creation and
  validation of the project-local AutoFX model-governance package per
  migration-runbook Prompt 6A (specification not yet in this repository —
  Q-012, fails closed until supplied). Until that package is
  `OWNER_APPROVED`: no Round A resumption, no V1 forensic audit, no
  subagent use, no acceptance of any critical discovery artifact.

## Session configuration (D-012)

- VERIFIED 2026-08-18 (first terminal session): `claude --model best
  --effort ultracode` works on this machine — session resolved to Fable 5
  (`claude-fable-5`) with Ultracode effort. Recovery item 1 CLOSED; record
  in MODEL_ROUTING_POLICY.md § Verification record. Per-session `/status` +
  `/effort` checks remain mandatory.

## Working directory / git

- Working directory: `C:\AutoFXV2.0` (VERIFIED empty at engagement start
  2026-08-17 and **not initially a git repository**; initialised that day).
- Branch: `planning/discovery-handoff`; this V2 repo's default branch is
  **`master`** (@ `24db4ea`), not `main`; renaming to `main` remains Jacob's
  open option (NEXT_ACTIONS B-1).
- Branch tip: `39e2730`. **Jacob CONFIRMED 2026-08-18** that he authorised
  `fcde457` (the 17-file terminal-handoff change set) and `39e2730`
  (enablement of the three D-013-approved plugins). Recovery finding F-1
  (stale "uncommitted" claims vs git reality) is RESOLVED; the stale text
  was reconciled in this session's change set.
- This session's recovery-reconciliation change set is **UNCOMMITTED**
  pending Jacob's review (proposed commit in NEXT_ACTIONS B-1). Never
  pushed; no remote exists.

## Last completed acceptance criterion

Terminal recovery audit complete (read-only; no subagents/workflows/MCP;
V1/PostgreSQL/cTrader untouched); recovered state presented and
OWNER_APPROVED by Jacob 2026-08-18; the seven authorised documentation-only
corrections applied (uncommitted, awaiting his review).

## First incomplete acceptance criterion

Jacob reviews and commits the recovery-reconciliation change set
(NEXT_ACTIONS B-1). Thereafter the single next work item is the
model-governance package (B-2, D-017): Jacob supplies the Prompt 6A
specification (Q-012), Claude creates and validates the package, and Jacob
approves it. Only after that approval: Round A batch 2 recorded and
summarised (B-3) and/or the repo-side V1 audit on Jacob's explicit go (B-5).

## Decisions captured (lifecycle · evidence)

- D-001 drawdown direction — OWNER_APPROVED 2026-08-17 · USER-STATED
  (configurable per-book cap; realised peak-relative dd canonical for
  approval; MTM + heat separate live controls; $100k/1% standard; numbers →
  Round E, Q-005).
- D-008 Jacob-only personal trading — OWNER_APPROVED · USER-STATED.
- D-009 eight CFD classes, phased FX-first, per-class Gate 1 — OWNER_APPROVED
  · USER-STATED.
- D-010 P1 full = implementation MVP; P2/P3 planning-only — OWNER_APPROVED ·
  USER-STATED.
- D-011 terminal primary workspace (Desktop = visual review/wireframes) —
  OWNER_APPROVED 2026-08-18 · USER-STATED.
- D-012 model routing (`--model best --effort ultracode`; Fable critical/
  acceptance; Opus bounded reasoning; Sonnet deterministic from approved
  specs; Haiku extraction only; uncertainty escalates upward) —
  OWNER_APPROVED · USER-STATED; launch mechanism VERIFIED 2026-08-18.
- D-013 plugin policy (three discovery plugins INSTALLED 2026-08-18, commit
  `39e2730`; data after Q-001; design at wireframe round;
  engineering/security/LSP/review after implementation authorisation;
  marketing P3; no ECC now) — OWNER_APPROVED · USER-STATED.
- D-015 environment-visible external tooling = OUT-OF-SCOPE / NOT AUTHORISED
  FOR AUTOFX USE (Figma deferred to wireframe phase; only
  TOOLING_REGISTER-approved project-scoped tools authorised) —
  OWNER_APPROVED 2026-08-18 · USER-STATED.
- D-016 handoff files exempt from six-field header rule (comply with handoff
  schemas instead) — OWNER_APPROVED 2026-08-18 · USER-STATED.
- D-017 model-governance package (per migration-runbook Prompt 6A) must be
  created, validated, and OWNER_APPROVED before Round A resumption, the V1
  audit, subagent use, or acceptance of critical discovery artifacts —
  OWNER_APPROVED 2026-08-18 · USER-STATED (spec location → Q-012).
- D-002…D-007 legacy conflicts — OPEN · CONFLICT/UNKNOWN (per entry).
- D-014 rules-file naming — recorded CONFLICT; resolution PROPOSED (Q-011).

## Agreed safety and quality principles (all recorded as requirements)

Backtest-to-live fidelity (VAL-001); closed-position peak-relative drawdown
as approval metric with MTM/heat separate (RISK-004/006, D-001); compounding
capital from closed positions (RISK-003); full-book drawdown enforcement with
flagged constituent exceptions (RISK-005); crisis validation on measured
episodes (VAL-004); news/weekend restrictions, fail-closed (EXEC-006/007,
VAL-005); real-world costs incl. bid/ask, commission, slippage, swaps
(DATA-003, VAL-002); data integrity + point-in-time correctness (DATA-004/005);
out-of-period evidence / locked holdout (QUANT-003); no live execution by
default — approved books disabled, live approval separate and version-specific
(EXEC-002). Every trade has a stop loss (EXEC-004). All USER-STATED from the
master prompt; none yet independently validated (nothing is TESTED).

## Verified evidence locations

- V1 repo `JDep8/AutoFX`: private; read-only access VERIFIED via
  authenticated `gh` (account JDep8), Python, `main`, updated 2026-07-30, 247
  tree entries. Audit **NOT STARTED** — all V1 correctness is UNKNOWN.
  Security flag: committed `101005649.rdp` at V1 root (contents never read).
- V2 workspace emptiness + git init: VERIFIED 2026-08-17 (DISCOVERY_STATUS.md
  § Verified facts).
- Scaffold completeness: VERIFIED by independent critic 2026-08-17.
- Terminal recovery audit 2026-08-18 (all VERIFIED, read-only): entire git
  history is documentation-only (every path ever committed is `.md`,
  `.gitignore`, or `.claude/settings.json`); filesystem = git index exactly
  (87 files; nothing untracked/ignored on disk); metadata-only secrets scan
  across all 5 revisions + working tree — zero value-like hits (no
  credentials, connection strings, tokens, keys); tracked-filename check
  clean; status vocabulary and headers compliant (handoffs exempt per
  D-016); gate phrase verbatim-consistent everywhere; all requirement IDs
  cited here trace to REQUIREMENTS_CATALOGUE.md and TRACEABILITY_MATRIX.md.

## Unresolved conflicts / blockers

- D-002…D-007 (legacy conflicts) — open, assigned to Rounds E–J as recorded.
- D-014/Q-011 rules naming — CONFLICT, non-blocking, Jacob to resolve.
- Q-001 (PostgreSQL read-only path) blocks DB-side V1 audit; Q-002 (cBot
  location) blocks Round J sizing decision.
- (Resolved 2026-08-18: recovery finding F-1 — Jacob confirmed authorship of
  `fcde457`/`39e2730`; stale pre-commit statements reconciled.)

## Outstanding questions (all in QUESTION_REGISTER.md)

Q-001 DB access · Q-002 cBot location · Q-003 consumer-AI automation
(BLOCKED) · Q-004 video-content boundary · Q-005 drawdown numbers (Round E) ·
Q-006 jurisdictions · Q-007 budget/horizon/team/infra · Q-008 KPIs/non-goals ·
Q-009 measurable backtest-accuracy form · Q-010 V1 holdout contamination ·
Q-011 rules naming · Q-012 Prompt 6A / model-governance specification
location (blocks D-017 package creation; fails closed until supplied).
Round A batch 2 (Q-001/002/006–009) was asked 2026-08-17
— verbatim wording in INTERVIEW_RECORD.md § Batch 2; answers pending. **Do
not re-ask; do not convert answered items back to OPEN.**

## Work in progress / exact partial state

- Recovery-reconciliation change set (this session, 2026-08-18) on branch
  `planning/discovery-handoff`, **uncommitted** pending Jacob's review.
  Files changed: `.claude/rules/documentation-and-traceability.md`,
  `docs/00-governance/DECISION_LOG.md`, `QUESTION_REGISTER.md`,
  `TOOLING_REGISTER.md`, `MODEL_ROUTING_POLICY.md`, `DOCUMENT_INDEX.md`,
  and the four `docs/handoffs/` files.
- No other partial work. No application code, schemas, migrations,
  infrastructure, or trading artefacts exist anywhere in the repo (VERIFIED
  2026-08-18 across the full history).

## Recovery Required (re-verify rather than assume; do not redo verified work)

1. ~~`--effort ultracode` launch flag~~ — **CLOSED 2026-08-18**: VERIFIED
   working (Fable 5 + Ultracode); recorded in MODEL_ROUTING_POLICY.md.
2. **Safety-material skeletons (INFERRED risk):** RISK_AND_DRAWDOWN_SPEC,
   BACKTEST_FIDELITY_SPEC, LEAKAGE_AND_HOLDOUT_POLICY,
   ORDER_AND_FILL_LIFECYCLE, CIRCUIT_BREAKERS_AND_KILL_SWITCHES were
   agent-drafted and passed one automated critic; give each a Fable re-read
   at the start of its owning round before treating its skeleton structure as
   settled. Financial-safety material.
3. **Q-010 holdout contamination (UNKNOWN, safety-material):** resolve by V1
   audit evidence + Round B, never by assumption.
4. **Glossary formulas (USER-STATED/PROPOSED):** candidate drawdown/heat
   definitions come from the master prompt; canonical sign-off is Round E.
5. **V1 `.rdp` exposure (VERIFIED risk, owner action):** rotate any
   credentials it may embed; removal from V1 history at Jacob's discretion.

## Single first safe next action

Wait for Jacob's review/commit of the reconciliation change set (B-1). The
single first safe next action after that commit is creation and validation
of the project-local model-governance package per Prompt 6A (B-2, D-017) —
blocked until Jacob supplies the Prompt 6A specification (Q-012). Round A
and the V1 audit follow only after the package is OWNER_APPROVED. Open no
new discovery work and use no subagents until then (owner instructions
2026-08-18).
