# Discovery Status

- **Owner:** Jacob Depares
- **Status:** Living register
- **Version:** 0.3.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** INTERVIEW_RECORD.md, DECISION_LOG.md
- **Approval evidence:** n/a (register)

## Phase status

| Phase | Status | Notes |
|-------|--------|-------|
| Phase 0 — Discovery repository scaffold | COMPLETE 2026-08-17 | 78 planning files created; completeness-verified (53 domain skeletons checked: 0 missing, 0 header violations, 0 overclaims) |
| Phase 1 — Read-only V1 forensic assessment | NOT STARTED | Repo access verified (gh, read-only); DB access model approved (D-022) but role provisioning pending; start gated on Jacob's explicit go (NEXT_ACTIONS § B); primary bridge target identified (D-023: `code/TradingViewBridge.cs`) |
| Interview rounds A–O | Round A in progress | See below |
| Discovery Exit Review | NOT STARTED | Requires all rounds complete |
| Implementation | **GATED** | Requires `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>` |

## Interview rounds

| Round | Theme | Status |
|-------|-------|--------|
| A | Vision, users, business boundaries, success | IN PROGRESS — batches 1+2 answered; 11 decisions captured (D-001 direction, D-008…D-010, D-018…D-024); Q-001/002/006–009 resolved to the extent supported; Round A summary `PROPOSED` (INTERVIEW_RECORD.md), awaiting Jacob's approval |
| B | V1 outcomes and migration stance | NOT STARTED (feeds from V1 audit) |
| C | Markets, instruments, sessions, operating scope | NOT STARTED |
| D | Data acquisition, rights, quality, operations | NOT STARTED |
| E | Canonical accounting, drawdown, risk | NOT STARTED (Q-005 queued) |
| F | Backtest truth model | NOT STARTED |
| G | Strategy discovery, ML, experiment governance | NOT STARTED |
| H | Holdout, crises, regimes, acceptance gates | NOT STARTED (D-002 queued) |
| I | Book generation and approval | NOT STARTED (D-005 queued) |
| J | Accounts, cTrader, execution, reconciliation | NOT STARTED (D-006, Q-002 queued) |
| K | Open-trade monitor and trade ledger | NOT STARTED |
| L | Deep Research Centre | NOT STARTED (Q-003, Q-004 queued) |
| M | Content Studio, AI characters, business plan | NOT STARTED |
| N | Architecture, security, operations, delivery | NOT STARTED |
| O | UX, information architecture, wireframe | NOT STARTED (wireframes need `AUTHORISE WIREFRAME ONLY`) |

## Verified facts (dated)

- 2026-08-17: `C:\AutoFXV2.0` was empty at engagement start; git initialised
  same day; documentation-only content.
- 2026-08-17: V1 repo `JDep8/AutoFX` is private, accessible read-only via
  authenticated `gh` CLI (account JDep8). Python, branch `main`, updated
  2026-07-30, 247 tree entries, extensive root-level review docs.
- 2026-08-17: V1 repo root contains `101005649.rdp` — recorded as a security
  flag for the V1 audit; contents never read.
- 2026-08-17: Unauthenticated access to the V1 repo returns 404 — all V1
  inspection must use `gh`.
- 2026-08-18: Private GitHub repository `JDep8/AutoFX-V2` created per D-024
  (VERIFIED at creation: private visibility; default branch `main`; branches
  `main` + `planning/discovery-handoff` pushed @ `ad1d1e4`); local default
  branch renamed `master` → `main`; V1 repository untouched.
- 2026-08-18 (later): repository visibility VERIFIED as **PUBLIC**
  (`isPrivate: false` via authenticated `gh`, metadata-only). Attribution:
  changed by Jacob — USER-STATED (his closure-assurance instruction,
  2026-08-18); the `gh` check verifies the state, not the actor. The
  earlier private-visibility evidence was accurate at its recorded time.
  Tracked as Q-014 (temporary or permanent?); see TOOLING_REGISTER.md
  § Repository visibility.

## Round A completion assessment (2026-08-18 — closure-assurance pass)

Round A definition-of-done, per required topic. Classifications:
**COMPLETE** = `OWNER_APPROVED`; **COMPLETE FOR ROUND A** = decided at Round
A altitude, detailed values intentionally assigned to a named later round;
**INCOMPLETE** = requires another owner answer; **EVIDENCE PENDING** =
requires research/V1 evidence/specialist input. Round A must not close while
any topic is INCOMPLETE.

