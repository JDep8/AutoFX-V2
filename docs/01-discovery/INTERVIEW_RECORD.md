# Interview Record

- **Owner:** Jacob Depares
- **Status:** Living register — **Round A CLOSED (`OWNER_APPROVED`
  2026-08-18, D-036)**; Round B not started
- **Version:** 1.0.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** DISCOVERY_STATUS.md, DECISION_LOG.md
- **Approval evidence:** Answers below are Jacob's explicit selections/text

## Round A — Vision, users, business boundaries, and success

### Batch 1 — 2026-08-17 (asked during plan review; 6 questions)

**Q1. Who is AutoFX V2 for — business model?**
Options offered: Jacob-only personal (recommended) / personal now, customer-ready later / customer-facing from start / internal team.
**Answer:** "Jacob-only, personal trading" → D-008 `OWNER_APPROVED`.

**Q2. Asset classes for first release?**
Options offered: FX only (recommended) / FX + crypto day one / FX + other CFDs.
**Answer (free text, verbatim):** "Forex, Indices, Metals CFD, Crypto CFD, Agriculture, Equities CFD, Cash CFD, Commodities."

**Q2b (clarification). Full target universe with phased rollout, or all eight end-to-end at first release?**
Options offered: target universe, phased FX-first (recommended) / all eight at first release / decide per class in Round C/D with cost evidence.
**Answer:** "Target universe; phased rollout, FX first" → D-009 `OWNER_APPROVED`.

**Q3. Drawdown-model conflict (D-001)?**
First response: "Can you explain please" → plain-language explanation provided
(realised vs mark-to-market drawdown; peak-relative measurement; V1's linked
25% cap / 15% heat / 10k translation package; V2 brief's configurable cap +
$100k/1% standard; why the definition drives approvals, kill switches, sizing).
**Answer after explanation:** "Configurable cap, keep V1's measurement
discipline" → D-001 direction `OWNER_APPROVED`; numbers → Round E (Q-005).

**Q4. Priority 1 MVP boundary?**
Options offered: P1 full, P2/P3 planning-only (recommended) / P1 staged demo-first / P1 + minimal Research Centre.
**Answer:** "Yes — P1 full, P2/P3 planning-only" → D-010 `OWNER_APPROVED`.

### Batch 2 — asked 2026-08-17 *(historical as-asked record; answers
received 2026-08-18 — see § Batch 2 answers below)*

**Q5 (Q-006). Jurisdictions and legal entity.** Where is Jacob tax-resident
and trading from, under personal name or a company?
Options offered: (a) personal name — recommended, record current reality now;
(b) existing company; (c) defer entity questions until the content business.
Noted: does not block P1; hard-blocks Round M financial-promotion compliance.
**Answer (2026-08-18, verbatim):** "Q5 = A will be personal name" → option
(a): trading under Jacob's personal name → D-018 `OWNER_APPROVED`.
Jurisdiction/tax residency not yet stated — Q-006 stays OPEN for that
component only (blocks Round M, not P1). *(Superseded the same day by the
full Q-006 answer in § Batch 2 answers below — jurisdiction supplied and
D-018 completed.)*

**Q6 (Q-007). Budget, horizon, availability, team, infrastructure.**
Free-form: monthly budget range for data + infrastructure; target date for
first *paper* trading; hours/week available; other people involved; existing
servers (this Windows Server? the V1 VPS?). Calibrates roadmap estimate
ranges.

**Q7 (Q-008). Measurable KPIs and explicit non-goals.** Candidates to be
proposed for editing; two seed non-goals put forward for confirmation:
no high-frequency/latency-sensitive trading; no manual discretionary trades
routed through AutoFX (it executes approved books only).

**Q8 (Q-009). Measurable meaning of backtest "accuracy".**
Options offered: (a) tolerance bands — live/paper stays within an agreed band
of backtest expectations on return, drawdown, cost-per-trade; (b) distribution
tests — live outcomes statistically consistent with backtest distributions;
(c) both, bands as the headline gate — recommended. Numbers set in Round F;
only the *form* asked now.

