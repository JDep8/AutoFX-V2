# Decision Log

- **Owner:** Jacob Depares
- **Status:** Living register
- **Version:** 0.3.0
- **Last reviewed:** 2026-08-18
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

---

## D-011 — Terminal is the primary workspace

- **Decision:** Claude Code in the terminal is the primary workspace for this
  engagement; Claude Desktop remains available for visual review and
  wireframes.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (owner handoff instruction;
  evidence class USER-STATED).
- **Affects:** session continuity, tooling (TOOLING_REGISTER.md),
  `.claude/rules/20-session-continuity.md`.

## D-012 — Model routing policy

- **Decision:** Main terminal sessions launch with
  `claude --model best --effort ultracode`; `/status` must resolve `best` to
  Fable and `/effort` must confirm Ultracode before critical work. Fable is
  required for critical judgment and acceptance; Opus handles substantial
  bounded reasoning; Sonnet handles deterministic work from approved
  specifications; Haiku is extraction/search/formatting only; uncertainty
  always escalates upward. Retained from the master prompt: never change
  models merely to evade a usage cap.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (owner handoff instruction;
  evidence class USER-STATED). Full policy: MODEL_ROUTING_POLICY.md.
- **Affects:** every session; acceptance quality.

## D-013 — Plugin policy

- **Decision:** Install now: product-management, claude-md-management,
  session-report. Deferred: data (until the read-only database decision,
  Q-001); design (at the wireframe round); engineering/security/LSP/review
  (only after implementation authorisation); marketing (Priority 3). Do not
  install ECC now.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (owner handoff instruction;
  evidence class USER-STATED). Register: TOOLING_REGISTER.md.
- **Affects:** tooling, no-build-gate hygiene.

## D-014 — Rules-file naming (recorded CONFLICT, resolution PROPOSED)

- **Conflict:** The master prompt (2026-08-17) requires six topic rule files
  (`discovery-and-authorisation.md`, `quantitative-evidence.md`,
  `data-integrity.md`, `execution-and-risk.md`, `security-and-secrets.md`,
  `documentation-and-traceability.md`). The terminal-handoff instruction
  (2026-08-18) requires three numbered files (`00-discovery-gate.md`,
  `10-evidence-and-traceability.md`, `20-session-continuity.md`). Sources:
  master prompt § Phase 0 vs handoff instruction § minimum scaffold.
- **Resolution applied (PROPOSED, not silently chosen as final):** both sets
  exist; the three numbered files are thin authoritative entry points that
  link into the six detailed topic files. No content was deleted.
- **Status:** `PROPOSED` — Jacob to confirm keep-both or direct a
  consolidation (tracked as Q-011). *[Pointer note, 2026-08-18: confirmed
  and closed by **D-031** (keep both; topic files authoritative; entry
  points link; repeated safety wording byte-identical). Q-011 RESOLVED.]*
- **Affects:** `.claude/rules/` layout only; no safety impact.

## D-015 — Environment-visible external tooling boundary

- **Context:** The first terminal session (2026-08-18, recovery audit finding
  F-3) found user/account-scope tooling visible in the session environment
  but not enabled by this repository: a Figma plugin (skills + MCP tools) and
  claude.ai connectors (HubSpot, Lucid, Microsoft 365, Productive.io, Thomax
  Knowledge Platform). Repo-scoped `.claude/settings.json` enables only the
  three D-013-approved plugins.
- **Decision:** Externally configured tooling is classified
  **ENVIRONMENT-VISIBLE / OUT-OF-SCOPE / NOT AUTHORISED FOR AUTOFX USE**.
  Do not authenticate, invoke, remove, or modify it. Figma remains deferred
  until the approved wireframe phase. Only project-scoped tools explicitly
  approved in TOOLING_REGISTER.md are authorised for AutoFX work.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (terminal recovery review, ruling
  on finding F-3; evidence class USER-STATED). Register: TOOLING_REGISTER.md.
- **Affects:** tooling governance, no-build-gate hygiene, session discipline.

## D-016 — Handoff files exempt from the six-field header rule

- **Context:** The recovery audit (2026-08-18, finding F-5) found the four
  `docs/handoffs/` files do not carry the six-field document header required
  by `.claude/rules/documentation-and-traceability.md`; they follow the
  handoff protocol's own schemas instead.
