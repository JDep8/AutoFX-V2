# Book Acceptance Criteria
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [STRATEGY_ACCEPTANCE_CRITERIA.md](./STRATEGY_ACCEPTANCE_CRITERIA.md), [CRISIS_AND_STRESS_FRAMEWORK.md](./CRISIS_AND_STRESS_FRAMEWORK.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-001, D-005), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (FR-003, FR-006, RISK-001..RISK-005)
- **Approval evidence:** None yet

## Purpose

This document defines Gate 4 — the checkpoint at which a portfolio of eligible
strategies becomes an eligible book. It sets the composition, diversity, and
risk rules a candidate book must satisfy, and protects the honest outcome that
sometimes no suitable book exists. Gate 4 eligibility is not live approval:
approved books remain disabled until separately live-marked (EXEC-002).

## Scope and decisions this document will own

- The Gate 4 evidence pack and its pre-registered thresholds.
- Minimum composition and diversity rules (D-005, FR-006) and
  duplicate/near-duplicate detection between constituents.
- Exposure clustering analysis: hidden concentration across symbols, sessions,
  and strategy families.
- Independent recomputation of the declared drawdown cap and risk figures,
  outside the optimiser that produced the book.
- The first-class "no suitable book" outcome (D-005, FR-003).
- Out of scope: live activation (Gates 5–7), constituent eligibility (Gate 3),
  and canonical drawdown formulas (Round E, D-001/Q-005).

## Structure skeleton

### 1. Gate 4 evidence pack
Required contents: constituent Gate 3 packs, book-level validation with
uncertainty, portfolio resilience score
([CRISIS_AND_STRESS_FRAMEWORK.md](./CRISIS_AND_STRESS_FRAMEWORK.md)),
worst-period analysis at book level, diversity and clustering reports, and
independent risk recomputation. Contents fixed in Round I; thresholds
pre-registered before evaluation.

### 2. Minimum composition and diversity (D-005, FR-006)
The rule preventing a "book" from collapsing to one member (a V1 failure
mode): minimum constituents, spread across strategies/symbols/timeframes, and
how the taxonomy's family labels feed diversity measurement. Rule content is
Jacob's Round I decision — no minimum number is invented here.

### 3. Duplicate and near-duplicate detection
How constituents that are effectively the same trade (correlated signals,
shared parameters, overlapping exposures) are detected and treated. Detection
method and similarity treatment decided in Round I.

### 4. Exposure clustering
Analysis of concentration that composition counts alone miss: correlated
symbols, shared sessions, common risk factors, and behaviour under the
correlation-convergence stress. Method decided in Round I with Round H stress
inputs.

### 5. Independent cap recomputation (RISK-001, RISK-005)
The declared drawdown cap, risk per trade, and book-level figures are
recomputed by an independent path — never trusted from the optimiser that
constructed the book. Constituents exceeding the cap alone while the book
complies are prominently flagged and separately risk-assessed (RISK-005).
Recomputation design in Round I; formulas come from Round E (D-001, Q-005).

### 6. Standard comparison configuration (RISK-002)
Every candidate book is additionally evaluated at the standard configuration
(USD 100,000 / 1% risk per trade, per D-001) so books are comparable across
differing user inputs. Presentation decided in Round I.

### 7. No-suitable-book outcome (FR-003, D-005)
Generation may honestly end with zero qualifying books — a first-class result,
never an error and never coerced into output. What is reported in that case
(closest candidates, failing criteria, breadth) is decided in Round I.

### 8. Candidate-book ranking without hidden failures
Book ranking always shows the full generation denominator: books attempted,
rejected, and why — mirroring the Gate 3 rule. Format decided in Round I with
[EXPERIMENT_REGISTRY_SPEC.md](./EXPERIMENT_REGISTRY_SPEC.md).

## Known inputs

- D-001 (`OWNER_APPROVED`, direction): drawdown cap is a user input per book;
  realised peak-relative drawdown is the canonical approval metric; USD
  100k/1% is the standard comparison configuration. Exact numbers → Q-005,
  Round E.
- D-005 (`PROPOSED`, open): minimum composition and no-suitable-book rule —
  Round I decision.
- FR-001: Gate 4 feeds the approval workflow into the Approved Books register.
- FR-002: multi-day generation jobs must be resumable and deterministic — the
  evidence pack must survive checkpoint/resume.
- EXEC-002: approved books are disabled by default; live-marking is separate.
- UX-002: everything in the Gate 4 pack must be exposable on the book detail
  page.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Minimum composition/diversity rule content | D-005, Round I (Jacob) |
| Duplicate/near-duplicate detection method | Round I |
| Exposure-clustering method and stress interaction | Rounds H/I |
| Independent recomputation design and its formula source | Round E (Q-005) → Round I |
| No-suitable-book reporting contents | Round I |
| Book-level threshold values (pre-registered) | Rounds H/I |
