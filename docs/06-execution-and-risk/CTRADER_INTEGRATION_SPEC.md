# cTrader Integration Specification

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [INTEGRATION_CONTRACTS.md](../03-architecture/INTEGRATION_CONTRACTS.md), [ORDER_AND_FILL_LIFECYCLE.md](ORDER_AND_FILL_LIFECYCLE.md), [ACCOUNT_AND_SIZING_SPEC.md](ACCOUNT_AND_SIZING_SPEC.md), [BROKER_RECONCILIATION.md](BROKER_RECONCILIATION.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (EXEC-001, FR-005)
- **Approval evidence:** None yet

## Purpose

This document will specify how AutoFX V2 talks to cTrader: which supported API
messages are used for authentication, discovery, quotes, and orders, and how
the connection stays correct through rate limits, disconnects, and restarts.
It also owns the multi-account fan-out design and the hard separation between
demo and live environments. Everything here is discovery-phase specification;
no connection to any account is made before explicit implementation
authorisation (no-build gate).

## Scope and decisions this document will own

- The exact cTrader API surface AutoFX V2 uses (EXEC-001).
- Connection lifecycle: authentication, heartbeat, reconnect, recovery.
- Idempotency and client-order-ID scheme.
- Demo/live environment separation and its unmistakable labelling.
- Multi-account fan-out and partial-account-failure behaviour (FR-005).

Out of scope: order semantics above the transport (owned by
[ORDER_AND_FILL_LIFECYCLE.md](ORDER_AND_FILL_LIFECYCLE.md)); reconciliation
policy (owned by [BROKER_RECONCILIATION.md](BROKER_RECONCILIATION.md)).

## Structure skeleton

### 1. Authentication and authorisation
Which cTrader authentication flow is used, token lifecycle, and how credentials
are stored and rotated — specified without ever placing a secret in this
repository (SEC-001). Researched in Round J; secret-handling rules per
[SECURITY_AND_THREAT_MODEL.md](../03-architecture/SECURITY_AND_THREAT_MODEL.md)
(Round N).

### 2. Account discovery
How available demo/live accounts are enumerated, registered, and mapped to
AutoFX account records. Researched in Round J.

### 3. Symbol mapping
Mapping between canonical AutoFX symbols
([CANONICAL_DATA_MODEL.md](../04-data/CANONICAL_DATA_MODEL.md)) and
broker/cTrader symbol identifiers, including per-account symbol availability
and contract specifications. Round J, with per-class detail gated by D-009
phasing (FX first).

### 4. Rate limits
Documented cTrader/broker rate limits, how AutoFX stays inside them, and what
happens when a limit is hit (fail closed, never silently drop). Facts gathered
in Round J — no limit values are assumed here.

### 5. Streaming quotes
Quote subscription model, spot/depth requirements, staleness detection, and
the hand-off to the data-stale breaker. Round J, aligned with live-input
requirements (EXEC-003).

### 6. Heartbeat, reconnect, and recovery
Heartbeat cadence, disconnect detection, reconnect strategy, and the recovery
sequence that re-establishes truth (resubscribe, resync open state, reconcile)
before any new order is sent. Round J; recovery invariants shared with
[BROKER_RECONCILIATION.md](BROKER_RECONCILIATION.md).

### 7. Idempotency and client order IDs
ID scheme guaranteeing that retries, reconnects, and restarts can never
duplicate an order, and that every broker event maps back to one AutoFX
decision. Round J.

### 8. Demo/live environment separation
Hard separation of credentials, endpoints, configuration, and storage between
demo and live, with unmistakable visual labelling in every surface (UX-001).
Round J for mechanics; Round O for the visual treatment.

### 9. Multi-account fan-out
One approved book signal fanning out to multiple linked accounts (EXEC-002,
FR-005): ordering, per-account sizing overlays, partial-account failure
(some accounts fill, some reject), divergence detection between accounts, and
recovery to a consistent state. Round J.

## Known inputs

- EXEC-001: integration uses cTrader's supported API messages; message flows
  must be replay-tested before approval.
- EXEC-002: approved books are disabled by default; live-marking is separate
  and links to multiple demo/live accounts.
- FR-005: trading-account management across multiple demo and live accounts
  with partial-failure handling.
- D-006 (open): V1 gaps include polling-versus-bar timing differences and no
  proven reconnect/recovery discipline — V2 must design these explicitly.
- UX-001: environment (demo/live), broker connection, and kill-switch state
  must be impossible to overlook.
- No-build gate: no demo or live connection during discovery.

## Open questions

- Which cTrader API (and which message subset) is selected → Round J research
  brief with dated citations.
- Broker(s) and account structure to integrate first → Rounds C/D (D-009
  remainder) and Round J.
- Rate-limit values and back-off policy → Round J research.
- Client-order-ID format and uniqueness scope → Round J.
- Fan-out ordering and partial-failure policy (halt book vs continue per
  account) → Round J owner decision.
- Recovery sequence acceptance evidence for Gate 6 → Round J with
  [BACKTEST_FIDELITY_SPEC.md](../05-research-and-validation/BACKTEST_FIDELITY_SPEC.md).