- **Decision:** `CURRENT_STATE.md`, `NEXT_ACTIONS.md`, `RESUME_PROMPT.md`,
  and `SESSION_LOG.md` are explicitly exempt from the six-field header rule;
  they must instead comply with their specific handoff schemas and required
  metadata.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (terminal recovery review, ruling
  on finding F-5; evidence class USER-STATED). Rule updated:
  `.claude/rules/documentation-and-traceability.md` § Document standard.
- **Affects:** documentation standard only; no safety impact.

## D-017 — Model-governance package precedes further discovery work

- **Context:** Owner instruction, 2026-08-18 (terminal recovery session,
  pre-commit governance correction). A project-local AutoFX model-governance
  package is specified in "Prompt 6A" of Jacob's migration runbook; that
  runbook is **not held in this repository** — its location/content is
  tracked as Q-012 and the dependency fails closed until supplied.
- **Decision:** After the recovery-reconciliation commit, the single first
  next action is the creation and validation of the project-local AutoFX
  model-governance package per Prompt 6A. Until that package is completed
  and `OWNER_APPROVED`, the following are prohibited: resuming Round A;
  beginning the V1 forensic audit; using subagents; accepting any critical
  discovery artifact.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (owner instruction; evidence
  class USER-STATED).
- **Package status:** specification supplied in-session (Q-012 RESOLVED);
  package created and validated against Claude Code 2.1.234; package and
  validation results **`OWNER_APPROVED` by Jacob 2026-08-18**. The D-017
  prerequisite is satisfied; Round A resumption and the V1 audit still wait
  on Jacob's separate inputs (NEXT_ACTIONS B-3/B-5). *[Pointer note,
  2026-08-18 later the same day: Round A subsequently resumed and batch 2
  was answered; NEXT_ACTIONS has been renumbered — the V1-audit go now
  lives in NEXT_ACTIONS § B. The original text above is preserved as the
  historical record.]*
- **Affects:** discovery sequencing, session discipline, subagent use,
  acceptance quality. Registers: QUESTION_REGISTER.md (Q-012);
  NEXT_ACTIONS.md § B-2.

## D-018 — Jurisdiction and trading entity (Q-006)

- **Decision:** Jacob is tax-resident in **Australia**. Discovery,
  development, backtesting, and paper trading are conducted under his
  **personal name**. Recorded explicitly as the current state, **not** the
  final production business structure.
- **Mandatory pre-live / pre-commercialisation gate:** an Australian legal,
  tax, financial-services, and financial-promotion review must occur before
  any of: live commercial trading through a business entity; accepting or
  managing external capital; copy trading; charging performance,
  subscription, or platform fees; selling trading signals, strategies, or
  research; monetising financial or trading content; publicly promoting
  expected trading returns.
- **Final entity structure:** deferred to that mandatory decision gate.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (Round A batch 2, Q-006; initial
  entity-only answer received first, full answer with jurisdiction and gate
  received the same day; both verbatim in INTERVIEW_RECORD.md § Batch 2).
  Evidence class USER-STATED. *[Confirmation note, 2026-08-18 (Round A
  reconciliation): Jacob explicitly re-confirmed this approach — discovery
  proceeds on the Australian/personal-name basis; final entity and
  regulatory structure deferred to the mandatory pre-live/
  pre-commercialisation Australian legal review gate. Complete for Round
  A; NOT permission to trade commercially or provide financial services.]*
- **Affects:** legal/compliance scope (Round M, CONTENT-003),
  PROJECT_CHARTER.md (BUS-007/BUS-008), P3 planning, live-enablement gating.

## D-019 — Budget, timeline, availability, and autonomous operating model (Q-007)

- **Budget:** operating ceiling **AUD 400/month**, excluding Claude, ChatGPT,
  and the existing VPS (already funded elsewhere). A ceiling, not a target.
  Free options preferred whenever they meet required quality, reliability,
  security, licensing, coverage, retention, and usage limits — never
  selected if they materially compromise backtest accuracy, data quality,
  security, maintainability, or production reliability. **Every** new
  expense requires Jacob's explicit prior approval (even within the
  ceiling), presented with free option, recommended option, price, benefits,
  limitations, and expected ongoing cost. No trial/service/subscription may
  auto-transition to paid. One-off/exceptional costs (historical data,
  specialist datasets, regulatory/legal advice) proposed separately. If
  required quality cannot be achieved within budget: present evidence,
  alternatives, and cost difference — never silently reduce quality.
