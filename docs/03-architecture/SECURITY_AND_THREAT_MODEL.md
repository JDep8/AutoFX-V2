# Security and Threat Model

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [SYSTEM_CONTEXT.md](SYSTEM_CONTEXT.md), [LOGICAL_ARCHITECTURE.md](LOGICAL_ARCHITECTURE.md), [INTEGRATION_CONTRACTS.md](INTEGRATION_CONTRACTS.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md)
- **Approval evidence:** None yet

## Purpose

This document will specify how AutoFX V2 protects credentials, capital,
and evidence integrity before any implementation starts, satisfying
SEC-003's requirement that security is specified pre-build. It covers
environments, secrets, identity, encryption, audit, supply chain, and a
threat model scoped to a single-operator personal-capital system (D-008).
Owner approval of this document is an Exit Review condition (SEC-003).

## Scope and decisions this document will own

- Environment separation rules and what each environment may access.
- Infrastructure-as-code, secrets-management, and identity/RBAC policy.
- Least-privilege, encryption, and audit-logging requirements.
- Supply-chain security and dependency policy.
- The threat model: assets, adversaries, attack surfaces, mitigations, and
  accepted residual risks.
- It does not own per-interface security detail (contract entries in
  [INTEGRATION_CONTRACTS.md](INTEGRATION_CONTRACTS.md)) or live trading
  operational runbooks (OPS-001, Round J/N documents).

## Structure skeleton

### 1. Assets and trust boundaries

Will enumerate what must be protected: broker credentials and API tokens,
trading accounts and capital, market/news data licences, research and
evidence integrity (tampering with evidence is a safety issue, BUS-003),
and the audit trail (FR-004). Trust boundaries follow
[SYSTEM_CONTEXT.md](SYSTEM_CONTEXT.md). Round N.

### 2. Environments and separation

Will define the environment set, promotion rules, and which environments
may hold live credentials or reach the broker — aligned with the
shadow/paper/live promotion path (Gates 6–7). Round N, with Round J for
live-environment specifics.

### 3. Infrastructure as code and configuration control

Will decide the IaC approach, configuration versioning, and how
environment drift is detected — supporting deterministic reproducibility
(VAL-003). Tooling choice is open. Round N (ADR).

### 4. Secrets management

Will define where secrets live, how they rotate, and how the SEC-001
absolute rule (never exposed, never committed, never read into output) is
enforced technically, not just procedurally. Technology open. Round N.

### 5. Identity, RBAC, and least privilege

Will define identities (human and service), role separation, and
least-privilege grants. Single human user (D-008) does not remove the need
for separated service identities — e.g. research identities must have no
write-path to live configuration (RES-003). Round N.

### 6. Encryption

Will state encryption requirements at rest and in transit per data class.
No algorithms or key-management products are selected here. Round N.

### 7. Audit logging

Will define what is audit-logged, tamper-evidence expectations, and
retention — complementing the trade ledger (FR-004) with security events.
Round N, with Round K for ledger overlap.

### 8. Supply-chain security and dependency policy

Will define dependency vetting, pinning, update cadence policy, and
provenance checks — noting the no-build gate forbids installing
dependencies before authorisation (CLAUDE.md). Round N.

### 9. Threat model

Will apply a structured method (method choice itself a Round N decision)
to the P1 attack surfaces: broker session hijack or credential theft,
data-poisoning of research inputs, tampering with approval or evidence
records, unauthorised activation of a disabled book (EXEC-002), and
unreachable kill switches (EXEC-010, D-006). D-008 scopes the model:
threat actors are external plus compromised tooling, not malicious
internal users. Round N.

### 10. Discovery-phase controls (already in force)

Will restate the controls active now: read-only bounded V1 database access
(SEC-002, Q-001 → D-022 access model), no secrets in output or commits (SEC-001), and
documentation-only commits. These are policy statements, not evidence of
testing.

## Known inputs

- SEC-001: no credentials, tokens, account identifiers, or private data
  exposed or committed — anywhere, ever (`PROPOSED`, absolute rule in
  force).
- SEC-002: discovery database access is read-only and bounded (Q-001 →
  D-022: V1 permanently read-only via `autofx_v1_readonly`; provisioning
  pending). D-022 also fixes the six-role least-privilege separation and
  credential-isolation safeguards this document will elaborate (SEC-004,
  SEC-005).
- SEC-003: this document must be owner-approved before implementation.
- D-008 (`OWNER_APPROVED`): single user; no multi-tenancy; threat model
  scoped accordingly.
- EXEC-002/EXEC-010: disabled-by-default approvals and demonstrably
  reachable kill switches are security-relevant invariants.
- RES-003: no write-path from research output to live configuration.

## Open questions

- Hosting model and therefore the physical/provider trust boundary? →
  Round N.
- Secrets-management, IaC, and identity tooling selections? → Round N
  (ADRs).
- Environment count and which hold live credentials? → Round N (Round J
  for live).
- Threat-modelling method and the accepted-residual-risk register format?
  → Round N.
- Audit-log retention and tamper-evidence mechanism? → Rounds K/N.
- Dependency policy specifics (vetting depth, pinning, update cadence)? →
  Round N.
- Does the content business (P3) change the exposure surface (public
  publishing, brand impersonation), and when is that assessed? → Round M
  (D-008 notes separate assessment).
