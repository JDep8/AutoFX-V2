# Logical Architecture

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [SYSTEM_CONTEXT.md](SYSTEM_CONTEXT.md), [SERVICE_AND_EVENT_CATALOGUE.md](SERVICE_AND_EVENT_CATALOGUE.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [ADR_INDEX.md](ADR_INDEX.md)
- **Approval evidence:** None yet

## Purpose

This document defines how AutoFX V2 is divided into modules, why each
boundary sits where it does, and which platform-level technology choices the
system depends on. It records the reasoning that keeps research, approval,
and execution honestly separated, so that no module can quietly weaken
another's guarantees. Technology selections are deliberately open until
Round N.

## Scope and decisions this document will own

- The set of logical services and the responsibility boundary between them.
- The rules governing inter-service communication (synchronous vs event,
  ownership of data, single-writer rules).
- Platform technology strategy: hosting, operating system, implementation
  language(s), PostgreSQL strategy, queueing, object storage, analytical
  storage, observability stack — all currently **open** (Round N).
- Performance and scale assumptions the architecture must satisfy.
- Which choices are significant enough to require an ADR (see
  [ADR_INDEX.md](ADR_INDEX.md)).

## Structure skeleton

### 1. Module inventory and boundaries

Will define each logical service and its single responsibility: **data**,
**research**, **backtest**, **portfolio (book generation)**, **approval**,
**account**, **execution**, **monitoring**, **ledger**, plus the
planning-only **research-centre** (P2) and **content** (P3) services.
Boundary placement — especially research/backtest vs portfolio, and
approval vs execution — is a Round N decision informed by Rounds F–K
domain answers. P2/P3 services are architecture-only until P1 is
live-validated (D-010).

### 2. Boundary rules and invariants

Will state the invariants each boundary enforces, e.g.: approval output is
disabled-by-default (EXEC-002); one authoritative sizing engine shared by
backtest and live (EXEC-008, Q-002); research output can never directly
modify a live configuration (RES-003); no-suitable-book is a first-class
outcome of the portfolio service (FR-003, D-005). Confirmed in Rounds
I/J/N.

### 3. Communication and data-ownership model

Will decide which interactions are events, which are direct calls, and
which service owns each datum (single-writer principle). Event names and
payload sketches live in
[SERVICE_AND_EVENT_CATALOGUE.md](SERVICE_AND_EVENT_CATALOGUE.md). Round N.

### 4. Platform technology strategy (all OPEN — Round N)

One subsection per open choice, each ending in an ADR before any selection
is treated as decided: hosting model; operating system; implementation
language(s); PostgreSQL strategy (single instance vs separated
transactional/analytical roles); queue/messaging technology; object
storage; analytical storage for ten-year minute-resolution data;
observability stack (OPS-001). No technology is chosen in this skeleton.

### 5. Performance and scale assumptions

Will record the sizing assumptions the architecture must carry: ten years
of minute-resolution data across eight CFD classes (DATA-001, DATA-002,
D-009); multi-day book-generation jobs with checkpoints, resumability,
cancellation, and deterministic seeds (FR-002, OPS-003); deterministic
exact reruns (VAL-003). Quantified volumes and throughput targets are
derived in Round D (data volumes) and Round I (generation workload) —
no numbers are assumed here.

### 6. Environments and promotion path

Will map the shadow → paper → live promotion path onto environments and
state which services run where (Gates 6–7; VAL-001). Round N, with Round J
for live specifics.

### 7. Architecture diagrams (planned artefacts)

Named planned Mermaid diagrams — none exist yet:

- **`service-boundaries.mmd`** — the module inventory of section 1 with
  ownership and communication edges (after Round N).
- **`promotion-state-machine.mmd`** — shadow/paper/live promotion states
  and gate transitions (after Rounds F/J).
- **`end-to-end-data-lineage.mmd`** — shared with
  [SYSTEM_CONTEXT.md](SYSTEM_CONTEXT.md) (after Rounds D/N).

## Known inputs

- MVP is the full Priority 1 pipeline: data → research → backtest → books →
  approval → cTrader execution → monitoring → ledger → risk controls —
  D-010, BUS-006 (`OWNER_APPROVED`).
- Architecture, data model, and calendars are designed for all eight CFD
  classes from day one; implementation rolls out FX-first — D-009, DATA-008
  (`OWNER_APPROVED`).
- Single user, single tenancy — D-008, BUS-005 (`OWNER_APPROVED`).
- USD accounts initially with a documented, unblocked multi-currency path —
  RISK-008.
- Multi-day generation jobs must checkpoint, resume, cancel, and reproduce
  identical results — FR-002, OPS-003, VAL-003.
- Approved books are disabled by default; live-marking is a separate act —
  EXEC-002, FR-001.

## Open questions

- Hosting model, operating system, and implementation language(s)? → Round N.
- PostgreSQL strategy, including whether analytical workloads share the
  transactional instance? → Round N.
- Queue/messaging, object storage, analytical storage, and observability
  technology selections? → Round N (each concluding in an ADR).
- Where exactly does the boundary sit between backtest and portfolio
  generation, and between approval and execution? → Round N, informed by
  Rounds F–J.
- Which component is the single authoritative sizing engine — AutoFX or
  Jacob's cBot? → Q-002, Round J (EXEC-008).
- What are the quantified data-volume and generation-throughput assumptions?
  → Rounds D and I (no figures assumed here).
- Which platform choices are build-vs-buy, and in what order are their ADRs
  raised? → Round N ([ADR_INDEX.md](ADR_INDEX.md)).
