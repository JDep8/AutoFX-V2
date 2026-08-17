# Work Breakdown and Dependencies
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DELIVERY_ROADMAP.md](./DELIVERY_ROADMAP.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-009, D-010), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-001, Q-002, Q-007), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [V1_AUDIT.md](../01-discovery/V1_AUDIT.md)
- **Approval evidence:** None yet

## Purpose

This document breaks the roadmap into named work packages, records which
package depends on which, and identifies the critical path — the chain of
work that determines the earliest honest delivery of the P1 MVP. It also
records who does the work and what capability is assumed. Almost all of its
content is pending Rounds B–O, because each round defines the specifications
the work packages implement.

## Scope and decisions this document will own

- The work-package register: naming, sizing discipline (ranges only), owner,
  status, and traceability to requirement IDs.
- The dependency graph across discovery, specification, and (post-
  authorisation) implementation packages.
- The critical-path analysis and where it can be shortened without weakening
  evidence or safety standards (BUS-003 forbids shortening by weakening).
- Staffing and capability assumptions.
- Out of scope: stage sequencing and roadmap categories
  ([DELIVERY_ROADMAP.md](./DELIVERY_ROADMAP.md)); test definitions
  ([TEST_AND_EVIDENCE_STRATEGY.md](./TEST_AND_EVIDENCE_STRATEGY.md)).

## Structure skeleton

### 1. Work-package register format
The fields every package carries: ID, description, requirement IDs served,
inputs required, outputs produced, owner, status (repo vocabulary only), and
estimate range with assumptions. Format fixed here; population follows each
round's close, Rounds B–O.

### 2. Discovery work packages (Rounds B–O)
One package per remaining interview round plus the V1 audit, each listing the
documents it unblocks. The V1 audit package depends on Q-001 (read-only V1
database access) for its data-lessons depth. Round ordering is a Round N
decision recorded in the roadmap.

### 3. P1 implementation work breakdown (post-authorisation)
The pipeline domains from D-010 — data platform, research/experiment
infrastructure, backtest engine, book generation, approval workflow, cTrader
execution, monitoring, trade ledger, risk controls — each broken into
packages only after the specifications exist (Rounds C–K) and implementation
is explicitly authorised. Until then this section holds placeholders mapped
to the specs that will define them.

### 4. Dependency graph
The directed graph across all packages: which specification blocks which
build package, which data contract (Gate 1, per class under D-009) blocks
which class rollout, and which evidence artefact blocks which gate. Drawn
first for discovery (Rounds B–O interdependencies), extended to
implementation after Round N.

### 5. Critical path
The longest dependency chain to a live-eligible P1 book (Gate 7). Expected to
run through the data contract (Round D), canonical accounting (Round E),
backtest fidelity (Round F), and execution safety (Round J) — confirmed, not
assumed, once the graph is populated. No dates or durations are stated until
Q-007 is answered.

### 6. Staffing and capability
Who executes each package and with what skills — pending Q-007 (team
capability, weekly availability). D-008 establishes Jacob as sole user, but
not necessarily sole builder; this section records the actual answer.

### 7. External and evidence dependencies
Dependencies outside the team's control: Q-001 (secure read-only V1 database
access), Q-002 (Jacob's cBot code for the Round J sizing decision), DATA-007
(FMP evaluation against the full data contract), provider terms research
(Q-003, Q-004), and broker/platform constraints surfaced in Rounds C/D/J.

## Known inputs

- D-010: the P1 boundary fixes which domains need implementation packages.
- D-009: per-class Gate 1 dependency structure for the asset rollout.
- Q-001 and Q-002 are open and already known to block specific packages
  (V1 audit depth; Round J sizing-engine review).
- DATA-007: FMP must be evaluated, never assumed — an explicit package.
- OPS-003: resumability discipline applies to discovery work itself, so
  handoff upkeep is standing work, not a package that ends.
- BUS-003: no dependency may be removed by weakening an evidence or safety
  standard.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Staffing, capability, and weekly availability | Q-007, Round A continuation |
| Round ordering and which rounds can run in parallel | Round N |
| Full dependency graph contents | Populated as Rounds B–O close; reviewed Round N |
| Critical path confirmation and estimate ranges | After Q-007 + Round N |
| V1 audit depth (schema/data lessons) | Q-001 resolution |
| Sizing-engine review inputs (cBot code location) | Q-002 resolution → Round J |