- **Timeline:** first controlled paper-trading candidate targeted ≈6 months
  after implementation is explicitly authorised — a planning target that
  never overrides data-integrity, backtest-fidelity, security, risk, or
  acceptance gates; 9–12 months acceptable if required for trustworthy
  evidence. Live trading has **no committed date** and requires successful
  paper validation, execution validation, and separate explicit approval.
- **Availability / team:** Jacob ≈5–10 hours/week as product owner,
  decision-maker, and final human approver — not the technical operator (no
  manual coding, routine queries, or result-relaying). Claude performs
  permitted technical work autonomously; Claude/ChatGPT/other AI systems are
  tools, never accountable owners. No permanent human development team
  assumed. Specialist Australian legal, tax, regulatory, security,
  data-licensing, or quantitative advice proposed when the relevant gate
  requires it.
- **Autonomous working model — discovery:** maintain approved discovery and
  governance documentation; read-only repository inspections; authorised
  read-only database queries; approved research; documentation/traceability
  validation; documentation commits pushed to approved branches when
  specifically authorised.
- **Autonomous working model — after the exact implementation-authorisation
  phrase for a named phase:** write/refactor application code; create and
  run tests/validation; generate and execute permitted SQL; create/execute
  development migrations; build development infrastructure; inspect results
  and diagnose failures; create commits; push validated work to the approved
  phase branch; iterate until phase acceptance criteria are met or a genuine
  decision/blocker requires Jacob. No per-file/per-query/per-commit
  approvals within an approved phase.
- **Mandatory stops (always Jacob's decision):** any new expense; a major
  unresolved product or architecture decision; conflicting requirements;
  risk acceptance; legal or regulatory uncertainty; destructive production
  operations; changes to V1; live-trading enablement; production deployment;
  merging into main; publication or distribution of financial content; any
  decision outside the authorised phase.
- **Infrastructure:** existing VPS available and funded but **not**
  automatically approved as production infrastructure — inventory its
  specifications, OS, access model, security, capacity, backup, and recovery
  capability during infrastructure discovery. Current Windows computer =
  development/administrative infrastructure only. V2 designed portable,
  reproducible, backed up, and hosting-portable. No additional
  infrastructure purchases without approval.
- **Gate note:** these answers define the future operating model; they do
  **not** authorise application implementation. The no-build gate remains
  ACTIVE.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (verbatim in INTERVIEW_RECORD.md
  § Batch 2). Evidence class USER-STATED.
- **Affects:** DELIVERY_ROADMAP.md, OPERATING_COST_MODEL.md (Q-007
  dependency), operating model (OPS-004/OPS-005), session discipline,
  Round N infrastructure.

## D-020 — Non-goals (Q-008)

- **Decision:** twelve non-goals recorded:
  1. no high-frequency, ultra-low-latency, or latency-arbitrage trading;
  2. no routing of manually initiated discretionary trades — AutoFX executes
     approved, versioned books only;
  3. no guarantee of profitability or fixed returns;
  4. no live trading by default;
  5. no autonomous AI decision to enable live trading;
  6. no strategy approval based solely on an attractive historical backtest;
  7. no weakening of validation, data-quality, or risk gates to meet a
     deadline;
  8. no direct reuse of V1 code without evidence-based review;
  9. no external customer funds, paid signals, or copy trading in the
     initial scope;
  10. no content output that overstates or influences trading-research
      conclusions;
  11. no production deployment merely because code or a Git branch is
      complete;
  12. no silent acceptance of missing, contaminated, or insufficient
      evidence.
- **KPIs:** Claude may propose measurable KPI candidates in the appropriate
  discovery round; all final targets, thresholds, and pass/fail criteria
  require Jacob's approval.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (verbatim in INTERVIEW_RECORD.md
  § Batch 2). Evidence class USER-STATED.
