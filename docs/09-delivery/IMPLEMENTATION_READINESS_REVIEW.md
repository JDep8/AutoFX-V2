# Implementation Readiness Review
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DELIVERY_ROADMAP.md](./DELIVERY_ROADMAP.md), [TEST_AND_EVIDENCE_STRATEGY.md](./TEST_AND_EVIDENCE_STRATEGY.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md), [TRACEABILITY_MATRIX.md](../00-governance/TRACEABILITY_MATRIX.md), [CURRENT_STATE.md](../handoffs/CURRENT_STATE.md)
- **Approval evidence:** None yet

## Purpose

This document defines the Discovery Exit Review: the complete package Jacob
examines before deciding whether implementation may begin, the adversarial
self-review that hunts for the ways this project could be fooling itself, and
the readiness classification rules. Implementation starts only when Jacob,
having reviewed this package, explicitly writes
`AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>`. No other artefact
or approval substitutes for that statement.

## Scope and decisions this document will own

- The exit-review package checklist (contents fixed here; each item's
  substance is owned by its source document).
- The adversarial self-review question list and how findings are recorded.
- The readiness classification rules (READY / CONDITIONALLY_READY /
  NOT_READY) and the open-item register format.
- Out of scope: the authorisation decision itself (Jacob's alone) and the
  post-authorisation phase plan ([DELIVERY_ROADMAP.md](./DELIVERY_ROADMAP.md)).

## Structure skeleton

### 1. Review package checklist (20 items)
Each item is checked only when its source document is `OWNER_APPROVED` (or,
for drills and audits, actually performed with recorded evidence). Rounds
that resolve each item are shown.

1. Executive summary of the whole discovery outcome — written last.
2. Scope, priorities, non-goals, users, jurisdictions, success metrics —
   [SCOPE_AND_PRIORITIES.md](../01-discovery/SCOPE_AND_PRIORITIES.md),
   [PROJECT_CHARTER.md](../00-governance/PROJECT_CHARTER.md) (Round A
   continuation; Q-006, Q-008).
3. V1 evidence audit and reuse register —
   [V1_AUDIT.md](../01-discovery/V1_AUDIT.md),
   [V1_REUSE_REGISTER.md](../01-discovery/V1_REUSE_REGISTER.md) (Round B;
   Q-001).
4. Approved glossary and canonical calculations —
   [GLOSSARY.md](../00-governance/GLOSSARY.md) (Round E; Q-005).
5. Complete requirements catalogue with traceability —
   [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md),
   [TRACEABILITY_MATRIX.md](../00-governance/TRACEABILITY_MATRIX.md) (all
   rounds).
6. Workflows, permissions, page spec, wireframes —
   [PAGE_AND_WORKFLOW_SPEC.md](../02-product-and-ux/PAGE_AND_WORKFLOW_SPEC.md),
   [WIREFRAME_REVIEW.md](../02-product-and-ux/WIREFRAME_REVIEW.md) (Round O;
   wireframes under their own `AUTHORISE WIREFRAME ONLY` gate).
7. Logical architecture, data flows, service boundaries, integrations,
   threat model, ADRs — docs in `../03-architecture/` (Rounds C–N).
8. Data-source, point-in-time, quality, lineage, licensing, retention,
   monitoring, backup and recovery plans — docs in `../04-data/` (Round D).
9. Backtest truth model and fidelity plan —
   [BACKTEST_FIDELITY_SPEC.md](../05-research-and-validation/BACKTEST_FIDELITY_SPEC.md)
   (Round F; Q-009).
10. Research protocol, experiment registry, leakage/holdout policy,
    statistical plan, model governance — docs in
    `../05-research-and-validation/` (Rounds G/H; D-002, D-003, Q-010).
11. Crisis/regime/stress/survivability framework —
    [CRISIS_AND_STRESS_FRAMEWORK.md](../05-research-and-validation/CRISIS_AND_STRESS_FRAMEWORK.md)
    (Round H; D-004).
12. Strategy and book acceptance criteria, incl. minimum composition and
    no-suitable-book — acceptance-criteria docs (Rounds H/I; D-005).
13. Drawdown, heat, exposure, account, sizing, and live-risk specs —
    [RISK_AND_DRAWDOWN_SPEC.md](../06-execution-and-risk/RISK_AND_DRAWDOWN_SPEC.md),
    [ACCOUNT_AND_SIZING_SPEC.md](../06-execution-and-risk/ACCOUNT_AND_SIZING_SPEC.md)
    (Rounds E/J; D-001, Q-005).
14. cTrader lifecycle, multi-account, reconciliation, monitoring, stop
    protection, breakers, incident response — docs in
    `../06-execution-and-risk/` (Rounds J/K; D-006).
15. Trades evidence model (ledger in painful detail, FR-004) — Round K.
16. Research Centre plan and lawful provider options — docs in
    `../07-research-centre/` (Round L; Q-003, Q-004).
17. Content studio, AI-character, publishing, compliance, business plan —
    CONTENT-001..004 documents (Round M; Q-006).
18. Delivery roadmap, dependency graph, phased backlog, estimate ranges,
    cost scenarios, test plan, release gates — this folder's five sibling
    documents (Round N; Q-007).
19. Context-continuity procedure and a resume drill actually performed with
    recorded evidence (OPS-003) — `../handoffs/` discipline.
20. Full gap review across product, quant, data, ML, execution, security,
    SRE, compliance, UX, and business perspectives — performed at review
    time.

### 2. Adversarial self-review
Before classification, the package is attacked with these questions, each
answered in writing with evidence, and every failure logged as an open item:
hidden leakage or a touched holdout (D-002, Q-010); optimistic fills/costs or
impossible intrabar assumptions; inconsistent drawdown or sizing definitions;
acceptance reached because too many alternatives were tried (QUANT-001,
D-003); crisis periods chosen after outcomes were seen (D-004); a book
collapsing to a single risk driver (D-005); missing no-suitable-book
behaviour (FR-003); backtest/paper/live code-path divergence (D-006);
unprotected positions or unreachable kill switches (EXEC-004, EXEC-010);
reconciliation gaps (EXEC-009); stale or missing news failing open (D-007);
unsafe multi-account partial success (FR-005); provider-licensing or
consumer-UI automation assumptions (Q-003, Q-004, RES-004); fabricated or
weak evidence (BUS-003, RES-002); financial-promotion, synthetic-media,
likeness, or copyright exposure (CONTENT-003); handoffs depending on chat
memory (OPS-003); requirements without measurable acceptance evidence.

### 3. Readiness classification
- **READY** — only if **all** safety-critical and evidence-critical
  decisions are `OWNER_APPROVED` and traceable, the checklist is complete,
  and the adversarial review found no unresolved blocking finding.
- **CONDITIONALLY_READY** — open items exist but none carries the
  blocks-implementation flag; each has an owner, impact, recommendation, and
  decision deadline.
- **NOT_READY** — at least one open item blocks implementation.
Classification criteria detail is agreed with Jacob in Round N; the READY
bar above is fixed and not negotiable downward (BUS-003).

### 4. Open-item register format
Every open item at review time records: owner, impact, recommendation,
decision deadline, and a blocks-implementation flag. Items mirror into
[QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) where they are
questions.

### 5. Authorisation protocol
Even at READY, nothing is built until Jacob writes the exact authorisation
statement (per CLAUDE.md), naming the phase. Approval of this document, or of
the review package, is not approval to build.

## Known inputs

- The no-build gate wording and its list of forbidden pre-authorisation
  actions (CLAUDE.md).
- Q-001..Q-010 are the current open items feeding this review; several
  (Q-003 `BLOCKED`, Q-005, Q-007, Q-009, Q-010) already touch checklist
  items above.
- D-001 direction and D-008/D-009/D-010 are `OWNER_APPROVED`; D-002..D-007
  are open and safety- or evidence-critical, so all currently block READY.
- BUS-003/BUS-004: standards are never relaxed; profitability is never
  guaranteed anywhere in the package.

## Open questions

| Question | Resolved by |
|----------|-------------|
| Detailed classification criteria and review procedure | Round N |
| Resume-drill design and pass criteria (checklist item 19) | Round N (OPS-003) |
| Which open items carry the blocks-implementation flag | Populated at review time from the registers |
| Jurisdiction inputs to items 2 and 17 | Q-006, Round A continuation / Round M |
