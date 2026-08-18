# Project Charter — AutoFX V2.0

- **Owner:** Jacob Depares
- **Status:** `OWNER_APPROVED` at Round A altitude (Round A closure
  candidate approved 2026-08-18, D-036). Governed items carry their own
  lifecycle status per D-032: success hierarchy `OWNER_APPROVED` (D-027);
  KPI framework `OWNER_APPROVED` at form level (D-028); all numerical
  thresholds deliberately unset — owned by Rounds D–N.
- **Version:** 1.0.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** DECISION_LOG.md (D-008…D-010, D-018…D-021,
  D-027/D-028/D-034), SCOPE_AND_PRIORITIES.md, INTERVIEW_RECORD.md,
  TRADING_SIMULATION_AND_CERTIFICATION_SPEC.md
- **Approval evidence:** Round A batch 1 (2026-08-17) and batch 2
  (2026-08-18, verbatim in INTERVIEW_RECORD.md § Batch 2 answers)

## Mission

1. Produce backtests whose results are trustworthy indicators of what could
   reasonably be expected under real trading conditions.
2. Find and operate profitable portfolios within explicitly approved risk
   limits.

Profit is an optimisation objective. Data integrity, absence of leakage,
honest out-of-sample evidence, drawdown compliance, execution fidelity, and
live-trading safety are hard constraints. Profitability is never guaranteed.

## Success hierarchy (`OWNER_APPROVED` — D-027, 2026-08-18; Q-015 resolved)

1. **Capital protection / live-trading safety** and **evidence integrity /
   backtest fidelity** are **co-equal, non-negotiable hard constraints** —
   drawdown compliance, stop-loss protection, fail-closed breakers,
   kill-switch reachability; data integrity, no leakage, honest
   out-of-sample evidence, degradation within approved tolerances (D-021).
2. **Profitability** is pursued only inside those constraints; never
   guaranteed (BUS-004).
3. **Cost and delivery speed** come after safety, evidence integrity, and
   constrained profitability; deadlines never weaken gates (D-020
   non-goal 7; BUS-003).

**Conflict rule (owner-stated):** if safety and evidence integrity ever
conflict, neither may be silently weakened — the conflict escalates to
Jacob.

## Why V2 exists

V1 began implementation before the end-to-end product and evidence model were
sufficiently defined. V2 is a discovery-first engagement under an absolute
no-build gate (root `CLAUDE.md`).

## Owner, users, jurisdiction, and entity

- Jacob Depares is product owner, decision-maker, and final human approver;
  per D-008 (`OWNER_APPROVED` 2026-08-17) the sole user: personal trading
  with own capital. No customers, subscribers, or copy-trading clients.
- Per D-019, Jacob contributes ≈5–10 hours/week and is not the technical
  operator; Claude performs permitted technical work autonomously within the
  D-019 operating model, stopping for the twelve mandatory owner-decision
  triggers. AI systems are tools, never accountable owners.
- Per D-018 (`OWNER_APPROVED` 2026-08-18): Jacob is tax-resident in
  **Australia**; discovery, development, backtesting, and paper trading run
  under his **personal name** — explicitly the current state, not the final
  production structure. A **mandatory Australian legal, tax,
  financial-services and financial-promotion review** must occur before any
  commercial step (entity trading, external capital, copy trading, fees,
  selling signals/strategies/research, monetising content, promoting
  expected returns). Final entity structure is deferred to that gate.

## Priorities

- **P1 (implementation MVP, per D-010):** data platform, strategy research,
  realistic backtesting, book generation, approval workflow, approved-books
  register (disabled by default), account management, cTrader execution,
  open-trade monitoring, trade ledger, production risk controls.
- **P2 (planning-only until P1 live-validated):** Deep Research Centre.
- **P3 (planning-only until P1 live-validated):** Content and AI-media
  business.

## Asset universe

Eight CFD classes (D-009), phased rollout FX-first, each class gated on its
data contract.

## Budget and timeline (D-019, `OWNER_APPROVED` 2026-08-18)

