# Risk and Drawdown Specification

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-001), [GLOSSARY.md](../00-governance/GLOSSARY.md), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-005), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md), [ACCOUNT_AND_SIZING_SPEC.md](ACCOUNT_AND_SIZING_SPEC.md), [CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md)
- **Approval evidence:** None yet

## Purpose

This document will hold the canonical definitions of every risk and accounting
quantity AutoFX V2 uses — so the backtester, the live engine, the monitor, and
the approval workflow all compute the same numbers the same way. It turns the
D-001 direction (configurable cap per book, realised peak-relative drawdown as
the approval metric) into exact, owner-approved formulas and limits. Nothing in
this skeleton is a decided value; decided values arrive in Round E.

## Scope and decisions this document will own

- Canonical formulas for all accounting and risk quantities (finalising the
  Glossary's (E)-marked terms).
- The limit framework: which limits exist, at which scopes, and how they
  interact.
- Event-ordering rules when multiple events share a timestamp.
- Emergency risk ownership and manual override permissions.
- Resolution of Q-005 (default numbers; fate of the legacy 15% heat cap and
  10,000-account translation rule).

Out of scope: position-size calculation (owned by
[ACCOUNT_AND_SIZING_SPEC.md](ACCOUNT_AND_SIZING_SPEC.md)); automatic trip
behaviour (owned by
[CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md](CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md)).

## Structure skeleton

### 1. Canonical accounting definitions
Exact formulas for closed balance, realised equity, mark-to-market equity,
realised peak, realised drawdown, open risk/heat, margin, free margin, and
exposure. Seeded plain-language versions live in the Glossary; Round E signs
off the canonical technical forms.

### 2. Currency conversion rules
Which rate, from which source, at which moment, converts non-USD quantities
into account currency for every definition above. Resolved in Round E;
multi-currency path constraints per RISK-008.

### 3. Event ordering
Deterministic ordering when entries, exits, price moves, or multiple fills
share a timestamp — required so drawdown, peak, and heat are reproducible to
the tick in backtest and live. Resolved in Round E.

### 4. Drawdown model (per D-001 direction)
Configurable drawdown cap per book; realised peak-relative drawdown as the
canonical approval metric; mark-to-market excursion and heat as separate,
always-visible live controls. Formulas per Glossary; defaults are Q-005.

### 5. Limit framework
Per-trade, aggregate, per-symbol, per-currency, and correlated-exposure
limits: which exist, their scopes, and precedence when several bind at once.
Defined in Round E.

### 6. Loss-based and margin controls
Daily loss, weekly loss, consecutive-loss, and margin limits: definitions,
measurement windows, and reset rules. Defined in Round E; trip behaviour is
cross-referenced to the breakers document.

### 7. Standard comparison configuration
USD 100,000 starting capital / 1% risk per trade as the common yardstick every
book is also evaluated at (D-001, RISK-002). This section records how the
standard configuration is applied, not whether it exists.

### 8. Account-specific overlays
How per-account risk overlays layer on top of book-level limits, and the rule
that each live configuration is separately revalidated. Interfaces with
RISK-007; detail split with
[ACCOUNT_AND_SIZING_SPEC.md](ACCOUNT_AND_SIZING_SPEC.md) in Rounds E/J.

### 9. Emergency risk ownership and manual override
Who owns risk in an emergency, which manual overrides exist, what permissions
they require, and how every override is evidenced. Defined in Round E; runbook
procedures live in
[INCIDENT_AND_RECOVERY_RUNBOOK.md](INCIDENT_AND_RECOVERY_RUNBOOK.md).

## Known inputs

- D-001 (`OWNER_APPROVED` direction, 2026-08-17): configurable cap per book;
  realised peak-relative drawdown canonical for approval; MTM excursion and
  heat separate live controls; USD 100k/1% standard comparison.
- RISK-001: user inputs include max acceptable portfolio drawdown and risk per
  trade, recomputed independently of the optimiser.
- RISK-004: drawdown measured from prior portfolio peak, not starting capital.
- RISK-005: book-level cap applies to the whole book; constituent exceedance
  is flagged and separately risk-assessed.
- RISK-006 (`OWNER_APPROVED` direction): canonical metric split as above.
- Glossary seeds for all (E)-marked terms.

## Open questions

- Q-005: default drawdown numbers; does the legacy 15% heat cap survive; fate
  of the 10,000-account translation rule → Round E with V1 audit evidence.
- Exact canonical formulas for every (E)-marked Glossary term → Round E.
- Event-ordering rule for shared timestamps → Round E.
- Full limit list (per-trade/aggregate/symbol/currency/correlated) and
  precedence → Round E.
- Daily/weekly loss, consecutive-loss, and margin limit definitions → Round E.
- Emergency risk ownership and override permission model → Round E.
