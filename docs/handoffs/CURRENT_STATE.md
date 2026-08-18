# Current State

- **Owner:** Jacob Depares
- **Status:** Living handoff (refreshed every checkpoint)
- **Date/time:** 2026-08-18 06:08 UTC
- **Source session:** second terminal session (Fable 5 + Ultracode),
  continued — Round A decision reconciliation (D-025…D-035), trading
  simulation & certification requirement (D-034), command-runbook
  correction pass (D-035). Earlier same session: batch 2 recording,
  D-024 execution, closure-assurance pass, runbook v0.1.0. History:
  SESSION_LOG.md.

## Phase, round, gate

- Phase 0: COMPLETE 2026-08-17. Phase 1 (V1 forensic assessment): NOT
  STARTED — gated on Jacob's explicit go; DB-side depth additionally
  needs `autofx_v1_readonly` provisioning (D-022 — blocks the DB-side
  audit only, per Jacob's 2026-08-18 confirmation).
- Round A: all required topics now COMPLETE or COMPLETE FOR ROUND A
  (completion assessment, DISCOVERY_STATUS.md). **The single remaining
  closure step is Jacob's approval of the Round A closure candidate**
  (INTERVIEW_RECORD.md § Round A closure candidate). Round A is NOT
  closed; Round B not started.
- **No-build gate: ACTIVE.** `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE
  <number/name>` not given; `AUTHORISE WIREFRAME ONLY` not given. D-034
  simulation modes are specified, not authorised to run.
- Standing rules now in force (2026-08-18): **D-025** owner decisions one
  at a time ("noted" ≠ "approved"); **D-026** every substantive task's
  output persists in the repository, ends with validation + commit + push
  to the approved branch.

## Session configuration (D-012)

- VERIFIED this session: Fable 5 (`claude-fable-5`) + Ultracode; Claude
  Code 2.1.234.

## Working directory / git

- `C:\AutoFXV2.0`; branch `planning/discovery-handoff` tracking origin;
  remote https://github.com/JDep8/AutoFX-V2; local `main` @ `ad1d1e4` =
  remote (untouched). Base at this task's start: `2e19d9b`, tree clean.
- **Visibility: PUBLIC by owner decision D-033 (Q-014 resolved):**
  temporarily public for independent ChatGPT review; returns to private
  when an authenticated review path exists and Jacob explicitly
  authorises; sensitivity stop-rule applies before every push; D-024's
  other git controls unchanged (no main merges, no force-push, approved
  branches only).

## Last completed acceptance criterion

Round A reconciliation change set persisted: D-025…D-035 recorded with
confirmation notes on D-014/D-018/D-021/D-022/D-024; Q-008 completed and
Q-011/Q-013/Q-014/Q-015/Q-016 resolved; PROJECT_CHARTER updated
(co-equal hierarchy D-027; KPI framework `OWNER_APPROVED` form level
D-028, 22 areas headline/supporting incl. KPI-21/22);
TRADING_SIMULATION_AND_CERTIFICATION_SPEC.md created (D-034, P1;
EXEC-012…014, VAL-008); command runbook corrected to v0.2.0 against the
full 105-row official catalogue with errata (v0.1.0 REJECTED, D-035);
rules files updated (D-025/026/031/032); registers, index, matrix,
DISCOVERY_STATUS (assessment now closable pending approval), and
handoffs reconciled; validation + independent read-only consistency
check run before commit (SESSION_LOG.md).

## First incomplete acceptance criterion

Jacob approves (or amends) the **Round A closure candidate**
(INTERVIEW_RECORD.md) — the only remaining Round A step. Separately
queued one-at-a-time items: corrected command-runbook policies (D-035);
`autofx_v1_readonly` provisioning; explicit V1-audit go.

## Open owner decisions / blockers

- Round A closure candidate approval (the next single question).
- Command-runbook v0.2.0 policy approval — one at a time per D-025
  (B-7 remains NOT approved; conservative reading applies meanwhile).
- `autofx_v1_readonly` provisioning (blocks DB-side audit depth only).
- Explicit V1-audit go (repo-side; blocks Phase 1 start).
- Q-003 BLOCKED (legal); Q-004 (Round L); Q-005 (Round E); Q-010
  (safety-material; V1 audit + Round B).
- D-002…D-007 legacy conflicts open, assigned Rounds E–J.
- Optional: extend committed settings allowlist (NEXT_ACTIONS § B).

## Work in progress / exact partial state

- None after this checkpoint; all outputs persisted and pushed. Round A
  closure candidate, corrected runbook, simulation spec design details:
  all `PROPOSED`, awaiting Jacob.
- No application code, schemas, migrations, infrastructure, or trading
  artefacts exist anywhere in the repo. V1 untouched. No V1 audit
  started. No loop/goal/schedule/workflow running.

## Recovery Required (re-verify rather than assume)

1. Safety-material skeletons (RISK_AND_DRAWDOWN_SPEC,
   BACKTEST_FIDELITY_SPEC, LEAKAGE_AND_HOLDOUT_POLICY,
   ORDER_AND_FILL_LIFECYCLE, CIRCUIT_BREAKERS_AND_KILL_SWITCHES, and now
   TRADING_SIMULATION_AND_CERTIFICATION_SPEC's Claude-proposed design
   sections) — Fable re-read at each owning round's start.
2. Q-010 holdout contamination (UNKNOWN, safety-material) — V1 audit +
   Round B evidence only; fail closed.
3. Glossary formulas — canonical sign-off Round E.
4. V1 `.rdp` exposure — owner action (rotate/remove at his discretion).
5. Visibility sensitivity stop-rule (D-033): before every push, ask
   whether new content would expose security detail, credentials,
   strategy IP, or legally sensitive material publicly — stop and raise
   one owner decision if so.

## Single first safe next action

Ask Jacob the single closure question (approve/amend the Round A closure
candidate), per D-025 one at a time. Then, on approval: close Round A in
the registers. Open no new discovery work unprompted; V1 audit waits for
his explicit go; delegation and critical acceptance route through the
`autofx-model-governor`.