**Q9 (Q-001). PostgreSQL read-only access path.**
Options offered: (a) Jacob creates a dedicated read-only role (e.g.
`autofx_readonly`) with connection details in a local file outside the repo,
never echoed or committed — recommended; (b) Jacob runs drafted queries and
pastes results; (c) skip the DB audit.

**Q10 (Q-002). cBot location.** Repo or machine path of Jacob's cTrader cBot,
for Round J's single-authoritative-sizing-engine decision.

**Answers:** Q5 partially answered earlier on 2026-08-18 (above); the full
batch answered later the same day — recorded verbatim below.

### Batch 2 answers — 2026-08-18 (owner decisions, verbatim)

Jacob's instruction: "Record the following as my Round A Batch 2 answers and
owner decisions." Mapping: Q-006 → D-018 · Q-007 → D-019 · Q-008 → D-020 ·
Q-009 → D-021 · Q-001 → D-022 · Q-002 → D-023 · GitHub authorisation →
D-024. The message closed with turn-scoped execution instructions (validation
checks, commit, repository creation/push, reporting) — executed this session
and logged in SESSION_LOG.md; the durable content is below, verbatim.

> Q-006 — Jurisdiction and legal entity
>
> I am currently tax-resident in Australia and will initially conduct
> discovery, development, backtesting and paper trading under my personal
> name.
>
> This is not the final production business structure. A mandatory
> Australian legal, tax, financial-services and financial-promotion review
> must occur before any of the following:
>
> - live commercial trading through a business entity;
> - accepting or managing external capital;
> - copy trading;
> - charging performance, subscription or platform fees;
> - selling trading signals, strategies or research;
> - monetising financial or trading content;
> - publicly promoting expected trading returns.
>
> Record personal ownership as the current state. Defer the final entity
> structure to a mandatory pre-live and pre-commercialisation decision gate.
>
> Q-007 — Budget, timeline, availability, team and operating model
>
> BUDGET
>
> - The operating budget ceiling is AUD 400 per month.
> - This excludes Claude, ChatGPT and the existing VPS because they are
>   already paid through other arrangements.
> - AUD 400 is a ceiling, not a spending target.
> - Prefer a free version whenever it meets the required quality,
>   reliability, security, licensing, data coverage, retention and usage
>   limits.
> - A free option must not be selected if it materially compromises backtest
>   accuracy, data quality, security, maintainability or production
>   reliability.
> - Every new expense requires my explicit approval before purchase or
>   subscription, even when it is within the AUD 400 ceiling.
> - Before requesting approval, present the free option, recommended option,
>   price, benefits, limitations and expected ongoing cost.
> - No trial, service or subscription may automatically transition into a
>   paid plan.
> - One-off historical-data purchases, specialist datasets, regulatory
>   advice, legal advice and other exceptional costs must be proposed
>   separately.
> - If the required quality cannot be achieved within the budget, present
>   the evidence, alternatives and cost difference for my decision. Do not
>   silently reduce quality.
>
> TIMELINE
>
> - Target the first controlled paper-trading candidate approximately six
>   months after implementation is explicitly authorised.
> - This is a planning target and must not override data-integrity,
>   backtest-fidelity, security, risk or acceptance gates.
> - A nine-to-twelve-month timeline is acceptable if required to produce
>   trustworthy evidence.
> - Live trading has no committed date.
> - Live trading requires successful paper validation, execution validation
>   and separate explicit approval.
>
> AVAILABILITY AND TEAM
>
> - Assume I can contribute approximately 5–10 hours per week.
> - I am the product owner, decision-maker and final human approver.
> - I do not want to act as the technical operator by manually writing code,
>   running routine queries or copying query results between systems.
> - Claude should autonomously perform permitted technical work while I
>   guide requirements, product decisions, risk decisions, commercial
>   decisions, expenditure and acceptance.
> - Claude, ChatGPT and other AI systems are tools rather than accountable
>   owners.
> - No permanent human development team should currently be assumed.
> - Specialist Australian legal, tax, regulatory, security, data-licensing
>   or quantitative advice should be proposed when the relevant gate
>   requires it.
>
> AUTONOMOUS WORKING MODEL
>
> During discovery, Claude may autonomously:
>
> - maintain approved discovery and governance documentation;
> - perform read-only repository inspections;
> - run authorised read-only database queries;
> - conduct approved research;
> - validate documentation and traceability;
> - create documentation commits and push them to approved branches when
>   specifically authorised.
>
> After I provide the exact implementation-authorisation phrase for a named
> phase, Claude may autonomously:
>
> - write and refactor application code;
> - create tests;
> - run tests and validation;
> - generate and execute permitted SQL;
> - create and execute development migrations;
> - build development infrastructure;
> - inspect results and diagnose failures;
> - create commits;
> - push validated work to the approved phase branch;
> - continue iterating until the phase acceptance criteria are met or a
>   genuine decision/blocker requires me.
>
> I should not have to approve every file edit, query, table, index, test,
> commit or routine technical decision within an approved phase.
>
> Claude must stop for my decision when encountering:
>
> - any new expense;
> - a major unresolved product or architecture decision;
> - conflicting requirements;
> - risk acceptance;
> - legal or regulatory uncertainty;
> - destructive production operations;
> - changes to V1;
> - live trading enablement;
> - production deployment;
> - merging into main;
> - publication or distribution of financial content;
> - a decision outside the authorised phase.
>
> The current implementation gate remains active. These answers define the
> future operating model but do not themselves authorise application
> implementation.
>
> INFRASTRUCTURE
>
> - The existing VPS is available and already funded.
> - It is not automatically approved as production infrastructure.
> - Inventory its specifications, operating system, access model, security,
>   capacity, backup and recovery capability during infrastructure
>   discovery.
> - Treat the current Windows computer as development and administrative
>   infrastructure only.
> - Design V2 to be portable, reproducible, backed up and capable of moving
>   between hosting environments.
> - Do not purchase additional infrastructure without my approval.
>
> Q-008 — KPIs and non-goals
>
> I confirm these non-goals:
>
> 1. AutoFX V2 will not perform high-frequency, ultra-low-latency or
>    latency-arbitrage trading.
> 2. AutoFX V2 will not route manually initiated discretionary trades. It
>    executes approved and versioned books only.
>
> Also record these non-goals:
>
> - No guarantee of profitability or fixed returns.
> - No live trading by default.
> - No autonomous AI decision to enable live trading.
> - No strategy approval based solely on an attractive historical backtest.
> - No weakening of validation, data-quality or risk gates to meet a
>   deadline.
> - No direct reuse of V1 code without evidence-based review.
> - No external customer funds, paid signals or copy trading in the initial
>   scope.
> - No content output that overstates or influences trading-research
>   conclusions.
> - No production deployment merely because code or a Git branch is
>   complete.
> - No silent acceptance of missing, contaminated or insufficient evidence.
>
> Claude may propose measurable KPI candidates in the appropriate discovery
> round. All final targets, thresholds and pass/fail criteria require my
> approval.
>
> Q-009 — Measurable backtest accuracy
>
> Select option C: both tolerance bands and statistical distribution tests.
>
> TOLERANCE BANDS
>
> Tolerance bands will provide an understandable headline comparison between
> backtest, paper and live performance, including:
>
> - net return;
> - drawdown;
> - risk-adjusted return;
> - win rate where statistically meaningful;
> - trade frequency;
> - average win and loss;
> - holding time;
> - realised spread;
> - commission;
> - swap and financing costs;
> - slippage;
> - cost per trade;
> - missed or rejected trades;
> - execution timing;
> - fill quality.
>
> DISTRIBUTION AND DRIFT TESTS
>
> Distribution and calibration tests must determine whether paper/live
> outcomes remain statistically consistent with expected backtest
> distributions and detect:
>
> - execution degradation;
> - market-regime changes;
> - feature drift;
> - strategy decay;
> - cost-model drift;
> - changes in trade frequency;
> - unexpected tail behaviour;
> - breakdown of cross-strategy or cross-symbol relationships.
>
> The final tolerance values, sample-size requirements, confidence levels,
> warning thresholds, failure thresholds and remediation rules will be
> established in Round F.
>
> A strategy or book may not be declared accurate based only on headline
> return, correlation or a small number of live trades.
>
> Q-001 — PostgreSQL access and autonomous database management
>
> Separate V1 audit access from V2 database construction.
>
> A. V1 DATABASE — PERMANENTLY READ-ONLY
>
> The existing AutoFX V1 PostgreSQL database remains read-only.
>
> Use a dedicated read-only role, provisionally named:
>
> autofx_v1_readonly
>
> Once secure access is configured, Claude may autonomously:
>
> - inspect schemas, tables, indexes, constraints and metadata;
> - generate and execute SELECT queries;
> - inspect query plans;
> - profile data quality;
> - identify missing records, gaps and duplicates;
> - analyse data distributions;
> - investigate lineage;
> - repeat and refine read-only queries without per-query approval.
>
> I do not want to manually run Claude-generated queries and paste the
> results back.
>
> Claude must not perform any INSERT, UPDATE, DELETE, CREATE, ALTER, DROP,
> TRUNCATE, migration, repair or administrative operation against V1.
>
> B. V2 DEVELOPMENT DATABASE — AUTONOMOUS BUILD ACCESS
>
> After I provide the exact implementation-authorisation phrase for the
> relevant named phase, Claude is authorised to autonomously create and
> maintain isolated AutoFX V2 development and test databases.
>
> Within an authorised V2 development or test environment, Claude may:
>
> - create databases and schemas;
> - create, alter and remove tables;
> - create and modify columns;
> - create constraints and relationships;
> - create, rebuild and remove indexes;
> - create views and materialised views;
> - create functions and procedures where justified;
> - implement partitioning and retention structures;
> - insert, update and delete development data;
> - ingest historical and current market data;
> - ingest news, cost, spread, commission, swap and slippage data;
> - perform deduplication and controlled data repairs;
> - create and execute migrations;
> - create rollback or forward-recovery procedures;
> - generate seed and test data;
> - analyse and optimise query performance;
> - recreate disposable development/test databases;
> - run database tests and validation queries;
> - execute approved migration pipelines without requiring me to run
>   individual commands.
>
> I should not be required to approve every development query, database,
> table, column, index, constraint or routine migration within an authorised
> implementation phase.
>
> C. DATABASE ROLE SEPARATION
>
> Design separate least-privilege roles, provisionally:
>
> - autofx_v1_readonly — V1 audit access only;
> - autofx_v2_migrator — V2 schema migrations and controlled DDL;
> - autofx_v2_ingestor — market, news and cost-data ingestion and authorised
>   maintenance;
> - autofx_v2_app — normal application runtime access without
>   schema-administration privileges;
> - autofx_v2_readonly — analytics, research and audit access;
> - a separately controlled bootstrap/admin role used only where database or
>   role creation requires it.
>
> The final role names and privileges require specification and testing
> before production use.
>
> D. DATABASE SAFEGUARDS
>
> - V1 and V2 must be physically or logically separated.
> - No V2 command may target the V1 database.
> - Development, test, staging and production credentials must be separate.
> - All persistent schema changes must be represented by version-controlled
>   migrations.
> - Do not rely on undocumented manual schema changes.
> - Migrations require automated verification and an appropriate rollback or
>   forward-recovery plan.
> - Destructive development operations are permitted only after verifying
>   that the target is an isolated V2 development/test environment and the
>   affected data is recoverable or reproducible.
> - Production DROP, TRUNCATE, destructive bulk DELETE, irreversible
>   migration, restore or data-repair operations require explicit approval.
> - Production schema changes must use an approved deployment and migration
>   process.
> - Database credentials must remain outside Git.
> - Credentials must never be printed, echoed, documented or committed.
> - Material database operations must produce audit evidence.
> - Data repair must preserve lineage and record what changed, why, when and
>   under which rule.
> - Any database operation that creates additional cost requires prior
>   approval.
> - Backups, restoration testing, migration testing and integrity validation
>   must be included in the implementation.
>
> E. CURRENT DATABASE GATE
>
> This decision defines Claude's permitted operating model for future V2
> implementation.
>
> It does not itself open the current implementation gate.
>
> Do not create V2 databases, schemas, tables, indexes, migrations or
> application code until I provide the exact implementation-authorisation
> phrase for the relevant named phase.
>
> Q-002 — Existing cTrader cBot/bridge
>
> The relevant implementation is in the V1 repository:
>
> - code/TradingViewBridge.cs
> - related file: code/PriceBridge.cs
>
> Treat TradingViewBridge.cs as the primary cBot/bridge candidate for the V1
> forensic audit.
>
> The V1 file and class are named for TradingView. The V2 implementation
> should be renamed to describe its actual responsibility.
>
> Provisional naming candidates are:
>
> - CTraderExecutionBridge
> - AutoFXExecutionBridge
>
> Recommend the final name after auditing its responsibilities and
> dependencies.
>
> The existing TradingView bridge includes percentage weighting by symbol.
> AutoFX V2 does not need this per-symbol percentage-weighting feature.
>
> Requirements:
>
> - Verify and document the existing weighting behaviour during the V1
>   audit.
> - Do not carry per-symbol percentage weighting into V2.
> - Position sizing must follow the approved book, the trading account's
>   risk-per-trade configuration and the single authoritative sizing-engine
>   decision.
> - Do not modify V1.
> - Classify each relevant V1 component as REUSE, ADAPT, REJECT or UNKNOWN.
> - Any V2 implementation or removal occurs only after implementation
>   authorisation.
>
> AUTONOMOUS GITHUB CREATION AND PUSH — EXPLICITLY AUTHORISED
>
> I explicitly authorise creation of a new private GitHub repository:
>
> JDep8/AutoFX-V2
>
> This repository must remain completely separate from:
>
> JDep8/AutoFX
>
> This authorisation covers only:
>
> - committing the current Round A documentation and governance updates
>   after validation;
> - creating the private AutoFX V2 GitHub repository;
> - establishing the origin remote;
> - establishing main as the default branch;
> - pushing the validated V2 repository history;
> - pushing the planning/discovery-handoff branch.
>
> [Preconditions, GitHub requirements, and branch procedure recorded in
> DECISION_LOG.md D-024 — nine pre-creation verifications; private
> visibility; no remote-generated files; no paid features; no V1 content;
> no branch deletion; no history rewrite; no force-push; clean fast-forward
> of master to the validated planning/discovery-handoff state renamed to
> main; stop-and-report on any unexpected repository state.]
>
> FUTURE GIT OPERATING MODEL
>
> After the initial repository creation:
>
> - Claude may autonomously create commits and push validated work to an
>   explicitly approved discovery or implementation branch.
> - Claude must run the relevant tests, documentation validation and secret
>   checks before pushing.
> - No force pushes.
> - No direct merge into main without my explicit approval.
> - Prefer pull requests for merging approved phase work into main.
> - No live deployment occurs merely because changes have been pushed.
> - No paid GitHub feature may be enabled without my approval.