- **Affects:** PROJECT_CHARTER.md (BUS-010), scope boundaries, acceptance
  gates, content compliance.

## D-021 — Backtest-accuracy form: tolerance bands + distribution tests (Q-009)

- **Decision:** option (c) — both mechanisms. **Tolerance bands** are the
  headline backtest/paper/live comparison across: net return; drawdown;
  risk-adjusted return; win rate (where statistically meaningful); trade
  frequency; average win and loss; holding time; realised spread;
  commission; swap/financing costs; slippage; cost per trade;
  missed/rejected trades; execution timing; fill quality. **Distribution and
  calibration tests** must confirm statistical consistency with expected
  backtest distributions and detect: execution degradation; market-regime
  changes; feature drift; strategy decay; cost-model drift; trade-frequency
  changes; unexpected tail behaviour; breakdown of cross-strategy or
  cross-symbol relationships.
- **Deferred to Round F:** final tolerance values, sample-size requirements,
  confidence levels, warning thresholds, failure thresholds, remediation
  rules.
- **Hard rule:** a strategy or book may not be declared accurate based only
  on headline return, correlation, or a small number of live trades.
- **Status:** `OWNER_APPROVED` (form) — 2026-08-18 (verbatim in
  INTERVIEW_RECORD.md § Batch 2). Evidence class USER-STATED.
  *[Confirmation note, 2026-08-18 (Round A reconciliation): Jacob
  explicitly approved deferring the exact numerical thresholds to Round
  F. Round A defines what must be measured; Round F must use research and
  evidence to propose the actual tolerances, sample sizes, confidence
  requirements, warnings, failures, and remediation rules for Jacob's
  approval.]*
- **Affects:** BACKTEST_FIDELITY_SPEC.md, BUS-001, VAL-001/VAL-006/VAL-007,
  Gates 6–7.

## D-022 — Database access model and role separation (Q-001)

- **A — V1 permanently read-only:** dedicated role, provisionally
  `autofx_v1_readonly`. Once secure access is configured, Claude may
  autonomously inspect schemas/metadata, generate and execute SELECT
  queries, inspect query plans, profile data quality, identify missing
  records/gaps/duplicates, analyse distributions, investigate lineage, and
  repeat/refine read-only queries without per-query approval — Jacob does
  not manually relay queries or results. No INSERT, UPDATE, DELETE, CREATE,
  ALTER, DROP, TRUNCATE, migration, repair, or administrative operation
  against V1, ever.
- **B — V2 development databases (post-authorisation only):** after the
  exact implementation-authorisation phrase for the relevant named phase,
  Claude may autonomously create and maintain **isolated** V2
  development/test databases — schemas, tables, columns, constraints,
  indexes, views/materialised views, functions/procedures where justified,
  partitioning/retention, development data, ingestion (market, news, cost,
  spread, commission, swap, slippage), deduplication and controlled
  repairs, migrations with rollback/forward-recovery procedures, seed/test
  data, query-performance work, disposable database recreation, and
  database tests — executing approved migration pipelines without Jacob
  running individual commands, and without per-object approvals.
- **C — Role separation (provisional, least-privilege):**
  `autofx_v1_readonly` (V1 audit only) · `autofx_v2_migrator` (V2
  migrations/controlled DDL) · `autofx_v2_ingestor` (data ingestion +
  authorised maintenance) · `autofx_v2_app` (runtime, no schema admin) ·
  `autofx_v2_readonly` (analytics/research/audit) · a separately controlled
  bootstrap/admin role used only where database/role creation requires it.
  Final names and privileges require specification and testing before
  production use.
- **D — Safeguards:** V1 and V2 physically or logically separated; no V2
  command may target the V1 database; separate credentials per
  dev/test/staging/production; all persistent schema changes as
  version-controlled migrations (no undocumented manual changes); automated
  migration verification plus rollback/forward-recovery plans; destructive
  development operations only after verifying an isolated V2 dev/test
  target with recoverable/reproducible data; production DROP, TRUNCATE,
  destructive bulk DELETE, irreversible migration, restore, or data-repair
  operations require explicit approval; production schema changes via an
  approved deployment/migration process; credentials outside Git, never
  printed/echoed/documented/committed; material operations produce audit
  evidence; repairs preserve lineage (what/why/when/rule); cost-creating
  operations require prior approval; backups, restore testing, migration
  testing, and integrity validation included in implementation.