| # | Round A topic | Classification | Evidence / deferral |
|---|---------------|----------------|---------------------|
| 1 | Primary success hierarchy | **INCOMPLETE** | Substance USER-STATED (owner brief; D-019/D-020/D-021) but explicit ordering never individually confirmed — proposal recorded in PROJECT_CHARTER.md § Success hierarchy; awaiting Q-015 |
| 2 | Measurable meaning of trustworthy backtesting | **COMPLETE FOR ROUND A** | D-021 (form: bands + distribution tests, 15-metric set); values/samples/confidence → Round F |
| 3 | Profitability objective within hard evidence/risk constraints | **INCOMPLETE** (shared Q-015 dependency) | Substance owner-stated (owner brief BUS-001…004 + D-020 non-goals 3/6/7) — that part stands; the explicit ordering versus safety/evidence is the same missing input as Topic 1 (Q-015) |
| 4 | Users and operational roles | **COMPLETE** | D-008 (sole user) + D-019 (owner/approver vs autonomous technical operator) |
| 5 | Personal vs customer/commercial boundaries | **COMPLETE** | D-008; D-018 pre-commercialisation gate; D-020 non-goal 9 |
| 6 | Jurisdiction and legal-entity position | **COMPLETE FOR ROUND A** | D-018 (Australia; personal name as current state); final entity → the mandatory D-018 pre-live/pre-commercialisation gate; compliance detail → Round M |
| 7 | Priority 1/2/3 boundaries | **COMPLETE** | D-010 (+ D-009 universe/phasing) |
| 8 | Budget | **COMPLETE** | D-019 / BUS-009 (AUD 400/month ceiling, per-expense approval). The topic's decision content is fully decided; provider quotes are Round D/N work products, not budget-topic remainders |
| 9 | Timeline | **COMPLETE** | D-019 / BUS-011 (≈6-month paper target post-authorisation; 9–12 acceptable; live uncommitted). Targets fully decided; estimate ranges are Round N roadmap work products, not timeline remainders |
| 10 | Availability and autonomous operating model | **COMPLETE** | D-019 (5–10 h/week; autonomy lists; twelve mandatory stops) |
| 11 | Infrastructure constraints | **COMPLETE FOR ROUND A** | D-019 / OPS-005 (VPS funded, not production-approved; workstation dev/admin only; portability); VPS inventory → Round N |
| 12 | Measurable business KPIs | **INCOMPLETE** | Framework `PROPOSED` in PROJECT_CHARTER.md § KPI framework (20 KPIs, form-level, thresholds owned by Rounds D–N); awaiting Jacob's approval (Q-008 remainder) |
| 13 | Explicit non-goals | **COMPLETE** | D-020 / BUS-010 (twelve non-goals, canonical text in SCOPE_AND_PRIORITIES.md) |
| 14 | Database access path (asked in Round A batch 2) | **COMPLETE FOR ROUND A** | D-022 (model + roles + safeguards decided). Operational remainder: Jacob provisions `autofx_v1_readonly` — treated as a Phase 1 depth blocker, **not** a Round A closure blocker; Jacob confirms this exclusion via closure question (d) |
| 15 | Execution-bridge location (asked in Round A batch 2) | **COMPLETE** | D-023 (located: V1 `code/TradingViewBridge.cs` + `PriceBridge.cs`); behaviour verification is Round B/J audit work by design |
| 16 | Git/GitHub remote + operating model (authorised in Round A batch 2) | **COMPLETE** | D-024 (executed and verified). Visibility permanence is Q-014 — a governance question outside the Round A definition-of-done, decided by Jacob directly |

*Labelling rule:* COMPLETE FOR ROUND A is used when part of the topic's own
decision content is deferred to a named later round or gate; COMPLETE when
the topic's decision content is fully decided and only downstream work
products remain. *Vision note:* the mission/vision statement (charter
§ Mission, from the owner brief) is covered by Topics 1–3 — no separate
row.

**Verdict:** Round A may **not** close yet. Three rows INCOMPLETE — Topics
1 and 3 (one shared missing input: Q-015 hierarchy ordering) and Topic 12
(KPI framework approval, Q-008 remainder) — plus Jacob's approval of the
Round A summary itself. Closure condition: Q-015 answered + KPI framework
approved (or amended) + summary approved. No topic is EVIDENCE PENDING at
Round A altitude (Q-005/Q-010 evidence needs belong to Rounds E/H/B by
design). This assessment is `PROPOSED`; Jacob confirms or amends it —
including the row-14 exclusion of role provisioning from closure.