### Round A summary — 2026-08-18 *(historical; superseded later the same day by § Round A closure candidate below after the decision-reconciliation instruction)*

**Decisions captured (11):** D-001 (drawdown direction), D-008 (Jacob-only),
D-009 (eight-class universe, FX-first), D-010 (P1-full MVP) — batch 1;
D-018 (Australia, personal name, mandatory pre-commercialisation review
gate), D-019 (AUD 400/month ceiling, ~6-month paper target post-
authorisation, 5–10 h/week, autonomous operating model with twelve mandatory
stops, VPS not auto-approved), D-020 (twelve non-goals), D-021 (accuracy =
bands + distribution tests; values → Round F), D-022 (database access model
and role separation; V1 permanently read-only), D-023 (V1 bridge =
`code/TradingViewBridge.cs` + `PriceBridge.cs`; no per-symbol weighting in
V2), D-024 (GitHub remote + git operating model) — batch 2.

**Requirements changed:** new BUS-007…BUS-011, DATA-009, VAL-006/VAL-007,
SEC-004/SEC-005, EXEC-011, OPS-004/OPS-005 (all `OWNER_APPROVED`, evidence
USER-STATED); Q-dependencies on BUS-001/VAL-001 (Q-009) now point at D-021.

**Assumptions:** A-001…A-005 remain `PROPOSED`; A-006 (local-only git)
`SUPERSEDED` by D-024.