- **E — Current gate:** defines the future operating model only; does not
  open the implementation gate. No V2 databases, schemas, tables, indexes,
  migrations, or application code until the exact
  implementation-authorisation phrase for the relevant named phase.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (verbatim in INTERVIEW_RECORD.md
  § Batch 2). Evidence class USER-STATED. **Operational remainder:** Jacob
  provisions `autofx_v1_readonly` and the secure configuration path (outside
  chat/repo) before the DB-side V1 audit can begin. *[Classification note,
  2026-08-18 (Round A reconciliation), confirmed by Jacob: provisioning
  blocks the **database-side** V1 audit only — it blocks neither Round A
  closure nor a separately authorised repository-side V1 audit. No audit
  is authorised by that confirmation. V1 remains permanently read-only;
  post-gate V2 development-database autonomy and separate production
  governance stand as written; credentials stay outside chat and the
  repository; Jacob does not manually run/paste ordinary queries once
  secure access is approved.]*
- **Affects:** SEC-002/SEC-004/SEC-005, DATA-009, V1 audit depth (Phase 1),
  Rounds D/N design, data-plugin gate (TOOLING_REGISTER.md).

## D-023 — V1 execution bridge location and V2 sizing boundary (Q-002)

- **Location:** V1 repository — `code/TradingViewBridge.cs` (primary
  cBot/bridge candidate for the V1 forensic audit) and related
  `code/PriceBridge.cs`.
- **V2 naming:** the V1 file/class are named for TradingView; the V2
  implementation will be renamed for its actual responsibility. Provisional
  candidates: `CTraderExecutionBridge`, `AutoFXExecutionBridge`. Final name
  recommended after the audit maps responsibilities and dependencies.
- **Weighting:** the existing bridge includes per-symbol percentage
  weighting; V2 does **not** need it. The audit must verify and document the
  existing behaviour; the feature is not carried into V2. Position sizing
  follows the approved book, the trading account's risk-per-trade
  configuration, and the single-authoritative-sizing-engine decision
  (EXEC-008, Round J).
- **Constraints:** do not modify V1; classify each relevant V1 component
  REUSE / ADAPT / REJECT / UNKNOWN (V1_REUSE_REGISTER.md); any V2
  implementation or removal only after implementation authorisation.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (verbatim in INTERVIEW_RECORD.md
  § Batch 2). Evidence class USER-STATED — the bridge's actual behaviour
  remains UNKNOWN until audited.
- **Affects:** Round J sizing decision (EXEC-008/EXEC-011),
  ACCOUNT_AND_SIZING_SPEC.md, V1_AUDIT.md scope, V1_REUSE_REGISTER.md.

## D-024 — GitHub remote, repository creation, and git operating model

- **Explicit one-time authorisation (2026-08-18):** create the private
  GitHub repository `JDep8/AutoFX-V2`, completely separate from
  `JDep8/AutoFX` (V1). Scope limited to: committing the Round A
  documentation/governance updates after validation; creating the private
  repository; establishing the `origin` remote; establishing `main` as the
  default branch; pushing the validated V2 repository history; pushing
  `planning/discovery-handoff`.
- **Preconditions (verified before creation/push):** working directory
  `C:\AutoFXV2.0`; model-governance package committed; git
  status/diff/consistency checks; clean secret scan; no credentials,
  datasets, connection files, V1 source, or prohibited artefacts tracked;
  `.gitignore` covers local secrets and generated private data; no existing
  `origin`; target repository does not already exist; `gh` authenticated as
  JDep8 with private-repo permission. Stop-and-report (never overwrite) if
  the repository exists, has unexpected content, is owned elsewhere, would
  require payment, or cannot be private.
- **Repository requirements:** PRIVATE; no remotely generated
  README/licence/gitignore; no paid GitHub features; no V1 content; no
  branch deletion; no history rewrite; no force-push; no credentials in
  commands, output, logs, or documentation.