## Rounds B–O assurance matrix (high-level; recorded 2026-08-18)

Issue classifications: **OWNER_DECISION** (Jacob must decide) ·
**CLAUDE_RESEARCH_OR_EVIDENCE** (Claude completes autonomously and presents
evidence) · **TECHNICAL_AUTONOMY** (Claude determines without burdening
Jacob) · **EXTERNAL_SPECIALIST** (professional advice proposed at the gate).
**Standing rule:** TECHNICAL_AUTONOMY always means *drafting and mechanics
only* — every safety- or evidence-material artefact (formulas, lifecycles,
ledgers, message flows, breaker designs) requires Jacob's approval at the
round exit; nothing safety-material is self-approved (per
MODEL_ROUTING_POLICY quality rules and the discovery decision-authority
rule). This matrix is assurance-level, not the question inventory;
per-round batches are drafted when each round opens. Round ordering itself
is a Round N decision.

### Round B — V1 outcomes and migration stance
- **Entry evidence/dependencies:** Jacob's explicit V1-audit go; repo-side
  audit findings; DB-side depth needs D-022 role provisioned.
- **OWNER_DECISION:** migration stance per component (from proposed
  REUSE/ADAPT/REJECT/UNKNOWN); D-002 direction inputs; acceptance of Q-010
  contamination evidence (or its declared absence).
- **CLAUDE_RESEARCH_OR_EVIDENCE:** V1_AUDIT.md findings with evidence
  labels (ten audit areas incl. D-023 bridge + weighting); V1_REUSE_REGISTER
  proposals; truncation/selection-history evidence (D-003, Q-010).
- **TECHNICAL_AUTONOMY:** audit mechanics, file/dependency mapping, query
  design (read-only).
- **EXTERNAL_SPECIALIST:** none expected.
- **Artefacts:** V1_AUDIT.md § Findings; V1_REUSE_REGISTER.md.
- **Blockers:** owner go; role provisioning (depth only).
- **Exit criteria:** all ten audit areas evidenced or explicitly UNKNOWN
  (fail-closed); reuse classifications proposed with evidence + risk; Q-010
  answered by evidence or declared UNKNOWN.
- **Enables:** C, D, E (evidence), H (holdout facts), J (bridge facts).

### Round C — Markets, instruments, sessions, operating scope
- **Entry:** D-009 universe; Round B useful, not required.
- **OWNER_DECISION:** FX-first symbol shortlist; broker confirmation;
  session/weekend/news-window policy approvals (with D-007).
- **CLAUDE_RESEARCH_OR_EVIDENCE:** per-class session models, holiday/DST
  calendars, gap-risk evidence, broker symbol availability.
- **TECHNICAL_AUTONOMY:** calendar data modelling (versioned data, not
  code constants).
- **EXTERNAL_SPECIALIST:** none expected.
- **Artefacts:** MARKET_AND_NEWS_CALENDARS.md; SCOPE updates.
- **Blockers:** none once opened.
- **Exit:** FX symbol list + session model OWNER_APPROVED; per-class models
  drafted `PROPOSED`.
- **Enables:** D.

### Round D — Data acquisition, rights, quality, operations
- **Entry:** Round C symbols/sessions; data-contract template.
- **OWNER_DECISION:** provider selection and **every expense** (D-019);
  licensing acceptance; retention policy; quality thresholds (KPI-05/14
  numbers).
- **CLAUDE_RESEARCH_OR_EVIDENCE:** provider evaluations vs the full
  contract (FMP never assumed — DATA-007); dated licensing research; cost
  scenarios (free vs paid per D-019).
- **TECHNICAL_AUTONOMY:** schema/lineage/quality-check design detail.
- **EXTERNAL_SPECIALIST:** data-licensing legal review if redistribution/
  retention terms are ambiguous.
- **Artefacts:** all eight 04-data documents populated.
- **Blockers:** provider quotes; owner expense approvals.
- **Exit:** FX data contract `OWNER_APPROVED` and Gate-1-testable;
  PIT/quality/lineage policies approved.
- **Enables:** E/F; per-class Gate 1s.