**Contradictions:** none new. Open: D-014/Q-011 (rules naming, non-blocking);
D-002…D-007 legacy conflicts assigned to later rounds.

**Risks / evidence required:** V1 DB credential provisioning outstanding
(D-022 remainder — limits DB-side audit depth until supplied); Q-010 holdout
contamination UNKNOWN (V1 audit + Round B); Q-005 drawdown numbers → Round E;
Q-003 consumer-AI automation BLOCKED; KPI framework proposed in
PROJECT_CHARTER.md § KPI framework — approval outstanding (Q-008
remainder); VPS production suitability unverified → Round N.

**Round completion (per the 2026-08-18 completion assessment,
DISCOVERY_STATUS.md):** Round A closes when its INCOMPLETE topics are
resolved — Q-015 (success hierarchy) answered and the KPI framework
approved or amended (Q-008 remainder) — **and** Jacob approves this
summary. Next: Round B (V1 outcomes and migration stance) — feeds from the
V1 forensic audit, which starts only on Jacob's explicit go
(NEXT_ACTIONS § B).

## Round A decision reconciliation — 2026-08-18 (owner instruction)

Jacob supplied a reconciliation instruction stating that the following
were "explained individually and explicitly agreed." Recorded as
`OWNER_APPROVED` · USER-STATED (full decision text in DECISION_LOG.md
D-025…D-035; key phrases preserved):