- **Branch procedure:** confirm `master` is an ancestor of
  `planning/discovery-handoff`; only as a clean fast-forward, advance
  `master` to the validated `planning/discovery-handoff` state and rename it
  `main`; push `main` and `planning/discovery-handoff`; set `main` as the
  GitHub default; return the local working branch to
  `planning/discovery-handoff`; verify branches and private visibility;
  report the final URL.
- **Future git operating model (standing):** Claude may autonomously create
  commits and push validated work to an explicitly approved discovery or
  implementation branch, after running the relevant tests, documentation
  validation, and secret checks. No force pushes. No direct merge into
  `main` without Jacob's explicit approval — prefer pull requests for
  approved phase work. Pushing never implies deployment. No paid GitHub
  feature without approval.
- **Status:** `OWNER_APPROVED` — 2026-08-18 (explicit written authorisation;
  verbatim in INTERVIEW_RECORD.md § Batch 2). Evidence class USER-STATED;
  execution results and their verification are recorded in SESSION_LOG.md
  Session 5 as they occur.
- **Supersedes:** A-006 (git local-only default) — marked `SUPERSEDED` in
  ASSUMPTION_REGISTER.md.
- **Affects:** TOOLING_REGISTER.md § Git conventions, session continuity,
  push discipline, handoffs.
- *[Pointer note, 2026-08-18 later the same day: the repository was created
  PRIVATE as this decision requires and VERIFIED private at creation.
  Later that day its visibility became **PUBLIC** (VERIFIED via
  authenticated `gh`, metadata-only; the change was not made by Claude —
  Jacob states he made it, USER-STATED). This is a recorded **CONFLICT**
  between the standing PRIVATE requirement above and the current state,
  tracked as **Q-014** for Jacob's decision; no decision has superseded the
  PRIVATE clause. The original text above is preserved unchanged.]*
- *[Pointer note 2, 2026-08-18 (Round A reconciliation): the CONFLICT is
  resolved — **D-033** supersedes this decision's PRIVATE clause
  (temporarily public for external review; return to private on Jacob's
  explicit authorisation). All other D-024 git controls remain in force
  unchanged. Q-014 RESOLVED.]*

## D-025 — Owner interaction rule: one decision at a time

- **Decision (standing governance rule):** every owner decision or
  conflict is presented to Jacob **one at a time**, explained in plain
  English, with practical consequences and Claude's evidence-based
  recommendation. Approval is never silently inferred; **"noted" does not
  mean "approved."** Multiple approval questions are never combined into
  one response. Answered questions are never reopened unless new evidence
  creates a genuine conflict. A new conflict discovered mid-task is
  recorded, and one question is asked only after all safe,
  non-conflicting work is complete.
- **Status:** `OWNER_APPROVED` — 2026-08-18. Evidence class USER-STATED.
- **Affects:** interview method (`.claude/rules/discovery-and-authorisation.md`),
  every future approval interaction, NEXT_ACTIONS structure.

## D-026 — Repository-output persistence rule

- **Decision (standing governance rule):** every substantive Claude task
  persists its material output, decisions, evidence, traceability
  changes, and handoff state in the AutoFX V2 repository —
  terminal-only output is not sufficient. Secrets, credentials,
  connection files, raw private datasets, heap dumps, and other
  prohibited or sensitive material are never committed merely to satisfy
  this rule; if an expected output cannot safely be committed, stop and
  explain why. Each authorised documentation task ends with validation, a
  commit, and a push to the approved working branch unless Jacob
  explicitly says otherwise.
- **Status:** `OWNER_APPROVED` — 2026-08-18. Evidence class USER-STATED.
- **Affects:** session discipline
  (`.claude/rules/documentation-and-traceability.md`), handoff protocol,
  D-024/D-033 push practice.

## D-027 — Success hierarchy (resolves Q-015)

- **Decision:** (1) capital protection/live safety **and** evidence
  integrity/backtest fidelity are **co-equal, non-negotiable hard
  constraints**; (2) profitability is pursued only inside those
  constraints; (3) cost and delivery speed come after safety, evidence
  integrity, and constrained profitability. If safety and evidence
  integrity ever conflict, neither may be silently weakened — the
  conflict escalates to Jacob.