- Operating ceiling **AUD 400/month** (excl. Claude, ChatGPT, existing VPS);
  a ceiling, not a target; free-first where quality permits; **every**
  expense pre-approved by Jacob; no auto-paid transitions; exceptional costs
  proposed separately; quality never silently reduced (BUS-009).
- First controlled paper-trading candidate targeted **≈6 months after
  implementation authorisation** — a planning target that never overrides
  gates; 9–12 months acceptable; live trading has **no committed date** and
  requires paper validation, execution validation, and separate explicit
  approval (BUS-011).
- Existing VPS is available and funded but **not** auto-approved as
  production infrastructure; the Windows workstation is dev/admin only; V2
  is designed portable, reproducible, and backed up (OPS-005).

## Non-goals (D-020, `OWNER_APPROVED` 2026-08-18 — BUS-010)

The twelve owner-approved non-goals are recorded canonically in
[SCOPE_AND_PRIORITIES.md](../01-discovery/SCOPE_AND_PRIORITIES.md)
§ Non-goals: no HFT/latency arbitrage; no discretionary-trade routing; no
profit guarantees; no live-by-default; no AI live-enablement; no
backtest-only approval; no gate-weakening for deadlines; no unreviewed V1
reuse; no external funds/paid signals/copy trading initially; no
research-influencing content; no deploy-because-complete; no silent
acceptance of missing/contaminated/insufficient evidence.

## KPI framework (`OWNER_APPROVED` at form level — D-028, 2026-08-18; Q-008 resolved)

**Approval scope (D-028):** Jacob approved the 20 measurement areas below
(extended to 22 the same day by the D-034 simulation requirement) as the
form-level framework, organised into **headline KPIs** for
executive/product decisions and **supporting diagnostic/operational
metrics** beneath them. No numerical threshold is approved anywhere in
this section; thresholds, confidence requirements, minimum samples, and
warning/failure bands remain assigned to their named later rounds. The
`KPI-nn` labels are measurement definitions tracing to requirement IDs
(mapping table below), not requirement IDs themselves.

### Headline vs supporting organisation (implements D-028; grouping adjustable at Jacob's direction)

| Headline KPI (executive/product view) | Supporting diagnostics beneath it |
|---|---|
| KPI-01 Net profitability after all costs | KPI-11 research breadth/survival · KPI-20 delivery cadence (context) |
| KPI-02 Risk-adjusted performance | (reads with KPI-01 supports) |
| KPI-03 Drawdown compliance | KPI-12 robustness/crisis · KPI-13 diversification/concentration |
| KPI-04 Backtest→paper/live degradation | KPI-15 band adherence · KPI-16 distribution/drift · KPI-17 execution parity · KPI-14 data-pipeline health |
| KPI-07 Holdout & leakage integrity | KPI-05 data integrity/freshness · KPI-06 reproducibility |
| KPI-10 Budget compliance | (owner-set numbers, D-019) |
| KPI-21 Simulation fidelity & reproducibility (D-034) | replay reproducibility · replay fidelity · processing performance |
| KPI-22 Certification coverage & execution correctness (D-034) | order-message parity · symbol-certification coverage · risk-sizing correctness · mandatory-SL correctness · entry-price tolerance · monitoring/reconciliation correctness · **zero unintended external orders** · certification failure/remediation status · KPI-08 stop-loss coverage · KPI-09 reconciliation accuracy · KPI-18 incident detection/recovery |
| KPI-19 Traceability & gate compliance | (governance spine; reported at every gate) |

Form-level framework only. **No acceptance threshold is proposed here** —
each KPI names the later round that owns its numbers (per D-021 discipline
and the interview method). The only numeric values that appear are (a)
KPI-10's owner-set D-019 numbers (AUD 400 ceiling; zero unapproved
expenses) and (b) zero-/100%-tolerance restatements of already-recorded
hard constraints (zero point-in-time violations — data-integrity rule; zero
holdout touches — leakage rule; zero beyond-interval unprotected exposure —
EXEC-004; zero gate bypasses and zero status-vocabulary violations —
standing governance rules; full reproducibility — VAL-003; full experiment
registration — QUANT-001, with its enforcement mechanics decided in
Round G). Nothing else carries a number.

