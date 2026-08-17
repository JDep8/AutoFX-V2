# Decision Log

- **Owner:** Jacob Depares
- **Status:** Living register
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** REQUIREMENTS_CATALOGUE.md, QUESTION_REGISTER.md
- **Approval evidence:** Per-decision, recorded below

Decisions affecting leakage, holdout integrity, risk, drawdown, sizing, live
safety, or legal/compliance exposure require Jacob's explicit approval.
History is never erased; superseded decisions are marked, not deleted.

---

## D-001 — Drawdown model (legacy conflict #1)

- **Conflict:** V1's canonical model was one 25% cap on realised
  closed-position, peak-relative drawdown (`dd_realised_peak`), with
  mark-to-market excursion separately disclosed and used for
  monitoring/breakers — defensible only alongside a 15% heat cap and a
  10,000-account translation rule. The V2 brief instead proposes a
  user-configurable drawdown cap and a USD 100,000 / 1% standard backtest.
- **Options considered:** (a) configurable cap per book keeping V1's
  measurement discipline; (b) retain V1 fixed 25%/15%/10k package; (c) defer
  entirely to Round E.
- **Decision (direction):** Option (a). Drawdown cap is a user input per book;
  realised peak-relative drawdown is the canonical approval metric;
  mark-to-market drawdown and heat remain separate always-visible live safety
  controls; USD 100k/1% is the standard comparison configuration.
- **Status:** `OWNER_APPROVED` (direction) — 2026-08-17, explicit selection by
  Jacob after plain-language explanation (see INTERVIEW_RECORD.md, Round A).
- **Open remainder:** exact default numbers (incl. whether the 15% heat cap
  survives, and the fate of the 10k translation rule) → Round E with V1 audit
  evidence. Tracked as Q-005.
- **Affects:** drawdown, sizing, live safety, book acceptance (Gate 4/5).

## D-002 — Build/test period split and touched-holdout eligibility (legacy conflict #2)

- **Conflict:** Each data period must serve development/selection **or**
  untouched testing, never both. Earlier alternatives: 2020+ build with
  2008–2015 testing, versus 2012+ build with 2008–2011 testing. Earlier holdout
  data may already have been touched by selection and may no longer be valid as
  final out-of-sample evidence.
- **Status:** `PROPOSED` (open) — requires V1 audit evidence of what data
  actually influenced selection, then Round H decision by Jacob.
- **Affects:** leakage, holdout integrity, final evidence validity.

## D-003 — Explicit truncation policy (legacy conflict #3)

- **Conflict:** V1 analysis found truncation responsible for most candidate
  elimination. V2 needs an explicit truncation policy that is a visible,
  owner-approved rule — never hidden inside implementation details.
- **Status:** `PROPOSED` (open) — Rounds G/H; V1 audit to surface the original
  truncation behaviour and its effect sizes.
- **Affects:** selection bias, multiple-testing accounting, strategy acceptance.

## D-004 — Crisis validation framework retention (legacy conflict #4)

- **Conflict:** Crisis validation was accepted in principle in V1-era work:
  multiple configurable measured historical crises, explicit success criteria,
  per-strategy crisis scores, portfolio resilience score, integrated into book
  approval. Synthetic stresses complement, never replace, measured episodes.
  V2 must decide to retain/replace/supersede.
- **Status:** `PROPOSED` (open) — Round H. Recommendation will be retention
  with explicit episode selection *before* seeing candidate outcomes.
- **Affects:** book acceptance, risk, evidence honesty.

## D-005 — Minimum book composition / no-suitable-book rule (legacy conflict #5)

- **Conflict:** V1 could collapse a "book" to one member. V2 needs an approved
  minimum-composition/diversity rule and a first-class "no suitable book"
  outcome that is never forced into producing a book.
- **Status:** `PROPOSED` (open) — Round I.
- **Affects:** diversification, risk concentration, book acceptance (Gate 4).

## D-006 — V1 live-execution gaps (legacy conflict #6)

- **Conflict:** V1 live execution had unresolved gaps: no proven real-fill
  history; backtest/live sizing divergence; polling-versus-bar timing
  differences; absent broker-truth reconciliation; no demonstrably reachable
  runtime breaker/kill switch. V2 must decide remediation architecture rather
  than inherit these gaps.
- **Status:** `PROPOSED` (open) — Rounds F/J; V1 audit to document each gap
  with evidence.
- **Affects:** live safety, execution fidelity, reconciliation, Gates 6–7.

## D-007 — Deterministic news/calendar enforcement with replay tests (legacy conflict #7)

- **Conflict:** Deterministic news and market-calendar enforcement must be
  replay-tested. News intelligence is not a substitute for deterministic
  exclusion rules. V2 must make this an explicit, testable control.
- **Status:** `PROPOSED` (open) — Rounds C/F; fail-closed behaviour when news
  data is missing is a hard rule (see `.claude/rules/data-integrity.md`).
- **Affects:** live safety, backtest fidelity, calendars.

---

## D-008 — Users and business model

- **Decision:** AutoFX V2 is for Jacob only — personal trading with own
  capital. No customers, subscribers, or copy-trading clients in scope. The
  content business (Priority 3) is assessed separately for its own compliance
  needs.
- **Status:** `OWNER_APPROVED` — 2026-08-17 (Round A, explicit selection).
- **Affects:** regulatory scope, multi-tenancy, roles/permissions, threat model.

## D-009 — Asset universe and rollout phasing

- **Decision:** Target universe is eight CFD classes — Forex, Indices, Metals,
  Crypto, Agriculture, Equities, Cash, Commodities. Architecture, data model,
  and calendars are designed for all eight from day one. Implementation and
  validation roll out in phases, **FX first**; each class is gated on its data
  contract passing Gate 1 (data eligible).
- **Status:** `OWNER_APPROVED` — 2026-08-17 (Round A; universe listed by Jacob,
  phasing option explicitly selected).
- **Open remainder:** per-class symbol lists, brokers, session/cost models →
  Rounds C/D.
- **Affects:** data contract size/cost, calendars, cost models, backtester.

## D-010 — Priority 1 MVP boundary

- **Decision:** The implementation MVP is the full Priority 1 platform (data →
  research → backtest → books → approval → cTrader execution → monitoring →
  ledger → risk controls). Priorities 2 (Research Centre) and 3 (Content) are
  planning-and-architecture only until P1 is live-validated.
- **Status:** `OWNER_APPROVED` — 2026-08-17 (Round A, explicit selection).
- **Affects:** roadmap, scope, delivery sequencing.