- **Status:** `OWNER_APPROVED` — 2026-08-18. Evidence class USER-STATED.
  Supersedes the `PROPOSED` (partly INFERRED) ranked ordering previously
  in PROJECT_CHARTER.md; charter updated.
- **Affects:** PROJECT_CHARTER.md § Success hierarchy, BUS-003/BUS-004,
  every acceptance-gate trade-off, Round A completion (topics 1 and 3).

## D-028 — KPI framework approved at form level (completes Q-008's framework component)

- **Decision:** the proposed 20 measurement areas are approved as the
  form-level KPI framework, organised as a concise set of **headline
  KPIs** for executive/product decisions with **supporting diagnostic and
  operational metrics** underneath. No numerical thresholds are invented:
  thresholds, confidence requirements, minimum samples, and
  warning/failure bands remain assigned to their named later discovery
  rounds.
- **Status:** `OWNER_APPROVED` (form level) — 2026-08-18. Evidence class
  USER-STATED. Charter reorganised accordingly (headline vs supporting;
  KPI-21/22 added later the same day under D-034's simulation
  requirement).
- **Affects:** PROJECT_CHARTER.md § KPI framework, Q-008, Round A
  completion (topic 12), Rounds D–N threshold ownership.

## D-029 — VPS assessment split

- **Decision:** basic facts about the existing VPS may be collected
  earlier when required to avoid designing blindly; the VPS is **not**
  assumed production-ready; formal production suitability is decided in
  Round N after assessing performance, security, reliability, backups,
  recovery, monitoring, storage, network stability, and cTrader
  connectivity; any upgrade, replacement, or paid service requires a
  proposal showing evidence, free alternatives, and cost before Jacob
  approves spending (per D-019 budget governance).
- **Status:** `OWNER_APPROVED` — 2026-08-18. Evidence class USER-STATED.
- **Affects:** OPS-005, D-019 infrastructure stance, Round N matrix entry.

## D-030 — Rounds G and H are a paired sequence (resolves Q-016)

- **Decision:** Round G designs the statistical-validation methods,
  experiment governance, multiple-testing protections, and draft
  strategy-acceptance methodology; Round H applies the untouched holdout,
  regime, and crisis evidence and sets the final numerical thresholds and
  Gate 3 pass/fail criteria. `STATISTICAL_VALIDATION_PLAN.md` and
  `STRATEGY_ACCEPTANCE_CRITERIA.md` are shared across both rounds; Round
  H owns their final numerical acceptance criteria and final approval.
  **The test must be designed before final holdout results are
  examined.**
- **Status:** `OWNER_APPROVED` — 2026-08-18. Evidence class USER-STATED.
- **Affects:** DISCOVERY_STATUS.md assurance matrix (G/H), the two shared
  artefacts, leakage/holdout discipline (QUANT-003), Q-016.

## D-031 — Rules-file layout: keep both, one source of truth (resolves Q-011, closes D-014)

- **Decision:** keep both rule-file structures. The three numbered files
  remain concise entry points and operating checklists; the six detailed
  topic files remain the **authoritative** rule definitions; entry points
  link to detailed rules instead of substantially duplicating them. Any
  unavoidable repeated safety wording — including the implementation gate
  phrase — must remain **byte-identical** and be checked for drift. No
  rule may have two competing authoritative definitions.
- **Status:** `OWNER_APPROVED` — 2026-08-18. Evidence class USER-STATED.
  D-014's `PROPOSED` resolution is hereby confirmed and closed.
- **Affects:** `.claude/rules/` layout, documentation standard,
  consistency checks (gate byte-identity sweep added to validation).

## D-032 — Status-vocabulary scope (resolves Q-013)

- **Decision:** the formal lifecycle vocabulary (`PROPOSED`,
  `OWNER_APPROVED`, `IMPLEMENTED`, `TESTED`, `PAPER_VALIDATED`,
  `LIVE_VALIDATED`, `REJECTED`, `SUPERSEDED`) applies to **governed
  items** — requirements, decisions, strategies, books, implementation
  components, tests, and validation evidence. Clear descriptive progress
  states (e.g. `Living register`, `In progress`, `Complete`, `Gated`,
  `Paused`) are permitted for document headers, discovery rounds,
  registers, gates, and operational workflow status. A descriptive state
  must never imply `IMPLEMENTED`, `TESTED`, `PAPER_VALIDATED`, or
  `LIVE_VALIDATED`; documents must distinguish their own document status
  from the lifecycle status of governed items inside them.