KPI categories:
- **Outcome** — a result the project seeks; measured, never guaranteed.
- **Guardrail** — a bound that must never be breached and never be
  optimised against; a guardrail breach halts the affected activity and
  fails closed.
- **Leading** — a diagnostic indicator read ahead of outcomes; a leading
  breach does not auto-halt, but it must be dispositioned at the gate that
  owns it, and where a round adopts a leading KPI's threshold as a gate
  acceptance criterion (e.g. KPI-12/KPI-13 at Gates 3/4), failing it fails
  that gate.
- **Health** — a process-integrity indicator; the zero-tolerance items
  inside health KPIs (gate bypass, status-vocabulary violation) are
  governance-rule violations handled through the registers, not trading
  halts.

Every KPI is measured from repository-recorded evidence, never from memory
or chat. Risks of wrong optimisation are stated because a KPI pursued in
isolation can silently violate BUS-003.

### 1. Top-level success outcomes

**KPI-01 — Net profitability after all costs** (outcome)
- *Plain:* does trading actually make money once every real cost is paid?
- *Technical:* net realised P&L over the window, after spread, commission,
  swap/financing, slippage, and conversions; absolute and % of starting
  capital; computed from the trade ledger (FR-004), reconciled to broker
  statements.
- *Why:* the commercial objective inside hard constraints (BUS-002).
- *Data:* trade ledger, cost fields (DATA-003), broker statements.
- *Stage/cadence:* backtest per candidate; paper/live weekly and at Gate 8
  reviews.
- *Thresholds:* definitions Round E; Gate 4/5 values Rounds H/I; Gate 6
  values Round F; Gate 7 (live-enablement) values Rounds J/N.
- *Wrong-optimisation risk:* chasing headline P&L invites cost-model
  optimism and overfitting; never read without KPI-02/03/04.

**KPI-02 — Risk-adjusted performance** (outcome)
- *Plain:* is the return worth the risk taken to get it?
- *Technical:* risk-adjusted measures (e.g. Sharpe/Sortino/MAR family) on
  realised equity per canonical Round E accounting; exact measure set fixed
  in Rounds E/F.
- *Why:* raw return hides risk; approval quality depends on the ratio.
- *Data:* realised equity series, drawdown series.
- *Stage/cadence:* backtest per candidate; paper/live monthly.
- *Thresholds:* Rounds H/I (strategy/book acceptance).
- *Wrong-optimisation risk:* ratio-hacking via return smoothing or
  vol-dampening tricks; must be read with tail metrics (KPI-16).

**KPI-03 — Drawdown compliance** (guardrail)
- *Plain:* losses from the peak stay inside the cap Jacob set.
- *Technical:* realised peak-relative drawdown (D-001 canonical formula) vs
  the per-book cap; MTM excursion and open-risk heat tracked as separate
  always-visible live controls.
- *Why:* the primary capital-protection control (RISK-004/005/006).
- *Data:* realised equity, MTM marks, open-position risk.
- *Stage/cadence:* continuous in paper/live; per-run in backtest.
- *Thresholds:* Round E (Q-005: defaults, heat cap, translation rule).
- *Wrong-optimisation risk:* suppressing drawdown by holding losers
  unrealised — exactly why MTM/heat are separately visible.

### 2. Hard safety and evidence guardrails

**KPI-04 — Backtest→paper/live degradation within bands** (guardrail)
- *Plain:* live behaves like the backtest promised, within agreed bands.
- *Technical:* the D-021 fifteen-metric band set plus distribution/drift
  tests; breach = Gate 6 failure. **Precedence rule:** KPI-04 is the single
  guardrail; KPI-15 and KPI-16 are its evidence views (the measurements it
  is evaluated from) — any breach they surface is adjudicated under this
  KPI's guardrail rule, never separately.
