# Strategy Taxonomy
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [RESEARCH_PROTOCOL.md](./RESEARCH_PROTOCOL.md), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-009)
- **Approval evidence:** None yet

## Purpose

This document names and defines the strategy families AutoFX V2 will research
before any selection happens. It gives every experiment a family home so that
research breadth, diversity, and duplicate detection have a shared vocabulary.
It does not rank families or predict which will work — that would be filler,
not evidence.

## Scope and decisions this document will own

- The canonical list of strategy families and their definitions.
- The classification rules for assigning a candidate to a family (and to more
  than one, where hybrid).
- The per-family rationale template referenced by
  [RESEARCH_PROTOCOL.md](./RESEARCH_PROTOCOL.md) (QUANT-002).
- Out of scope: which families are ultimately pursued or prioritised — that is
  a research outcome, not a taxonomy decision.

## Structure skeleton

### 1. Family definitions
One subsection per family from the owner mandate, each with a plain-language
definition, typical signal inputs, and the kind of economic/microstructure
rationale expected. Definitions are drafted here and confirmed in Round G:

- Trend / momentum
- Mean reversion
- Breakout
- Carry
- Volatility
- Session / event
- Cross-sectional / relative value
- Pattern-based
- Rules-based (transparent, hand-specified logic)
- Statistical (fitted classical models)
- Machine learning (governed by [MODEL_GOVERNANCE.md](./MODEL_GOVERNANCE.md))

### 2. Classification rules
How a candidate is assigned a primary family, how hybrids are labelled, and how
family labels feed duplicate/near-duplicate detection in
[BOOK_ACCEPTANCE_CRITERIA.md](./BOOK_ACCEPTANCE_CRITERIA.md). Rules are settled
in Round G.

### 3. Family-by-asset-class applicability
Which families are researchable per CFD class in the eight-class universe
(D-009), FX first. Applicability notes are gathered during Rounds C/D data work
and confirmed in Round G; no family is excluded without recorded reasoning.

### 4. Research-breadth expectations
How the taxonomy supports QUANT-001: family labels let the experiment registry
report breadth per family so selection cannot quietly concentrate. Reporting
shape is decided with
[EXPERIMENT_REGISTRY_SPEC.md](./EXPERIMENT_REGISTRY_SPEC.md) in Round G.

### 5. Baseline expectations per family
Which transparent baseline each family must beat before ML variants are
attempted (see RESEARCH_PROTOCOL.md section 3). Baseline choices are a Round G
decision.

## Known inputs

- Owner mandate lists the eleven families above as the research universe.
- D-009 (`OWNER_APPROVED`): eight CFD classes designed-for from day one, FX
  first; taxonomy must not assume FX-only structure.
- QUANT-002: every family entry carries a rationale expectation, not a
  performance claim.
- FR-006: books span multiple strategies, symbols, and timeframes — the
  taxonomy is an input to diversity measurement (D-005, Round I).

## Open questions

| Question | Resolved by |
|----------|-------------|
| Final family definitions and hybrid-labelling rules | Round G |
| Baseline class required per family | Round G |
| Family applicability per asset class | Rounds C/D data contracts → Round G |
| How family labels feed diversity/duplicate rules for books | D-005, Round I |
| Whether any family is deferred beyond P1 scope | Round G (owner decision) |
