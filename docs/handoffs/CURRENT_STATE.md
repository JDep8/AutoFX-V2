# Current State

- **Owner:** Jacob Depares
- **Status:** Living handoff (refreshed every checkpoint)
- **Date/time:** 2026-08-18 00:38 UTC
- **Source session:** Claude Desktop (Claude Code Desktop app), session
  `69191095-a774-454b-918a-03be09b74d4a` — the Desktop→terminal handoff
  session. Prior history: two Desktop sessions, 2026-08-17/18 (SESSION_LOG.md).

## Phase, round, gate

- Phase 0 (discovery repository scaffold): **COMPLETE 2026-08-17** (VERIFIED —
  completeness critic: 53 domain skeletons, 0 missing/violations/overclaims).
- Round A: IN PROGRESS — batch 1 answered; batch 2 asked 2026-08-17, **no
  answers yet** (VERIFIED against INTERVIEW_RECORD.md).
- **No-build gate: ACTIVE.** The exact authorisation phrase is
  `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>` and has NOT been
  given. Wireframe gate `AUTHORISE WIREFRAME ONLY` also not given.

## Working directory / git

- Working directory: `C:\AutoFXV2.0` (VERIFIED empty at engagement start
  2026-08-17 and **not initially a git repository**; initialised that day).
- Branch: `planning/discovery-handoff` (VERIFIED via `git branch -a`; created
  2026-08-18 off `master` — this V2 repo's default branch is **`master`**, not
  `main`; renaming to `main` is Jacob's option, noted in NEXT_ACTIONS.md B-1).
- Last commit: `24db4ea` (tip of `master`; durability checkpoint 2026-08-18,
  VERIFIED). Handoff
  changes are **uncommitted by owner instruction** — Jacob reviews and commits
  (proposed command in NEXT_ACTIONS.md). Never pushed; no remote exists.

## Last completed acceptance criterion

Phase 0 scaffold complete and verified; discovery state durably written and
committed through `24db4ea` (VERIFIED).

## First incomplete acceptance criterion

Round A batch 2 answers recorded verbatim in INTERVIEW_RECORD.md with all
registers updated and a Round A domain summary produced for Jacob's approval.

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
  OWNER_APPROVED · USER-STATED.
- D-013 plugin policy (now: product-management, claude-md-management,
  session-report; data after Q-001; design at wireframe round;
  engineering/security/LSP/review after implementation authorisation;
  marketing P3; no ECC now) — OWNER_APPROVED · USER-STATED.
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

## Unresolved conflicts / blockers

- D-002…D-007 (legacy conflicts) — open, assigned to Rounds E–J as recorded.
- D-014/Q-011 rules naming — CONFLICT, non-blocking, Jacob to resolve.
- Q-001 (PostgreSQL read-only path) blocks DB-side V1 audit; Q-002 (cBot
  location) blocks Round J sizing decision.

## Outstanding questions (all in QUESTION_REGISTER.md)

Q-001 DB access · Q-002 cBot location · Q-003 consumer-AI automation
(BLOCKED) · Q-004 video-content boundary · Q-005 drawdown numbers (Round E) ·
Q-006 jurisdictions · Q-007 budget/horizon/team/infra · Q-008 KPIs/non-goals ·
Q-009 measurable backtest-accuracy form · Q-010 V1 holdout contamination ·
Q-011 rules naming. Round A batch 2 (Q-001/002/006–009) was asked 2026-08-17
— verbatim wording in INTERVIEW_RECORD.md § Batch 2; answers pending. **Do
not re-ask; do not convert answered items back to OPEN.**

## Work in progress / exact partial state

- Terminal-handoff documentation (this change set) on branch
  `planning/discovery-handoff`, **uncommitted** pending Jacob's review.
- No other partial work. No application code, schemas, migrations,
  infrastructure, or trading artefacts exist anywhere in the repo (VERIFIED).

## Recovery Required (re-verify rather than assume; do not redo verified work)

1. **`--effort ultracode` launch flag (UNKNOWN):** verify once in the first
   terminal session via `/status` and `/effort`; if unsupported, record the
   actual mechanism in MODEL_ROUTING_POLICY.md. Material to D-012 compliance.
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

In the terminal: run the recovery audit prescribed in RESUME_PROMPT.md (read
source-of-truth files, verify git state, restate the gate) and present the
recovered state to Jacob for approval — **then stop until he approves**.