- *Why:* fidelity is the product's first commercial goal (BUS-001).
- *Data:* paired backtest/paper/live metric series (VAL-006/007).
- *Stage/cadence:* per paper/shadow run, weekly summaries; live monthly.
- *Thresholds:* Round F.
- *Wrong-optimisation risk:* widening bands to pass is gate-weakening
  (forbidden); tuning the backtest to live data leaks.

**KPI-05 — Data integrity and freshness** (guardrail)
- *Plain:* the data is complete, correct, known-at-the-time, and current.
- *Technical:* completeness %, duplicate/malformed/out-of-order counts,
  point-in-time violation count (target zero), freshness SLA adherence,
  quarantine and repair rates (visible labels).
- *Why:* every downstream result inherits data quality (DATA-004/005/006).
- *Data:* quality-check outputs, quarantine log, lineage records.
- *Stage/cadence:* continuous once the platform exists; per-dataset at
  Gate 1.
- *Thresholds:* Round D.
- *Wrong-optimisation risk:* silent repair to boost completeness destroys
  PIT truth — quarantine-before-repair is mandatory.

**KPI-06 — Reproducibility** (guardrail)
- *Plain:* any recorded result can be exactly re-created.
- *Technical:* exact-rerun success rate from immutable code/data/config/seed
  versions (target: every audited result reproduces; VAL-003).
- *Why:* irreproducible evidence is not evidence.
- *Data:* experiment registry, version hashes, rerun logs.
- *Stage/cadence:* sampled per round of research; full check at Gates 2–5.
- *Thresholds:* Round F/G (sampling rules).
- *Wrong-optimisation risk:* narrowing the audited sample to pass; sample
  selection must be adversarial.

**KPI-07 — Holdout and leakage integrity** (guardrail)
- *Plain:* untouched test data stays untouched; every attempt is counted.
- *Technical:* holdout-touch count (target zero — the standing leakage
  rule), data-period ledger completeness, experiment-registration
  completeness (100% per QUANT-001; whether registration must precede
  execution is the `PROPOSED` default decided in Round G),
  multiple-testing accounting coverage (QUANT-001/003).
- *Why:* leakage silently fabricates performance (hard constraint).
- *Data:* data-period ledger, experiment registry.
- *Stage/cadence:* per experiment; audited at Gates 2/3 and Round H.
- *Thresholds:* Round H (with D-002/Q-010 evidence).
- *Wrong-optimisation risk:* relabelling touched data as unseen — expressly
  forbidden; a lost holdout is declared, not hidden.

**KPI-08 — Stop-loss protection coverage** (guardrail)
- *Plain:* no position sits unprotected longer than the approved interval.
- *Technical:* % of trades with protection attached atomically or within
  the approved compensating interval (EXEC-004); count of
  beyond-interval exposures (target zero, each an incident).
- *Why:* the core live-safety invariant.
- *Data:* order/fill event log, protection timestamps.
- *Stage/cadence:* continuous in paper/live; replay-tested pre-live.
- *Thresholds:* Round J (maximum unprotected interval).
- *Wrong-optimisation risk:* meeting coverage with token far-away stops;
  stop quality is a Round E/J sizing matter, not a checkbox.

**KPI-09 — Broker reconciliation accuracy** (guardrail)
- *Plain:* AutoFX's picture always matches the broker's truth, fast.
- *Technical:* discrepancy rate across positions/orders/fills/balance/
  margin, time-to-detect, time-to-resolve; broker truth authoritative
  (EXEC-009).
- *Why:* an unreconciled system trades on fiction.
- *Data:* reconciliation runs, broker statements/API state.
- *Stage/cadence:* continuous in paper/live.
- *Thresholds:* Rounds J/N (cadence + discrepancy classes).
- *Wrong-optimisation risk:* widening match tolerances to reduce
  "discrepancies" hides real divergence.

**KPI-10 — Budget compliance** (guardrail; numbers already owner-set)
- *Plain:* nothing is bought without Jacob; spend stays under the ceiling.
- *Technical:* unapproved expenditure count — target **zero** (owner-set);
  monthly operating spend vs the **AUD 400 ceiling** (owner-set, D-019);
  no auto-paid transitions.
