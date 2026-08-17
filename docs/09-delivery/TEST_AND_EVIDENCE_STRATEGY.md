# Test and Evidence Strategy
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [BACKTEST_FIDELITY_SPEC.md](../05-research-and-validation/BACKTEST_FIDELITY_SPEC.md), [STRATEGY_ACCEPTANCE_CRITERIA.md](../05-research-and-validation/STRATEGY_ACCEPTANCE_CRITERIA.md), [BOOK_ACCEPTANCE_CRITERIA.md](../05-research-and-validation/BOOK_ACCEPTANCE_CRITERIA.md), [BROKER_RECONCILIATION.md](../06-execution-and-risk/BROKER_RECONCILIATION.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-006, D-007), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-009)
- **Approval evidence:** None yet

## Purpose

This document maps the eight-gate acceptance architecture to the test types
that produce evidence for each gate, and records — honestly — what each test
type does and does not demonstrate. A passing test is evidence of the specific
behaviour it exercises, never proof of correctness or of future profitability.
It exists so that no gate is ever passed on vague or borrowed evidence.

## Scope and decisions this document will own

- The gate-to-evidence map: which artefacts each of Gates 1–8 requires.
- The test-type catalogue and the claim each type is allowed to support.
- The evidence-pack structure reviewed manually at Gate 5.
- The rule set for describing test results (status vocabulary discipline).
- Out of scope: the tests' technical content (owned by the fidelity,
  acceptance, and reconciliation specs above) and environment mechanics
  ([ENVIRONMENT_AND_RELEASE_PLAN.md](./ENVIRONMENT_AND_RELEASE_PLAN.md)).

## Structure skeleton

### 1. Gate-to-evidence map (Gates 1–8)
One subsection per gate stating required evidence and its source spec:
Gate 1 — data eligible (per-class data contract, quality and PIT checks;
Round D). Gate 2 — experiment valid (registry completeness, leakage checks;
Rounds G/H). Gate 3 — strategy eligible (acceptance criteria incl. rationale
review; Rounds G/H). Gate 4 — book eligible (composition, crisis, drawdown
evidence; Rounds H/I). Gate 5 — approved-but-disabled, with manual
evidence-pack review by Jacob. Gate 6 — shadow/paper eligible (degradation
within Q-009 tolerance; kill-switch reachability per EXEC-010). Gate 7 —
live eligible, with **separate explicit approval** and verified caps, kill
switches, stop protection, ops ownership, and an approved staged ramp
(Rounds J/N). Gate 8 — continue/reduce/pause/retire review.

### 2. Test-type catalogue
The seven committed test families and where each is defined: golden scenarios
(hand-computed expected outcomes), property-based tests, metamorphic tests,
cross-engine comparison, record/replay of live sessions, broker-statement
reconciliation (EXEC-009), and replay-tested calendar/news enforcement
(VAL-005, D-007). Contents of each suite are decided in Rounds C/F/J.

### 3. What each test type demonstrates — and does not
For every family: the exact claim a pass supports and the claims it cannot
support (a golden scenario proves agreement with a hand computation, not
market realism; reconciliation proves broker-truth agreement, not strategy
quality). **V1 tests are never treated as proof of correctness**: any V1 test
considered for reuse is recorded in
[V1_REUSE_REGISTER.md](../01-discovery/V1_REUSE_REGISTER.md) with a note of
what it actually demonstrates, per the V1 audit.

### 4. Evidence-pack structure (Gate 5)
The pack Jacob reviews manually before a book becomes approved-but-disabled:
assumptions, test results with their demonstrated claims, uncertainty and
degradation measures (BUS-004), crisis results, composition flags (RISK-005),
and approval history. Field list agreed in Rounds H/I; format aligns with
UX-002's book-detail contents.

### 5. Live and post-live evidence (Gates 6–8)
Shadow/paper degradation measurement against the Q-009 tolerance,
kill-switch and breaker reachability demonstrations (EXEC-010),
staged-ramp adherence evidence, continuous reconciliation, and the Gate 8
review inputs. Defined in Rounds F/J/K.

### 6. Status vocabulary discipline
Nothing is described as `TESTED` until the test has actually run and passed;
nothing as `PAPER_VALIDATED` or `LIVE_VALIDATED` without the corresponding
gate evidence. A backtest result is never described as live-validated.
Profitability is never guaranteed by any evidence in this strategy.

## Known inputs

- The eight-gate architecture and its vocabulary
  ([GLOSSARY.md](../00-governance/GLOSSARY.md), "Gate 1–8").
- Gate 5 is a manual evidence-pack review; Gate 7 requires separate explicit
  live approval — approval of a book is never approval to trade it (EXEC-002,
  FR-001).
- VAL-002/VAL-003: golden scenarios and exact reproducibility — `PROPOSED`,
  Round F.
- VAL-005 / D-007: replay-tested deterministic calendar/news enforcement,
  fail-closed on missing news.
- EXEC-009/EXEC-010 and D-006: reconciliation and demonstrably reachable kill
  switches are gate evidence, remediating V1's gaps by design.
- BUS-003: no evidence standard is ever relaxed to improve an apparent
  result.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Backtest-vs-live degradation tolerance (Gate 6 pass condition) | Q-009, Round A continuation → Round F |
| Golden-scenario list, property/metamorphic suite contents | Round F |
| Crisis episodes and success criteria feeding Gate 4 | D-004, Round H |
| Gate 5 evidence-pack field list and format | Rounds H/I |
| Reconciliation cadence and discrepancy thresholds | Rounds J/N (D-006) |
| Which V1 tests, if any, are reusable and with what demonstrated claims | V1 audit, Round B |
