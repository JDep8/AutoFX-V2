# Current State

- **Owner:** Jacob Depares
- **Status:** Living handoff (refreshed every checkpoint)
- **Date/time:** 2026-08-18 05:17 UTC
- **Source session:** second terminal session (Claude Code CLI, Fable 5 +
  Ultracode), continued — Round A closure-assurance pass (owner-directed):
  completion assessment, KPI framework proposal, repository-wide
  reconciliation, visibility verification, Rounds B–O assurance matrix,
  coverage check. Earlier in the same session: batch 2 recording +
  D-018…D-024 + D-024 execution. History: SESSION_LOG.md.

## Phase, round, gate

- Phase 0: COMPLETE 2026-08-17. Phase 1 (V1 forensic assessment): NOT
  STARTED — gated on Jacob's explicit go (NEXT_ACTIONS § B); DB depth also
  needs D-022 role provisioning; bridge target known (D-023).
- Round A: batches 1+2 answered; **Round A NOT closed** (owner direction
  2026-08-18). Completion assessment (DISCOVERY_STATUS.md): 11 of 13
  required topics COMPLETE or COMPLETE FOR ROUND A; **2 INCOMPLETE** —
  success hierarchy (Q-015) and KPI-framework approval (Q-008 remainder).
  Round A summary remains `PROPOSED`; the KPI framework (PROJECT_CHARTER.md)
  and completion assessment are `PROPOSED`; Jacob has explicitly **not yet**
  approved any of them.
- **No-build gate: ACTIVE.** `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE
  <number/name>` not given; `AUTHORISE WIREFRAME ONLY` not given.
- Governor routing: closure-assurance pass classified CRITICAL; main Fable
  session + one bounded autofx-opus-reviewer challenge (owner-permitted);
  no dynamic workflow. Recorded in MODEL_ROUTING_POLICY.md § Critical
  routing record.

## Session configuration (D-012)

- VERIFIED this session: Fable 5 (`claude-fable-5`) + Ultracode.

## Working directory / git

- Working directory `C:\AutoFXV2.0`; branch `planning/discovery-handoff`
  tracking `origin/planning/discovery-handoff`; remote `origin` =
  https://github.com/JDep8/AutoFX-V2; local `main` @ `ad1d1e4` = remote
  `main` (not advanced — no merge to main without Jacob's approval).
- **Repository visibility: PUBLIC** — VERIFIED 2026-08-18 (`isPrivate:
  false`); changed by Jacob after the private creation (that earlier
  evidence was accurate at its time). Owner decision pending: Q-014
  (temporary or permanent). Implications recorded in TOOLING_REGISTER.md
  § Repository visibility. Claude does not change visibility.
- This checkpoint commits the closure-assurance change set (≈25 documents:
  reconciliation of stale Round A references, charter rewrite with KPI
  framework, DISCOVERY_STATUS assessment + B–O matrix + coverage check,
  Q-014/Q-015, visibility record, routing record, handoffs) and pushes
  `planning/discovery-handoff` only.

## Command governance (2026-08-18, later in Session 5)

Owner-directed Claude Code command-governance research completed:
CLAUDE_CODE_COMMAND_RUNBOOK.md created (`PROPOSED`, v0.1.0) — catalogue
verified against v2.1.234 (official docs + read-only local verification;
no mutating command exercised), per-command AutoFX policies for the 45
owner-mandated commands with all owner-specified safeguards, ten session
sequences, upgrade revalidation procedure. Approval pending
(NEXT_ACTIONS § B-7); until approved, the most conservative reading
applies. TOOLING_REGISTER § Claude Code command governance added.

## Last completed acceptance criterion

Round A closure-assurance pass persisted: 16-row completion assessment
(verdict: may NOT close; 3 rows INCOMPLETE — Topics 1/3 share Q-015, Topic
12 = KPI approval); 20-KPI framework `PROPOSED` (form-level; acceptance
thresholds owned by Rounds D–N; KPI-10 carries owner-set D-019 numbers;
remaining numerics are itemised zero-/100%-tolerance restatements of
standing hard constraints); repository-wide stale-reference reconciliation
(~25 documents corrected incl. the 08-content folder, history preserved);
PUBLIC visibility verified and recorded (Q-014, CONFLICT vs D-024 PRIVATE
clause); Rounds B–O assurance matrix + full-scope coverage check
(`PROPOSED`) in DISCOVERY_STATUS.md; independent challenge review
(autofx-opus-reviewer) returned 38 findings — all dispositioned before
commit, Q-016 raised (SESSION_LOG.md Session 5 continued).

## First incomplete acceptance criterion

Jacob answers the four Round A closure questions (success hierarchy Q-015;
KPI framework approval; Q-014 visibility; deferral-map/assessment
confirmation) and then approves (or amends) the Round A summary — only that
closes Round A.

## Open owner decisions / blockers

- Q-015 success hierarchy; Q-008 remainder (KPI framework approval); Q-014
  repository visibility; Round A summary approval.
- D-022 role provisioning (blocks DB-side audit depth); explicit V1-audit
  go (blocks Phase 1 start).
- Q-003 BLOCKED (legal); Q-004, Q-005 (Round E), Q-010 (safety-material,
  Round B/H), Q-011, Q-013 open; Q-016 CONFLICT recorded (G/H artefact
  ownership — `PROPOSED` resolution awaiting Jacob, at latest when Round G
  opens).
- D-002…D-007 legacy conflicts open, assigned to Rounds E–J.

## Work in progress / exact partial state

- None after this checkpoint. All closure-assurance outputs are persisted
  in the repository (charter, DISCOVERY_STATUS, registers); nothing lives
  only in chat.
- Round A summary, KPI framework, completion assessment, B–O matrix, and
  coverage check: all `PROPOSED`, awaiting Jacob.
- No application code, schemas, migrations, infrastructure, or trading
  artefacts exist anywhere in the repo. V1 untouched.

## Recovery Required (re-verify rather than assume; do not redo verified work)

1. **Safety-material skeletons (INFERRED risk):** RISK_AND_DRAWDOWN_SPEC,
   BACKTEST_FIDELITY_SPEC, LEAKAGE_AND_HOLDOUT_POLICY,
   ORDER_AND_FILL_LIFECYCLE, CIRCUIT_BREAKERS_AND_KILL_SWITCHES — Fable
   re-read at the start of each owning round (now also recorded in the B–O
   matrix entries for Rounds E/F/H/J).
2. **Q-010 holdout contamination (UNKNOWN, safety-material):** V1 audit +
   Round B evidence only; fail closed if absent.
3. **Glossary formulas (USER-STATED/PROPOSED):** canonical sign-off Round E.
4. **V1 `.rdp` exposure (VERIFIED risk, owner action):** rotate any embedded
   credentials; removal from V1 history at Jacob's discretion.
5. **Repository visibility (PUBLIC, Q-014 pending):** until Jacob decides,
   treat sensitive-material placement as a standing consideration for every
   new document; never assume the repo is private.

## Single first safe next action

Wait for Jacob's answers to the four Round A closure questions (chat +
NEXT_ACTIONS § B), then record them and, if he approves, close Round A.
Open no new discovery work unprompted; V1 audit waits for his explicit go;
delegation and critical acceptance route through the `autofx-model-governor`
skill.