- *Why:* explicit owner control of cost (D-019/BUS-009).
- *Data:* expense approvals register, provider invoices.
- *Stage/cadence:* monthly, and at every proposed expense.
- *Thresholds:* already set by D-019 (the one KPI with owner-set numbers).
- *Wrong-optimisation risk:* meeting the ceiling by silently choosing
  quality-compromising free options — expressly forbidden.

### 3. Leading indicators

**KPI-11 — Research breadth and survival** (leading)
- *Plain:* how much was tried, and how much honestly survived.
- *Technical:* experiment-registration completeness (100% per QUANT-001;
  enforcement mechanics → Round G), candidate survival rate per gate,
  truncation counts under the D-003 policy.
- *Why:* survival context is required to judge multiple-testing risk.
- *Data:* experiment registry.
- *Stage/cadence:* per research cycle (Rounds G+; P1 operation).
- *Thresholds:* Round G/H (what survival profile is acceptable).
- *Wrong-optimisation risk:* maximising survivors weakens gates; breadth is
  evidence, not a score.

**KPI-12 — Strategy robustness and crisis resilience** (leading)
- *Plain:* strategies keep working when conditions wobble or break.
- *Technical:* parameter-stability/perturbation pass rates, adversarial-cost
  results, per-strategy crisis-episode scores and portfolio resilience
  score (D-004 framework).
- *Why:* fragile strategies fail exactly when it hurts most.
- *Data:* validation suite outputs, crisis framework results.
- *Stage/cadence:* per candidate at Gates 3/4.
- *Thresholds:* Round H (episodes chosen before outcomes are seen).
- *Wrong-optimisation risk:* tuning to the chosen crises; episode selection
  is pre-registered.

**KPI-13 — Book diversification and concentration** (leading)
- *Plain:* a book is genuinely diversified, not one bet in disguise.
- *Technical:* constituent count vs the D-005 minimum-composition rule,
  correlation/concentration measures, single-driver exposure flags
  (RISK-005 flagged exceptions).
- *Why:* concentration converts one strategy's failure into book failure.
- *Data:* book composition, constituent return series.
- *Stage/cadence:* at book generation and Gate 4; monitored live.
- *Thresholds:* Round I.
- *Wrong-optimisation risk:* nominal diversification with correlated
  constituents; correlation measures must accompany counts.

**KPI-14 — Data pipeline health** (leading)
- *Plain:* the data machine runs clean before problems reach research.
- *Technical:* quarantine rate, repair rate, late-arrival rate, correction/
  revision counts, ingestion failure rate.
- *Why:* early warning for KPI-05 breaches.
- *Data:* pipeline logs, quarantine ledger.
- *Stage/cadence:* continuous once the platform exists.
- *Thresholds:* Round D.
- *Wrong-optimisation risk:* under-quarantining to look healthy.

### 4. Paper/live validation outcomes

**KPI-15 — Band adherence in paper/shadow** (outcome — evidence view of the
KPI-04 guardrail)
- *Plain:* paper trading stayed inside every promised band.
- *Technical:* per-metric adherence across the D-021 fifteen-metric set for
  the full paper window; the Gate 6 headline evidence. A band breach here
  is adjudicated under KPI-04's guardrail rule.
- *Why:* the decisive pre-live fidelity test.
- *Data:* paper run ledger vs backtest expectations.
- *Stage/cadence:* per paper campaign; reviewed at Gate 6.
- *Thresholds:* Round F.
- *Wrong-optimisation risk:* short windows flatter results — minimum
  sample/duration is part of the Round F decision.

**KPI-16 — Distribution consistency and drift detection** (outcome —
evidence view of the KPI-04 guardrail)
- *Plain:* live outcomes still look like they came from the backtest's
  world; drift is caught, not discovered in the P&L.
- *Technical:* D-021 distribution/calibration test results — execution
  degradation, regime change, feature drift, strategy decay, cost-model
  drift, frequency shifts, tail behaviour, cross-relationship breakdown.
