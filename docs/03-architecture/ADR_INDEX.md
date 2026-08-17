# ADR Index

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [LOGICAL_ARCHITECTURE.md](LOGICAL_ARCHITECTURE.md), [../00-governance/DECISION_LOG.md](../00-governance/DECISION_LOG.md)
- **Approval evidence:** None yet

## Purpose

Architecture Decision Records (ADRs) capture significant, hard-to-reverse
technical choices with their evidence and alternatives, so future work can see
*why* the architecture is shaped as it is. The Decision Log owns product and
governance decisions; ADRs own technical ones. Build-versus-buy choices are
recorded here too.

## ADR template (mandatory structure)

Every ADR uses the review structure from
[.claude/rules/documentation-and-traceability.md](../../.claude/rules/documentation-and-traceability.md):

1. Objective
2. Current problem / evidence
3. Proposed design
4. Alternatives considered
5. Implementation concept
6. Benefits
7. Risks / failure modes
8. Dependencies
9. Acceptance evidence
10. Unresolved owner decisions

ADR statuses use the approved vocabulary only. An ADR affecting leakage,
holdout integrity, risk, drawdown, sizing, live safety, or compliance needs
Jacob's explicit approval before it is `OWNER_APPROVED`.

## Index

| ADR | Title | Status | Decision refs | Notes |
|-----|-------|--------|---------------|-------|
| *(none yet)* | — | — | — | First ADRs expected from Round N (hosting, PostgreSQL strategy, queues/workflows, object/analytical storage, observability) and Round J (execution engine placement) |

## Known upcoming ADR subjects (from the mandate — not yet decided)

- Hosting, OS, and language strategy → Round N (Q-007 constrains)
- PostgreSQL strategy; queues/workflows; object + analytical storage → Round N
- Observability stack → Round N
- One deterministic execution lifecycle shared across backtest/replay/paper/live → Round F
- Authoritative sizing engine: AutoFX vs cBot → Round J (EXEC-008, Q-002)
- Build-versus-buy per subsystem → Round N

## Open questions

- ADR numbering/versioning conventions and review cadence → Round N.
