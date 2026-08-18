# Page and Workflow Specification

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [INFORMATION_ARCHITECTURE.md](INFORMATION_ARCHITECTURE.md), [PRODUCT_REQUIREMENTS.md](PRODUCT_REQUIREMENTS.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md)
- **Approval evidence:** None yet

## Purpose

This document specifies the end-to-end workflows of AutoFX V2 and, for each
page in the approved inventory, what the page must show and allow. Workflows
come first: UX-003 requires flows to be defined before screens. It turns
catalogue requirements into concrete page obligations — most importantly the
safety surface (UX-001) and the book evidence pack (UX-002) — so that
wireframes can later be checked against it line by line.

## Scope and decisions this document will own

- The end-to-end user workflows across the platform lifecycle (idea →
  experiment → generation → candidate → approval → account linkage → live →
  monitoring → ledger → review).
- Per-page content obligations: which data, states, and actions each page must
  expose, cited by requirement ID.
- Interaction rules for safety-critical controls (kill switches, breakers,
  live-marking).
- It does **not** own the page inventory (IA), requirement text (catalogue),
  or wireframe acceptance ([WIREFRAME_REVIEW.md](WIREFRAME_REVIEW.md)).

## Structure skeleton

### 1. End-to-end workflows
One subsection per lifecycle flow, each as a step list with the pages touched
and the gates crossed (Gates 1–8 per the Glossary):
- Data onboarding and health monitoring (DATA-001..008) — flow detail from
  Round D.
- Experimentation and strategy research (QUANT-001..004) — Round G.
- Book generation runs: launch, checkpoint, resume, cancel, and the
  first-class "no suitable book" ending (FR-002, FR-003) — Round I.
- Candidate review and approval to the Approved Books register (FR-001,
  RISK-005) — Rounds H/I.
- Account linkage and live-marking of an approved book (EXEC-002, FR-005,
  RISK-007) — Round J.
- Live execution, open-trade monitoring, and controlled exits (EXEC-003..007,
  EXEC-010) — Rounds J/K.
- Ledger review and Gate 8 continue/reduce/pause/retire decisions (FR-004) —
  Round K.
- Incident handling and audit trails (OPS-001) — Round N.
Flow sequencing and page-touch mapping are confirmed in Round O.

### 2. Per-page specifications
One subsection per page area in the approved inventory (see
[INFORMATION_ARCHITECTURE.md](INFORMATION_ARCHITECTURE.md) section 1). Each
gives: mission, primary entities, required content cited by requirement ID,
available actions with their authorisation rules, and required states (empty,
loading, error, stale, fail-closed). Filled in Round O after the domain rounds
(C–K) supply the underlying definitions.

### 3. Book detail specification (UX-002)
The evidence pack a book detail view must expose: assumptions, constituents,
diversification, realised and mark-to-market drawdown, heat, costs, regimes,
crises, sensitivity, statistical evidence, failures, and approval history.
Each element is mapped to the round that defines its content: accounting
formulas → Round E (Q-005); costs and fidelity → Round F; regimes/crises →
Round H (D-004); diversification/composition → Round I (D-005); approval
history → Gate 4/5 workflow (FR-001). Layout is confirmed in Round O.

### 4. Safety surface behaviour (UX-001)
How the always-visible safety elements behave on every page, including what
changes when data goes stale, a breaker trips, or a kill switch is engaged —
all fail-closed presentations. Depends on breaker/kill-switch semantics from
Rounds J/K (D-006) and freshness definitions from Round D; presentation
decided in Round O.

### 5. Safety-critical interaction rules
Interaction patterns for irreversible or risk-bearing actions: live-marking a
book, engaging/disengaging kill switches at each scope, acknowledging
incidents, and cancelling generation runs. Confirmation semantics and
authorisation steps are decided in Rounds J/N and expressed as page behaviour
in Round O.

### 6. Standard comparison presentation
Wherever performance is shown, how the standard comparison configuration
(RISK-002, D-001) and per-book user inputs (RISK-001) are presented side by
side without conflation, always with uncertainty reporting (BUS-004). Detail
from Rounds E/F; placement in Round O.

## Known inputs (already decided)

- Realised peak-relative drawdown is the canonical approval metric; MTM
  excursion and heat are separate, always-visible live controls — RISK-006 /
  D-001 (`OWNER_APPROVED` direction).
- Standard comparison configuration exists (USD 100,000 / 1% risk per trade)
  as the common yardstick — RISK-002 / D-001.
- "No suitable book" is a first-class outcome and must be presentable as an
  honest result, never an error — FR-003 / D-005 direction.
- Approved books are disabled by default; live-marking is separate and
  version-specific — EXEC-002, FR-001.
- Every performance artefact carries uncertainty; profitability is never
  guaranteed — BUS-004.
- Generation runs are multi-day with checkpoints, resume, cancel, and status
  reporting — FR-002.

## Open questions

- Full page-by-page content obligations → Round O, after Rounds C–K supply
  definitions.
- Book detail element definitions: formulas and defaults → Q-005 (Round E);
  crisis framework → D-004 (Round H); composition rule → D-005 (Round I).
- Kill-switch and breaker interaction semantics per scope → D-006
  (Rounds F/J), expressed in Round O.
- Exit-reason hierarchy shown in Open Trades and Trade Ledger → EXEC-005
  (Round K).
- Reconciliation-discrepancy presentation (broker truth vs internal state) →
  EXEC-009 (Round J).
- Degradation-tolerance display on live books → D-021 form (bands +
  distribution tests); tolerance values → Round F.