- **Status:** `OWNER_APPROVED` — 2026-08-18. Evidence class USER-STATED.
- **Affects:** CLAUDE.md § Status vocabulary,
  `.claude/rules/10-evidence-and-traceability.md`,
  `.claude/rules/documentation-and-traceability.md`, Q-013.

## D-033 — Repository visibility: temporarily public (resolves Q-014; supersedes D-024's PRIVATE clause)

- **Decision:** the repository is **temporarily public** so ChatGPT can
  independently review committed project outputs. Visibility is not
  changed in this task. It returns to private after an authenticated
  review path is available **and Jacob explicitly authorises the
  change**. Already-public history cannot be made confidential
  retroactively. Strict secret and sensitivity checks continue before
  every push. If later-round content would expose dangerous security
  details, credentials, protected strategy IP, or legally sensitive
  material, Claude stops and raises one owner decision before committing
  it publicly. This decision supersedes the incompatible PRIVATE clause
  in D-024 while preserving all other D-024 git controls.
- **Status:** `OWNER_APPROVED` — 2026-08-18. Evidence class USER-STATED.
- **Affects:** D-024 (clause superseded), TOOLING_REGISTER § Repository
  visibility, Q-014, per-push sensitivity discipline.

## D-034 — Trading simulation and certification requirement (three modes, P1)

- **Decision:** AutoFX V2 requires three distinct simulation/certification
  modes as an owner-approved **product requirement** (not merely a KPI):
  **Mode A** accelerated historical execution replay (production
  behaviour against point-in-time history through the broker-neutral
  contract into an internal simulated broker; no look-ahead;
  deterministic; painful-detail audit; faster than real time with
  fidelity never weakened for speed); **Mode B** live shadow simulation
  (live inputs, order instructions routed only to the internal simulator,
  never an external order; degradation evidence retained; accidental
  routing to live/demo fails closed); **Mode C** cTrader demo-account
  certification (designated demo account; per-symbol minimum-risk test
  trades verifying the full owner-specified checklist incl. proof no
  order reached a live account; respects market closures and news
  safeguards; book approval never itself triggers a demo order; demo
  success proves wiring/calculations, not live-equivalence). Replay
  supplements backtesting and is never profitability evidence.
- **Priority:** P1 (within the D-010 full-P1 platform; no priority
  conflict identified).
- **Status:** `OWNER_APPROVED` (requirement intent) — 2026-08-18.
  Evidence class USER-STATED. Design details `PROPOSED` in
  TRADING_SIMULATION_AND_CERTIFICATION_SPEC.md; unresolved design matters
  (price tolerance, minimum test size, certification expiry, retest
  triggers, failure remediation, evidence retention) recorded for Rounds
  F/J/K/N — not decided.
- **Affects:** EXEC-012/013/014, VAL-008, KPI-21/22, Gates 5–7,
  Rounds F/J/K/N, 06-execution-and-risk documents,
  TEST_AND_EVIDENCE_STRATEGY.md.

## D-035 — Command-runbook v0.1.0 catalogue REJECTED; corrected version requires separate approval

- **Decision:** Jacob rejects approval item B-7 in its v0.1.0 form because
  the underlying catalogue contained factual errors (see runbook § 10
  errata — e.g. `/reload-skills` wrongly marked unavailable,
  `/usage-credits` wrongly classified read-only, omitted commands,
  conflated evidence axes). The corrected runbook (v0.2.0, correction
  pass 2026-08-18 against the full official catalogue) remains
  `PROPOSED`; its policies return to Jacob for **separate, one-at-a-time
  approval** per D-025. B-7 is NOT approved.
- **Status:** `OWNER_APPROVED` (the rejection and reapproval requirement)
  — 2026-08-18. Evidence class USER-STATED.
- **Affects:** CLAUDE_CODE_COMMAND_RUNBOOK.md, NEXT_ACTIONS § B,
  TOOLING_REGISTER § Claude Code command governance.