### Round E — Canonical accounting, drawdown, risk numbers
- **Entry:** D-001 direction; Round B evidence on V1's actual definitions.
- **OWNER_DECISION:** Q-005 (default drawdown numbers, 15% heat cap fate,
  10k translation rule); canonical sizing formula (RISK-003); per-account
  risk overlay rules; the full risk-limit set and precedence (per-trade,
  aggregate, per-symbol, per-currency, correlated-exposure), daily/weekly
  loss, consecutive-loss, and margin limit definitions; emergency risk
  ownership and the override permission model (RISK_AND_DRAWDOWN_SPEC
  § open questions); breaker trip-vs-alert-only classes and restart
  authority (prepared with Rounds J/N); KPI-01/02/03 definitions.
- **CLAUDE_RESEARCH_OR_EVIDENCE:** V1 accounting behaviour evidence;
  formula proposals with worked examples.
- **TECHNICAL_AUTONOMY:** glossary formalisation and golden-scenario
  drafts — *drafting only; the canonical formulas are Jacob's Round E
  decision, never Claude's*.
- **EXTERNAL_SPECIALIST:** none expected.
- **Artefacts:** RISK_AND_DRAWDOWN_SPEC.md; GLOSSARY formulas (Fable
  re-read of the agent-drafted skeleton first — CURRENT_STATE Recovery
  item).
- **Blockers:** Round B evidence (partial start possible).
- **Exit:** canonical formulas + default numbers OWNER_APPROVED (D-001
  remainder closed; Q-005 resolved).
- **Enables:** F, I, J.

### Round F — Backtest truth model
- **Entry:** D-021 form; Round E accounting; Round D contract.
- **OWNER_DECISION:** D-021 numeric tolerances/samples/confidence/
  warning-failure/remediation (KPI-04/15/16/17 Gate 6 numbers; KPI-06
  reproducibility sampling rules, with Round G); conservative intrabar
  policy; cost-model conservatism level; **minimum shadow/paper evidence
  before any live approval — duration and minimum samples are Jacob's
  decision** (execution-and-risk rule § Fidelity); D-006 backtest↔live
  parity mechanism (with Round J) and D-007 replay-enforcement rules (with
  Round C).
- **CLAUDE_RESEARCH_OR_EVIDENCE:** fidelity-method research; golden-scenario
  design; paper/shadow campaign *method* options for Jacob's decision.
- **TECHNICAL_AUTONOMY:** lifecycle spec detail and test-suite design —
  drafting only; approved at the round exit.
- **EXTERNAL_SPECIALIST:** none expected.
- **Artefacts:** BACKTEST_FIDELITY_SPEC.md (Fable re-read first);
  TEST_AND_EVIDENCE_STRATEGY updates.
- **Blockers:** Rounds D/E outputs.
- **Exit:** fidelity spec + tolerance numbers OWNER_APPROVED (Q-009 fully
  closed); paper-campaign design (duration/samples) OWNER_APPROVED; D-006
  parity approach settled with Round J.
- **Enables:** G/H; Gates 2+ evidence standards.

### Round G — Strategy discovery, ML, experiment governance
- **Entry:** Round F truth model.
- **OWNER_DECISION:** strategy-family scope; ML governance boundaries;
  truncation policy (D-003); research-breadth budget (KPI-11 context).
- **CLAUDE_RESEARCH_OR_EVIDENCE:** taxonomy research; validation-method
  research (PBO/DSR/Reality Check/SPA with stated limitations).
- **TECHNICAL_AUTONOMY:** experiment-registry spec detail.
- **EXTERNAL_SPECIALIST:** optional quantitative-methodology review.
- **Artefacts:** RESEARCH_PROTOCOL, STRATEGY_TAXONOMY,
  EXPERIMENT_REGISTRY_SPEC, STATISTICAL_VALIDATION_PLAN, MODEL_GOVERNANCE.
- **Blockers:** none beyond F.
- **Exit:** protocols OWNER_APPROVED incl. D-003 truncation policy.
- **Enables:** H.

### Round H — Holdout, crises, regimes, acceptance gates
- **Entry:** Round B Q-010 evidence; Round G protocols.
- **OWNER_DECISION:** D-002 build/test split; crisis episode list (before
  outcomes seen — D-004); strategy acceptance criteria (Gate 3); KPI-07/12
  numbers.