- **D-025** owner interaction rule — decisions one at a time; plain
  English; consequences + recommendation; *"'Noted' does not mean
  'approved.'"*; never combine approval questions; never reopen answered
  questions absent genuine new conflict.
- **D-026** repository-output rule — every substantive task persists its
  output in the repository; terminal-only output insufficient; sensitive
  material never committed to satisfy the rule; tasks end with
  validation, commit, and push unless Jacob says otherwise.
- **D-027** (Q-015) success hierarchy — safety/live-protection and
  evidence-integrity/fidelity are *"co-equal, non-negotiable hard
  constraints"*; profitability only inside them; cost/speed last; a
  safety-vs-evidence conflict is escalated, never silently weakened.
- **D-028** (Q-008) KPI framework approved at form level — 20 areas,
  organised headline/supporting; *no thresholds invented*; numbers stay
  with their named rounds.
- **D-021 confirmation** — backtest-accuracy values deferred to Round F;
  Round F researches and proposes tolerances/samples/confidence/warnings/
  failures/remediation for approval.
- **D-018 confirmation** — Australian/personal-name basis stands for
  discovery; entity/regulatory structure at the mandatory pre-live/
  pre-commercialisation review gate; *"not permission to trade
  commercially or provide financial services."*
- **D-029** VPS split — early basic facts allowed to avoid designing
  blindly; never assumed production-ready; suitability decided Round N;
  spending needs evidence + free alternatives + cost proposals.
