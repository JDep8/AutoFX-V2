# System Context

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [LOGICAL_ARCHITECTURE.md](LOGICAL_ARCHITECTURE.md), [INTEGRATION_CONTRACTS.md](INTEGRATION_CONTRACTS.md)
- **Approval evidence:** None yet

## Purpose

This document defines what AutoFX V2 is at its outermost boundary: the single
user, the external systems it talks to, and the hard line between what the
platform owns and what it merely consumes or commands. It exists so every
later architecture decision can be checked against one agreed picture of who
and what sits outside the system.

## Scope and decisions this document will own

- The definitive list of external actors and systems (owner, broker, data
  providers, news/calendar sources) and the direction of every interaction.
- The system boundary: which responsibilities are inside AutoFX V2 and which
  are explicitly delegated to external parties (e.g. broker truth per EXEC-009).
- The environment topology at context level (which environments exist and
  which external systems each may reach) — detailed environment design lives
  in [SECURITY_AND_THREAT_MODEL.md](SECURITY_AND_THREAT_MODEL.md).
- Naming of the planned context-level diagrams.

## Structure skeleton

### 1. Actors

Will enumerate human and system actors. Currently a single human actor —
Jacob, personal capital only (D-008, BUS-005) — plus external systems. Any
future actor change would reopen D-008. Confirmed in Round A; refined in
Round N if operational/service accounts are introduced.

### 2. External systems

Will list each external system at context level: cTrader (execution and
broker truth, EXEC-001, EXEC-009), market data provider(s) (DATA-001..003;
FMP under evaluation per DATA-007), news/economic-calendar source(s)
(DATA-004, D-007), and hosting/infrastructure providers. Provider selection
is open — Round D (data), Round N (hosting). Contract detail belongs in
[INTEGRATION_CONTRACTS.md](INTEGRATION_CONTRACTS.md), not here.

### 3. System boundary and delegated responsibilities

Will state, per external relationship, what AutoFX V2 trusts, verifies, or
owns — e.g. broker truth is authoritative for live positions/fills/balance
(EXEC-009) while AutoFX owns reconciliation. Resolved across Rounds D, J,
and N.

### 4. Environments at context level

Will name the environments (e.g. development, research/backtest,
shadow/paper, live) and which external connections each is permitted —
consistent with the promotion path Gate 6 → Gate 7. Environment set and
connection rules are decided in Round N; live-connection rules also depend
on Round J.

### 5. Context diagrams (planned artefacts)

Named planned Mermaid diagrams, to be produced once Rounds D/J/N settle
their inputs — none exist yet:

- **`system-context.mmd`** — actors, external systems, and boundary (this
  document's own diagram).
- **`end-to-end-data-lineage.mmd`** — provider → ingestion → storage →
  research/backtest → approval → execution → ledger lineage; jointly owned
  with the data-platform documents (Round D + Round N).
- Service-boundary and promotion-state-machine diagrams are owned by
  [LOGICAL_ARCHITECTURE.md](LOGICAL_ARCHITECTURE.md) and are only referenced
  here.

## Known inputs

- Sole user is Jacob; no customers, subscribers, or copy-trading — D-008,
  BUS-005 (`OWNER_APPROVED`).
- Execution broker interface is cTrader via its supported API messages —
  EXEC-001 (interface named in the owner brief; integration detail open).
- Eight CFD asset classes designed-for from day one, FX-first rollout —
  D-009, DATA-008 (`OWNER_APPROVED`).
- MVP boundary is the full Priority 1 platform; Research Centre and Content
  are planning-only until P1 is live-validated — D-010, BUS-006.
- Broker truth is authoritative for live state; AutoFX reconciles — EXEC-009
  (`PROPOSED`, Round F/J detail).
- FMP must be evaluated against the complete data contract, never assumed
  adequate — DATA-007.

## Open questions

- Which market-data provider(s) satisfy the data contract per class, and is
  FMP among them? → Round D (DATA-007).
- Which news/economic-calendar source(s) provide point-in-time events with
  the fields DATA-004 requires? → Round D.
- Hosting model and provider for each environment (cloud, VPS, on-premise,
  hybrid)? → Round N.
- Exact environment set and which environments may hold broker or provider
  credentials? → Round N (with Round J for live).
- Does the V1 database appear in the context as a read-only discovery source
  only, or also as a migration source? → Round N (bounded by SEC-002).
- Do the Research Centre (P2) and Content (P3) services introduce additional
  external systems (AI providers, publishing platforms), and how are they
  kept outside the P1 boundary until authorised? → Rounds L/M (D-010,
  RES-004).