- **CLAUDE_RESEARCH_OR_EVIDENCE:** regime/era research; measured episode
  evidence (LEAKAGE_AND_HOLDOUT_POLICY + CRISIS docs get Fable re-reads
  first).
- **TECHNICAL_AUTONOMY:** data-period ledger mechanics.
- **EXTERNAL_SPECIALIST:** none expected.
- **Artefacts:** LEAKAGE_AND_HOLDOUT_POLICY, CRISIS_AND_STRESS_FRAMEWORK,
  STRATEGY_ACCEPTANCE_CRITERIA.
- **Blockers:** Q-010 evidence from Round B (fail-closed if absent —
  prospective validation designed instead).
- **Exit:** D-002/D-004 closed; holdout locked and pre-registered; Gate 3
  criteria OWNER_APPROVED.
- **Enables:** I.

### Round I — Book generation and approval
- **Entry:** Rounds E/H.
- **OWNER_DECISION:** D-005 minimum composition/diversity rule; Gate 4/5
  book acceptance criteria (KPI-13 numbers); no-suitable-book confirmation
  (FR-003).
- **CLAUDE_RESEARCH_OR_EVIDENCE:** diversification/concentration measure
  research; V1 generation-scaling evidence (Round B area 6).
- **TECHNICAL_AUTONOMY:** job checkpoint/resume orchestration design
  (A-003, FR-002).
- **EXTERNAL_SPECIALIST:** none expected.
- **Artefacts:** BOOK_ACCEPTANCE_CRITERIA.md.
- **Blockers:** E (sizing canon), H (gates).
- **Exit:** D-005 closed; Gate 4/5 criteria OWNER_APPROVED.
- **Enables:** J.

### Round J — Accounts, cTrader, execution, reconciliation
- **Entry:** D-023 bridge evidence (Round B); Round E canon.
- **OWNER_DECISION:** single authoritative sizing engine (EXEC-008); D-006
  remediation architecture; maximum unprotected interval (EXEC-004);
  breaker/kill-switch policy; reconciliation discrepancy handling and
  **orphaned-position policy** (adopt/close/quarantine); **multi-account
  fan-out ordering and partial-failure policy**; **permitted order
  types/TIF/amendment set, partial-fill remainder policy, and retry
  classification/limits** (ORDER_AND_FILL_LIFECYCLE); **Gate 7
  live-enablement acceptance criteria** (prepared with Round N; decided by
  Jacob); KPI-08/09/17/18 numbers; V2 bridge name (D-023 candidates).
- **CLAUDE_RESEARCH_OR_EVIDENCE:** cTrader OpenAPI research; bridge audit
  evidence; broker constraint facts.
- **TECHNICAL_AUTONOMY:** message-flow/idempotency/reconnect design
  detail — drafting only; the specs are approved at the round exit.
- **EXTERNAL_SPECIALIST:** none expected.
- **Artefacts:** CTRADER_INTEGRATION_SPEC, ORDER_AND_FILL_LIFECYCLE,
  BROKER_RECONCILIATION, CIRCUIT_BREAKERS_AND_KILL_SWITCHES (Fable
  re-reads for the safety-material skeletons first), ACCOUNT_AND_SIZING_SPEC.
- **Blockers:** Round B bridge findings.
- **Exit:** cTrader integration, order/fill lifecycle, reconciliation, and
  breaker/kill-switch specs **OWNER_APPROVED**; EXEC-008 decided; D-006
  closed; live-safety invariants fully specified with replay-test designs.
- **Enables:** K; Gates 6–7 design.

### Round K — Open-trade monitor and trade ledger
- **Entry:** Round J.
- **OWNER_DECISION:** deterministic exit-reason hierarchy; monitoring signal
  set; risk-change response actions (reduce vs exit vs freeze —
  OPEN_TRADE_MONITOR_SPEC); Gate 8 review cadence and inputs (primary owner
  of the Gate 8 operational review — see coverage check below).
- **CLAUDE_RESEARCH_OR_EVIDENCE:** ledger provenance design; V1 monitor
  lessons.
- **TECHNICAL_AUTONOMY:** event-sourcing detail (FR-004 "painful detail").
- **EXTERNAL_SPECIALIST:** none expected.
- **Artefacts:** OPEN_TRADE_MONITOR_SPEC.md; ledger spec.
- **Blockers:** J.
- **Exit:** monitor + ledger specs OWNER_APPROVED incl. Gate 8 procedure.
- **Enables:** N; Gates 6–8 evidence collection.

