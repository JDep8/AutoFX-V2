# Integration Contracts

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [SYSTEM_CONTEXT.md](SYSTEM_CONTEXT.md), [SERVICE_AND_EVENT_CATALOGUE.md](SERVICE_AND_EVENT_CATALOGUE.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [CTRADER_INTEGRATION_SPEC.md](../06-execution-and-risk/CTRADER_INTEGRATION_SPEC.md)
- **Approval evidence:** None yet

## Purpose

This document will define, at contract level, every external interface
AutoFX V2 depends on: what each party promises, what AutoFX verifies, and
what happens when a promise is broken. It keeps external dependencies
explicit so no provider is ever "assumed adequate" (DATA-007). Detailed
message flows for cTrader live in
[CTRADER_INTEGRATION_SPEC.md](../06-execution-and-risk/CTRADER_INTEGRATION_SPEC.md);
this document links to that spec and never duplicates it.

## Scope and decisions this document will own

- The contract template all external interfaces must satisfy (fields,
  guarantees, failure behaviour, evidence of conformance).
- One contract entry per external interface: cTrader, market-data
  provider(s), news/economic-calendar source(s), and any Round N
  infrastructure interfaces that carry trading-relevant data.
- Fallback and degradation policy per interface (what fails closed, what
  degrades, what alerts).
- It does **not** own provider selection (Round D / Round N decisions) or
  cTrader message-flow detail (execution spec).

## Structure skeleton

### 1. Contract template

Will define the fixed shape of every contract entry: parties and
authoritative side; data or actions exchanged; freshness/latency
expectations; error and outage behaviour; idempotency and reconnect rules;
security requirements (credential handling per SEC-001); conformance
evidence required before Gate 1 or Gate 6. Template agreed in Round N.

### 2. cTrader contract (execution and broker truth)

Will state contract-level obligations only: authentication, account and
symbol discovery, quotes, order lifecycle, reconnect and idempotency
expectations (EXEC-001); broker truth authoritative with continuous
reconciliation (EXEC-009); reachability requirements for kill switches
(EXEC-010). All message-level detail is deferred to
[CTRADER_INTEGRATION_SPEC.md](../06-execution-and-risk/CTRADER_INTEGRATION_SPEC.md)
(Round J, informed by A-002 and D-006 audit evidence).

### 3. Market-data provider contract(s)

Will capture the per-class data contract each provider must pass before
that class is eligible (DATA-008, Gate 1): history depth (DATA-001),
granularity (DATA-002), cost fields (DATA-003), quality and freshness
obligations (DATA-005, DATA-006). The FMP evaluation (DATA-007) is
recorded against this contract. Provider selection and contract numbers:
Round D.

### 4. News and economic-calendar contract(s)

Will define the point-in-time event contract: scheduled and actual
timestamps, consensus, previous, revision vintage, surprise, region,
severity, provenance (DATA-004); and the deterministic-enforcement
obligation — missing news data fails closed (D-007, VAL-005, EXEC-007).
Source selection: Round D; enforcement semantics: Rounds C/F.

### 5. Degradation and outage matrix

Will map each interface outage or quality breach to a required system
response (fail closed, degrade, alert), consistent with breaker definitions
(Glossary) and EXEC-009/EXEC-010. Rounds D/J/N.

### 6. Conformance evidence

Will define what evidence proves each contract is met (replay tests,
coverage reports, reconciliation runs) and where it is recorded. Evidence
standards per `.claude/rules/quantitative-evidence.md`; specifics per
round noted above. Nothing here is describable as tested until such
evidence exists and is owner-reviewed.

## Known inputs

- cTrader is the named execution interface, via its supported API messages —
  EXEC-001 (`PROPOSED`; detail open).
- Broker truth is authoritative for live positions/orders/fills/balance/
  margin — EXEC-009.
- FMP must be evaluated against the complete data contract with dated
  evidence, gaps, and fallbacks — DATA-007.
- Point-in-time event fields required of any news source — DATA-004.
- Deterministic news/calendar enforcement with replay tests; fail closed on
  missing news — D-007, VAL-005.
- Per-class contracts gate each asset class's rollout — D-009, DATA-008
  (`OWNER_APPROVED`).

## Open questions

- Which provider(s) supply market data per asset class, and does FMP pass
  the contract? → Round D (DATA-007).
- Which news/calendar source(s) meet the DATA-004 field set with acceptable
  provenance? → Round D.
- What freshness/latency expectations apply per interface and environment?
  → Round D (data), Round J (execution) — no figures assumed here.
- What are the reconnect, idempotency, and rate-limit obligations on the
  cTrader session, and how are they evidenced? → Round J and
  [CTRADER_INTEGRATION_SPEC.md](../06-execution-and-risk/CTRADER_INTEGRATION_SPEC.md)
  (A-002, D-006).
- What exact system response follows each class of contract breach
  (fail-closed scope, controlled-exit policy)? → Rounds J/N.
- Do P2/P3 phases add AI-provider or publishing-platform contracts, and are
  any blocked pending terms review? → Rounds L/M (RES-004, Q-003).
