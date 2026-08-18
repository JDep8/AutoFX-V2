# Current State

- **Owner:** Jacob Depares
- **Status:** Living handoff (refreshed every checkpoint)
- **Date/time:** 2026-08-18 11:18 UTC
- **Source session:** second terminal session (Fable 5 + Ultracode),
  continued — Round A CLOSED (D-036); D-037 roadmap + private Project #1
  live; **repository-side V1 forensic audit PERFORMED (Issue #21).**
  History: SESSION_LOG.md.

## Phase, round, gate

- Phase 0: COMPLETE 2026-08-17. **Phase 1 (V1 forensic assessment):
  REPO-SIDE COMPLETE 2026-08-18** (Issue #21, owner-authorised; read-only;
  V1 untouched; no code copied). DB-side deferred — needs
  `autofx_v1_readonly` provisioning (D-022). Findings: V1_AUDIT.md +
  V1_REUSE_REGISTER.md; Q-010 answered (no untouched V1 holdout); no
  validated V1 profitability evidence found.
- **Round A: CLOSED — `OWNER_APPROVED` 2026-08-18 (D-036, evidence
  USER-STATED).** Closure candidate approved as written; deferred matters
  keep their assigned rounds. Round B NOT started.
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

## Roadmap surface (D-037, executed 2026-08-18)

- 52 issue-backed cards (#1–#52) + 21 labels live on `JDep8/AutoFX-V2`;
  idea template committed; inventory in
  docs/09-delivery/GITHUB_PROJECT_REGISTER.md; rules in
  GITHUB_PROJECT_OPERATING_MODEL.md. No card is Ready/In Progress; cards
  never authorise work.
- GitHub Project **#1 "AutoFX V2 — Project Roadmap"** created 2026-08-18
  (Jacob granted the `project` scope): **PRIVATE (VERIFIED)**, linked,
  11 fields, 52/52 items populated —
  https://github.com/users/JDep8/projects/1. Only the ten saved views
  remain a manual UI step (register § Views).
- Standing D-037 rule active: every substantive prompt reconciles
  repository ↔ roadmap and reports drift.

## Last completed acceptance criterion

Round A closed across every register (D-036); D-037 roadmap executed to
the limit of current `gh` scopes: 21 labels + 52 evidence-based issue
cards created (zero duplicates — repo had no issues), idea template
committed, operating model + register written, DELIVERY_ROADMAP/
TOOLING_REGISTER/DOCUMENT_INDEX/rules/CLAUDE.md pointers updated;
validation + secret/sensitivity checks run before commit
(SESSION_LOG.md).

## First incomplete acceptance criterion

Next one-at-a-time owner items (any order Jacob chooses): command-runbook
v0.2.0 policy approval (issue #19); `autofx_v1_readonly` provisioning
(issue #20); explicit repo-side V1-audit go (issue #21). Optional UI-only:
create the ten Project views (register § Views).

## Open owner decisions / blockers

- Command-runbook v0.2.0 policy approval — one at a time per D-025
  (issue #19; NOT approved; conservative reading applies meanwhile).
- `autofx_v1_readonly` provisioning (issue #20; blocks DB-side audit
  depth only).
- Explicit V1-audit go (issue #21; repo-side; blocks Phase 1 start).
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

Wait for Jacob's next one-at-a-time input: open Round B (V1 outcomes /
migration stance — evidence base now ready in V1_AUDIT.md); or any of the
ten V1-audit escalations; or runbook policy approvals (#19); or
`autofx_v1_readonly` provisioning (#20, unblocks the DB-side V1 audit).
Open no new discovery work unprompted; **Round B NOT started** (only its
evidence exists); delegation and critical acceptance route through the
`autofx-model-governor`; D-037 roadmap reconciliation applies to every
substantive task.