### Round L — Deep Research Centre (P2, planning-only)
- **Entry:** P1 rounds substantially specified; Q-003/Q-004 research briefs.
- **OWNER_DECISION:** Q-003 consumer-UI automation ruling (with legal
  input); Q-004 video boundary; provider governance; research budget caps
  within D-019.
- **CLAUDE_RESEARCH_OR_EVIDENCE:** dated provider-terms research (per the
  research standard, sceptical pass included).
- **TECHNICAL_AUTONOMY:** provenance/catalogue schema detail.
- **EXTERNAL_SPECIALIST:** legal review of provider terms (Q-003 is
  `BLOCKED` without it).
- **Artefacts:** all six 07-research-centre documents.
- **Blockers:** Q-003 legal review.
- **Exit:** P2 specs complete (`PROPOSED`), RES-004 boundary ruled,
  implementation still gated on P1 `LIVE_VALIDATED` (D-010).
- **Enables:** M; P2 backlog.

### Round M — Content Studio, AI characters, business plan (P3, planning-only)
- **Entry:** D-018 gate; Round L.
- **OWNER_DECISION:** business-plan scenario acceptance; compliance
  checklist approval; character/brand decisions; kill criteria.
- **CLAUDE_RESEARCH_OR_EVIDENCE:** Australian financial-promotion research;
  platform-terms research; CAC/LTV scenario modelling (ranges, sourced).
- **TECHNICAL_AUTONOMY:** workflow/pipeline design detail.
- **EXTERNAL_SPECIALIST:** **mandatory** Australian legal/tax/
  financial-services/financial-promotion review before any
  commercialisation (D-018 gate; CONTENT-003).
- **Artefacts:** all five 08-content documents.
- **Blockers:** D-018 gate for anything beyond planning.
- **Exit:** business plan + compliance framework complete (`PROPOSED`);
  nothing published; P3 implementation gated on P1 `LIVE_VALIDATED`.
- **Enables:** Exit Review completeness.

### Round N — Architecture, security, operations, delivery
- **Entry:** Rounds C–K outputs (bulk of P1 specification).
- **OWNER_DECISION:** architecture acceptance; threat-model acceptance;
  hosting/OS/language/storage ADRs; VPS production decision (OPS-005, after
  inventory); environment/release plan; roadmap + estimate ranges (BUS-011);
  incident criteria and severity levels (with Round J); Gate 7 drill list
  and pass criteria; RPO/RTO values (with Round D, OPS-002); the definition
  of **"P1 `LIVE_VALIDATED`"** — the D-010 trigger for P2/P3
  implementation (prepared Rounds J/N, decided by Jacob); KPI-18/19/20
  cadences; round-ordering ratification.
- **CLAUDE_RESEARCH_OR_EVIDENCE:** VPS inventory (read-only, when Jacob
  authorises access); technology option research within D-019 budget;
  threat modelling; cost-model population.
- **TECHNICAL_AUTONOMY:** service boundaries, event catalogue, ADR drafts,
  diagram set.
- **EXTERNAL_SPECIALIST:** optional independent security review.
- **Artefacts:** all six 03-architecture + six 09-delivery documents.
- **Blockers:** upstream rounds; VPS access authorisation.
- **Exit:** architecture, security, operations, delivery plan
  OWNER_APPROVED; SEC-003 satisfied on paper.
- **Enables:** O; Exit Review.

### Round O — UX, information architecture, wireframes
- **Entry:** Round N; page inventory before screens (UX-003).
- **OWNER_DECISION:** IA approval; `AUTHORISE WIREFRAME ONLY` gate;
  wireframe review approvals (UX-001/002 checklists).
- **CLAUDE_RESEARCH_OR_EVIDENCE:** journey traceability from
  USER_ROLES_AND_JOURNEYS; V1 UI pain-point evidence (Round B area 8).
- **TECHNICAL_AUTONOMY:** mock-data design; page-spec drafting.
- **EXTERNAL_SPECIALIST:** none expected.
- **Artefacts:** all four 02-product-and-ux documents; wireframes (only
  after the wireframe gate; Desktop per D-011).
- **Blockers:** the wireframe gate phrase.
- **Exit:** IA + wireframes approved; safety-visibility checklist passes.
- **Enables:** Discovery Exit Review.

