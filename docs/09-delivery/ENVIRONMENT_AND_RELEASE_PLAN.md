# Environment and Release Plan
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [SECURITY_AND_THREAT_MODEL.md](../03-architecture/SECURITY_AND_THREAT_MODEL.md), [CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](../06-execution-and-risk/CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md), [INCIDENT_AND_RECOVERY_RUNBOOK.md](../06-execution-and-risk/INCIDENT_AND_RECOVERY_RUNBOOK.md), [TEST_AND_EVIDENCE_STRATEGY.md](./TEST_AND_EVIDENCE_STRATEGY.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (EXEC-002, EXEC-010, SEC-003, OPS-001, UX-001)
- **Approval evidence:** None yet

## Purpose

This document defines the environments AutoFX V2 will run in, how demo and
live are kept strictly separate, and the release gates a change must pass to
move between them. Its central safety principle: initial live exposure is
staged and small — the system never targets full scale on day one. All
infrastructure decisions here are planning only; nothing is provisioned or
deployed before the explicit implementation authorisation.

## Scope and decisions this document will own

- The environment inventory and promotion path.
- Demo/live separation rules (credentials, configuration, visual identity).
- Release gates for code and configuration changes, aligned to Gates 5–8.
- The staged initial live-exposure ramp structure (numbers set by Jacob at
  Gate 7, not invented here).
- Infrastructure-as-code and secrets-management approach.
- Out of scope: threat model and RBAC detail
  ([SECURITY_AND_THREAT_MODEL.md](../03-architecture/SECURITY_AND_THREAT_MODEL.md));
  runtime breakers ([CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](../06-execution-and-risk/CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md)).

## Structure skeleton

### 1. Environment inventory and promotion path
Which environments exist (development, test/replay, shadow/paper, live —
final list to be confirmed), what each may and may not connect to, and the
promotion order between them. Decided in Round N; nothing may connect an
execution process to a demo or live account before authorisation
(no-build gate).

### 2. Demo/live separation
Hard separation of credentials, accounts, configuration, and data paths
between demo and live, plus the requirement that the active environment is
impossible to overlook in the UI (UX-001). Mechanisms decided in Rounds J/N;
multi-account handling per FR-005.

### 3. Release gates for changes
What evidence a code or configuration change needs before promotion:
mapping to Gates 5 (approved-but-disabled), 6 (shadow/paper), 7 (live, with
separate explicit approval), and 8 (ongoing review). Live-marking is
separate from book approval and version-specific (EXEC-002, FR-001).
Gate mechanics live in
[TEST_AND_EVIDENCE_STRATEGY.md](./TEST_AND_EVIDENCE_STRATEGY.md); this
section owns the release procedure around them.

### 4. Staged initial live exposure
The ramp structure for first live trading: start deliberately below target
exposure, expand only on evidence, **never target scale on day one**. Gate 7
requires the ramp itself to be owner-approved, alongside verified caps, kill
switches, stop protection, and named ops ownership. Ramp step definitions
and criteria are set by Jacob in Rounds J/N; no ramp numbers are proposed
here.

### 5. Infrastructure-as-code
Whether and how environments are defined as code, so a rebuild is
reproducible and auditable. Approach, tooling, and repository layout are
pending Round N; ties to OPS-002 (disaster rebuild) in
[BACKUP_RECOVERY_AND_REBUILD.md](../04-data/BACKUP_RECOVERY_AND_REBUILD.md).

### 6. Secrets and access management
Where credentials live, how they reach runtime, and how they never reach the
repository or chat (SEC-001). Design pending Round N under SEC-003; the
standing rule from `.claude/rules/security-and-secrets.md` applies during
discovery already.

### 7. Rollback, safe state, and incident hooks
How a bad release is withdrawn, what the safe state is for a live trading
system (fail closed: no new entries, controlled-exit policy), and how the
release process links to OPS-001 incident response. Defined in Rounds J/N
with the incident runbook.

## Known inputs

- No-build gate: no deployment, provisioning, or broker connection of any
  kind before `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>`
  (CLAUDE.md).
- EXEC-002: approved books are disabled by default; live-marking is separate
  and version-specific.
- EXEC-010 / D-006: kill switches and breakers must be demonstrably reachable
  before live approval — a release precondition, not an afterthought.
- SEC-003: environments, secrets, RBAC, least privilege specified before
  implementation — `PROPOSED`, Round N.
- OPS-001: incident runbook exercised before live (Gate 7).
- UX-001: environment and kill-switch state always visible.
- RISK-008: USD accounts initially; the environment design must not block the
  documented multi-currency path.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Final environment list and hosting location | Round N (constrained by Q-007) |
| Infrastructure-as-code tooling and repo layout | Round N |
| Secrets-management mechanism | Round N (SEC-003) |
| Staged-ramp step structure and progression criteria | Rounds J/N, approved at Gate 7 |
| Demo/live credential and account separation mechanics | Rounds J/N |
| Rollback and safe-state procedure detail | Rounds J/N with INCIDENT_AND_RECOVERY_RUNBOOK.md |