- **D-022 classification confirmation** — `autofx_v1_readonly`
  provisioning blocks only the DB-side V1 audit; not Round A closure; not
  a separately authorised repo-side audit; no audit authorised by the
  instruction.
- **D-030** (Q-016) Rounds G/H paired — G designs methods/governance/
  multiple-testing protections; H applies holdout/regime/crisis evidence
  and owns final numbers and Gate 3 pass/fail; shared artefacts; *"the
  test must be designed before final holdout results are examined."*
- **D-031** (Q-011) rules layout — keep both sets; topic files
  authoritative; entry points link; repeated safety wording
  byte-identical with drift checks.
- **D-032** (Q-013) status vocabulary — lifecycle labels for governed
  items; descriptive progress states for headers/rounds/registers/gates/
  workflow, never implying tested/validated states.
- **D-033** (Q-014) visibility — temporarily public for independent
  ChatGPT review; back to private when an authenticated review path
  exists and Jacob explicitly authorises; public history is irrevocable;
  sensitivity stop-rule on every push; supersedes D-024's PRIVATE clause
  only.
- **D-034** trading simulation & certification requirement (P1) — Modes
  A/B/C as specified in
  TRADING_SIMULATION_AND_CERTIFICATION_SPEC.md; owner intent recorded
  verbatim there.