### Discovery Exit Review
- **Entry:** all rounds closed; registers reconciled.
- **OWNER_DECISION:** readiness classification acceptance; the
  implementation-authorisation phrase itself (per phase; Jacob alone).
- **CLAUDE_RESEARCH_OR_EVIDENCE:** the 20-item package; adversarial
  self-review with written evidence; resume drill (item 19).
- **TECHNICAL_AUTONOMY:** package assembly and gap-review mechanics only.
- **EXTERNAL_SPECIALIST:** none beyond those already engaged per round.
- **Artefacts:** IMPLEMENTATION_READINESS_REVIEW.md completed with
  evidence; open-item register.
- **Blockers:** any round not closed; any safety-critical decision not
  `OWNER_APPROVED` (all D-002…D-007 must be closed).
- **Exit:** READY/CONDITIONALLY_READY/NOT_READY classification presented;
  building starts only on the exact phrase.

## Full-scope coverage check (2026-08-18)

Mandate area → owning round(s): data + point-in-time integrity → D;
backtest fidelity → F; strategy families/pattern recognition/ML → G;
experiment + multiple-testing governance → G (audited H); holdout/regime/
crisis validation → H (evidence B); book generation/approval → I; drawdown +
sizing → E (book application I; engine J); cTrader execution → J;
open-trade monitoring → K; trade ledger → K; Research Centre → L; content +
AI characters → M; business plan → M; architecture + security → N;
delivery/operations → N; token/session continuity → standing discipline
(`.claude/rules/20-session-continuity.md` + handoffs), verified by Exit
Review item 19; UX + wireframes → O.

Findings:

1. **Gate 8 ownership was split** across K (monitor/ledger evidence), L
   (TRADE_REVIEW_WORKFLOW), and N (ops cadence) with no named primary —
   now assigned: **Round K owns the Gate 8 operational review procedure**,
   with L contributing the recommend-only research loop (RES-003) and N the
   operational cadence. Recorded in the Round K matrix entry above.
2. **Paper/shadow campaign design** (duration, minimum samples) previously
   implicit between F and N — now explicit as a **Round F OWNER_DECISION**
   (minimum shadow/paper evidence before live approval is Jacob's per the
   execution-and-risk rule); environments mapped in Round N
   (ENVIRONMENT_AND_RELEASE_PLAN).
3. **Governance items outside the round structure:** repository visibility
   (Q-014), rules-file naming (Q-011), and status-vocabulary scope (Q-013)
   — decided by Jacob directly, not owned by any round.
4. **Deliberate split, not duplication:** calendars/news exist in C/D
   (deterministic data) and F (replay-tested enforcement) under D-007 —
   ownership boundaries confirmed correct.
5. **Nothing found prematurely decided as an acceptance threshold:** all
   acceptance thresholds remain assigned to Rounds D–N; D-021/D-022 fixed
   form/model only; D-022 role names and D-023 V2 bridge names are
   explicitly provisional. (The KPI framework's zero-/100%-tolerance
   values are restatements of standing hard constraints, itemised in
   PROJECT_CHARTER.md § KPI framework preamble — not new thresholds.)
6. **Gate 7 / "P1 LIVE_VALIDATED" ownership was unassigned** — found by the
   independent challenge review (2026-08-18): no round owned the Gate 7
   live-enablement acceptance criteria or the D-010 "P1 `LIVE_VALIDATED`"
   trigger definition. Now assigned: Gate 7 criteria prepared in Round J
   (with Round N drill/pass criteria); "P1 LIVE_VALIDATED" definition
   decided in Round N (prepared J/N). Recorded in those matrix entries.
7. **CONFLICT recorded (Q-016, no winner chosen):**
   STATISTICAL_VALIDATION_PLAN is assigned to Round G by this matrix and
   DOCUMENT_INDEX, but its own open-questions table assigns all items to
   Round H; STRATEGY_ACCEPTANCE_CRITERIA sits in Round H while assigning
   most items to Round G. This governs when multiple-testing corrections
   and Gate 3 statistical criteria are decided. `PROPOSED` resolution
   (not applied): treat G and H as a paired block sharing these two
   artefacts, with final numbers landing in H — Jacob confirms or directs
   otherwise (Q-016).
8. After findings 1 and 6, **no mandate area is unassigned**; no round
   carries two conflicting owners except the recorded Q-016 conflict.

This coverage check is `PROPOSED` (Claude's audit conclusion, evidence =
the documents cited); Jacob may direct changes.