- *Why:* bands catch size of error; distributions catch kind of error.
- *Data:* paired outcome distributions, cost observations.
- *Stage/cadence:* rolling in paper/live; reviewed at Gates 6–8.
- *Thresholds:* Round F (tests, confidence levels, warning/failure split).
- *Wrong-optimisation risk:* multiple-testing on drift alarms (alarm
  fatigue or cherry-picked calm) — test suite is fixed in advance.

**KPI-17 — Execution parity** (outcome)
- *Plain:* fills, costs, and timing in live match what was modelled.
- *Technical:* realised spread vs modelled, slippage vs modelled, fill
  quality, rejection/missed-trade rates, execution-timing deltas
  (bid/ask, never mid).
- *Why:* execution error compounds into silent strategy decay.
- *Data:* order/fill events, quote captures, cost model.
- *Stage/cadence:* continuous in paper/live; per-venue review Round J
  cadence.
- *Thresholds:* Rounds F/J.
- *Wrong-optimisation risk:* recalibrating the model to live without
  re-validating backtests creates circular fidelity.

### 5. Delivery and operational health

**KPI-18 — Incident detection and recovery** (guardrail/health)
- *Plain:* problems are seen fast, the system fails to a safe state, and
  recovery is proven — not assumed.
- *Technical:* time-to-detect, time-to-safe-state, breaker/kill-switch
  reachability test pass rate (EXEC-010), incident count by severity,
  recovery-drill results (OPS-001/003).
- *Why:* live safety is operational, not just architectural.
- *Data:* monitoring/alerting logs, incident records, drill evidence.
- *Stage/cadence:* drills pre-live (Gate 6); continuous live.
- *Thresholds:* Rounds J/N.
- *Wrong-optimisation risk:* under-reporting incidents to look stable;
  detection counts are evidence of visibility, not failure.

**KPI-19 — Traceability and gate compliance** (health)
- *Plain:* every requirement traces to evidence; no gate is ever skipped.
- *Technical:* % requirements with current design/test/evidence trace,
  gate-bypass count (target zero), register freshness (days since last
  reconciliation), status-vocabulary violations (target zero).
- *Why:* the governance spine of the whole engagement.
- *Data:* TRACEABILITY_MATRIX.md, registers, audit sweeps.
- *Stage/cadence:* per round close; full check at Exit Review.
- *Thresholds:* structural (zero-tolerance items already defined by rules);
  audit cadence agreed Round N.
- *Wrong-optimisation risk:* box-ticking traces without evidence quality —
  Fable review guards the trace content, not just its existence.

**KPI-20 — Delivery cadence vs plan** (health)
- *Plain:* progress tracks the roadmap ranges without gate pressure.
- *Technical:* milestone variance against Round N range estimates; explicit
  rule that variance is never closed by weakening a gate (D-020 non-goal
  7); paper-candidate target (≈6 months post-authorisation, BUS-011)
  tracked as a planning target only.
- *Why:* honest schedule visibility for a 5–10 h/week owner.
- *Data:* roadmap ledger, round-close records.
- *Stage/cadence:* monthly once implementation is authorised.
- *Thresholds:* Round N (range discipline).
- *Wrong-optimisation risk:* schedule pressure is the classic gate-eroder;
  this KPI exists to make that pressure visible, not to enforce dates.

**KPI-21 — Simulation fidelity and reproducibility** (guardrail; D-034)
- *Plain:* the accelerated replay behaves exactly like the production
  logic against honest history, and identical reruns give identical
  results, fast — without fidelity ever traded for speed.
- *Technical:* replay reproducibility (identical rerun ⇒ identical
  results); replay fidelity vs the Round F truth model (PIT correctness,
  no look-ahead); processing performance measured alongside.
- *Why:* Mode A is the pre-live proving ground for production behaviour
  (EXEC-012, VAL-008).
- *Data:* replay audit trail, version hashes, PIT datasets.
- *Stage/cadence:* per replay campaign; evidence at Gates 5–6.
- *Thresholds:* Round F.
- *Wrong-optimisation risk:* chasing replay speed by simplifying the fill
  or cost model — expressly forbidden (fidelity never weakened for
  speed).

