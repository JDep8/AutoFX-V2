# Incident and Recovery Runbook

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md), [BROKER_RECONCILIATION.md](BROKER_RECONCILIATION.md), [RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (OPS-001, OPS-003)
- **Approval evidence:** None yet

## Purpose

This document will be the operational playbook for when live trading goes
wrong: how an incident is declared, what the safe state is, how a human
intervenes, and under what conditions trading restarts. It complements the
automatic controls in
[CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md)
with human procedures. Per OPS-001, this runbook must be exercised before any
live approval (Gate 7).

## Scope and decisions this document will own

- Incident definition, declaration, and severity classification.
- The safe-state definition and how it is reached from any failure.
- Manual intervention procedures, permissions, and audit requirements.
- Restart preconditions and procedures.
- Post-incident review and the drill programme.

Out of scope: automatic trip conditions (owned by the breakers document);
data-platform backup and rebuild
([BACKUP_RECOVERY_AND_REBUILD.md](../04-data/BACKUP_RECOVERY_AND_REBUILD.md)).

## Structure skeleton

### 1. Incident definition and declaration
What counts as an incident (breaker trip, unresolved reconciliation
discrepancy, unprotected position, unexplained loss, infrastructure failure),
who declares it, and how declaration is recorded. Criteria defined in Rounds
J/N.

### 2. Severity classification
Severity levels and the response each mandates. Level definitions are Round
J/N owner decisions — none are invented here.

### 3. Safe-state definition
The precise state the system drives to on failure: which scopes halt, what
happens to open positions (fail closed: no new entries; controlled-exit policy
per Glossary), what keeps running (monitoring, reconciliation, logging).
Defined in Rounds E/J.

### 4. Manual intervention procedures
Step-by-step procedures for the interventions Jacob may need: activate a kill
switch at any scope, close a position manually, clear a breaker, correct
internal state after broker-truth adoption. Each intervention's permission
model follows the emergency-ownership decision in
[RISK_AND_DRAWDOWN_SPEC.md](RISK_AND_DRAWDOWN_SPEC.md) section 9 (Round E);
procedures drafted in Rounds J/N.

### 5. Audit trail
What every incident and intervention must record: who, what, when, why,
system state before/after, and linkage to affected trade-ledger entries
(FR-004). Requirements defined in Rounds K/N.

### 6. Restart procedure
Ordered preconditions before trading resumes: cause identified, reconciliation
clean, breaker conditions cleared, restart authorised by the designated owner,
evidence recorded. Restart authority defers to
[CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md)
section 5. Procedure drafted in Rounds J/N.

### 7. Recovery scenarios
Named scenarios with expected recovery paths: broker disconnect mid-trade,
AutoFX process crash with open positions, stale data during open positions,
partial-account failure during fan-out, orphaned position discovered. Each
scenario maps to the specs that own its mechanics. Drafted in Round J/N.

### 8. Post-incident review
Template and timing for reviewing every incident: cause, response quality,
control gaps, follow-up actions into the question/decision registers. Defined
in Round N.

### 9. Drill programme
Which scenarios are rehearsed before live approval and how the runbook
exercise required by OPS-001 (Gate 7) is evidenced. Drill design in Round N;
execution only after implementation authorisation.

## Known inputs

- OPS-001: production observability, alerting, incident response, and
  safe-state/restart rules are required; the runbook is exercised before live
  (Gate 7).
- OPS-003: failure recovery and resumability for all long-running jobs.
- EXEC-010: kill switches must be demonstrably reachable — this runbook's
  interventions depend on that reachability.
- EXEC-009: broker truth is authoritative — recovery always begins from broker
  state.
- Fail-closed rule (Glossary): ambiguous safety-relevant state means no new
  entries and controlled-exit handling.

## Open questions

- Incident criteria and severity levels → Rounds J/N owner decisions.
- Safe-state treatment of open positions per scenario (hold protected vs
  controlled exit) → Rounds E/J.
- Alerting channels and acknowledgement expectations → Round N (with
  observability decisions under OPS-001).
- Audit-trail storage, immutability, and retention → Rounds K/N (shared with
  the trade-ledger decisions in
  [ORDER_AND_FILL_LIFECYCLE.md](ORDER_AND_FILL_LIFECYCLE.md) section 10).
- Drill list and pass criteria for Gate 7 → Round N.