- **D-035** command-runbook v0.1.0 catalogue REJECTED (B-7 not approved);
  corrected v0.2.0 stays `PROPOSED` for one-at-a-time reapproval.

## Round A closure candidate — 2026-08-18 (**`OWNER_APPROVED` 2026-08-18 — Round A CLOSED**)

**Closure record (D-036):** Jacob approved this closure candidate on
2026-08-18 (evidence USER-STATED: "I approve the Round A closure
candidate. Close Round A as OWNER_APPROVED."). Round A is **CLOSED**. All
deferred matters below retain their assigned rounds. The approval does
not approve the command runbook (still `PROPOSED`, D-035), does not start
Round B or either V1 audit, and does not touch the no-build gate. The
candidate text is preserved unchanged below as approved.

**In plain English — what Round A decided:**

AutoFX V2 is built for one person: Jacob, trading his own money, from
Australia, under his personal name for now — with a mandatory Australian
legal review standing between today's work and any commercial step, ever.
The product's first job is honesty: safety of capital and integrity of
evidence are equal, untouchable constraints, and profit is only pursued
inside them; if the two ever pull against each other, the question comes
back to Jacob. The target universe is eight CFD classes rolled out FX
first; the implementation MVP is the full Priority 1 platform; the
Research Centre and content business stay planning-only until P1 proves
itself live.

The money and time box is set: at most AUD 400 a month, every expense
individually approved, free options first when quality allows; roughly
six months from an eventual implementation authorisation to a first
controlled paper-trading candidate (nine to twelve acceptable), and no
committed date for live trading. Jacob gives 5–10 hours a week as owner
and approver; Claude does the permitted technical work autonomously and
stops for the twelve mandatory decision triggers.

What "success" and "accurate" mean is now fixed in form: twelve non-goals
(no HFT, no discretionary routing, no profit promises, no gate-weakening,
and more); a 22-area KPI framework — headline measures for decisions,
supporting diagnostics underneath — with every numeric threshold
deliberately left to its later round; and backtest accuracy defined as
tolerance bands plus distribution tests, with the actual numbers to be
researched and approved in Round F. The platform must also prove itself
three ways before money is ever at risk: fast historical replay of real
production behaviour, a live shadow mode that can never place an external
order, and per-symbol certification on a designated cTrader demo account —
none of which claims live results will match demo, and none of which is
authorised to run today.

The machinery around the work is settled too: database access is designed
(V1 forever read-only; V2 autonomy only after the build gate), the V1
bridge is located for the future audit, the repository lives on GitHub
with strict push rules and is temporarily public by Jacob's decision, the
rulebook layout and status vocabulary are fixed, decisions come to Jacob
one at a time, and every task's output must land in the repository.

**What closing Round A does NOT do:** it does not start Round B or either
V1 audit; does not authorise wireframes, implementation, databases, or
trading; does not set any numeric threshold; does not approve the
command-runbook policies (rejected v0.1.0; corrected version awaits
separate approval); and does not touch the no-build gate, which remains
ACTIVE until the exact authorisation phrase.

**Deferred items and their owners:** drawdown numbers/heat cap/translation
rule → Round E (Q-005); accuracy tolerances and replay-fidelity criteria →
Round F; multiple-testing design → G, final acceptance numbers → H
(D-030); certification tolerances/expiry/remediation and Gate 7 criteria →
Round J (with N); VPS production suitability → Round N; holdout
contamination (Q-010) → V1 audit + Round B; consumer-AI automation
(Q-003) → BLOCKED pending legal; video boundary (Q-004) → Round L;
`autofx_v1_readonly` provisioning → Jacob, before the DB-side audit.

**The one closure question (asked separately per D-025):** does Jacob
approve this closure candidate, closing Round A? — **ANSWERED 2026-08-18:
approved (D-036).**