**KPI-22 — Certification coverage and execution correctness** (guardrail; D-034)
- *Plain:* every symbol in an approved book passes an end-to-end demo
  certification, sized and protected correctly, with proof nothing ever
  reached a live account.
- *Technical:* order-message parity simulation↔intended cTrader routing;
  per-symbol certification coverage; risk-sizing correctness;
  mandatory-SL correctness; entry-price tolerance adherence;
  monitoring/reconciliation correctness; **zero unintended external
  orders (absolute)**; certification failure/remediation status.
  Supporting: KPI-08, KPI-09, KPI-18.
- *Why:* Mode C is the wiring-and-calculation gate before live
  eligibility (EXEC-014); demo success never claims live-equivalence.
- *Data:* certification register, order/fill events, reconciliation runs.
- *Stage/cadence:* per book version before Gate 7 eligibility; re-run on
  retest triggers (Round J).
- *Thresholds:* Round J (tolerance, coverage, expiry, remediation).
- *Wrong-optimisation risk:* certifying with unrealistically forgiving
  tolerances, or treating demo fills as live evidence — both forbidden.

### Framework rules

- Guardrails are never traded against outcomes (BUS-003); a guardrail
  breach halts the affected activity and fails closed. Leading and health
  categories follow the semantics defined in the preamble.
- No KPI is read in isolation; the framework is reviewed as a set at each
  gate and Gate 8 cycle.
- All acceptance thresholds are owner decisions in their named rounds
  (D through N); nothing here pre-empts them. KPI-10's numbers are
  owner-set by D-019; the remaining numeric values are zero-/100%-tolerance
  restatements of standing hard constraints, itemised in the preamble.
- KPI evidence lives in the repository (registers, ledgers, evidence
  packs) — never only in chat or memory.

### ID namespace and traceability

`KPI-nn` labels are **measurement definitions inside the framework, not
requirement IDs** — `KPI` is not in the approved requirement-prefix list
(`BUS FR NFR DATA QUANT VAL RISK EXEC SEC OPS UX RES CONTENT`). With
D-028's form-level approval, the labels stand as measurement definitions
tracing to the requirement IDs below; no new ID namespace is created.

| KPI | Governing requirement IDs / decisions |
|-----|----------------------------------------|
| KPI-01 | BUS-002, BUS-004, FR-004, DATA-003 |
| KPI-02 | BUS-002, RISK-006 (Round E measures) |
| KPI-03 | RISK-004/005/006, D-001 |
| KPI-04 | BUS-001, VAL-001, VAL-006, VAL-007, D-021 |
| KPI-05 | DATA-004, DATA-005, DATA-006 |
| KPI-06 | VAL-003 |
| KPI-07 | QUANT-001, QUANT-003, D-002 |
| KPI-08 | EXEC-004 |
| KPI-09 | EXEC-009 |
| KPI-10 | BUS-009, D-019 |
| KPI-11 | QUANT-001, QUANT-004, D-003 |
| KPI-12 | VAL-004, QUANT-002, D-004 |
| KPI-13 | FR-006, RISK-005, D-005 |
| KPI-14 | DATA-005, DATA-006 |
| KPI-15 | VAL-001, VAL-006 (evidence view of KPI-04) |
| KPI-16 | VAL-007 (evidence view of KPI-04) |
| KPI-17 | VAL-002, EXEC-001 |
| KPI-18 | EXEC-010, OPS-001, OPS-003 |
| KPI-19 | BUS-003 + the standing traceability rule |
| KPI-20 | BUS-011, OPS-004, D-019 |
| KPI-21 | EXEC-012, VAL-008, D-034 |
| KPI-22 | EXEC-013, EXEC-014, EXEC-004, EXEC-009, EXEC-010, D-034 |

## Open charter items

- KPI numerical thresholds — decided in their named rounds (D–N), never
  here.
- (Resolved 2026-08-18: success hierarchy → D-027; KPI framework → D-028;
  repository visibility → D-033; Round A closure candidate approved →
  D-036, Round A CLOSED.)
