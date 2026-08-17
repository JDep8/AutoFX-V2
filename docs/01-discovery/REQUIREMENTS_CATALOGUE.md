# Requirements Catalogue

- **Owner:** Jacob Depares (owner of every requirement below)
- **Status:** Living register — all items `PROPOSED` unless marked otherwise
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** DECISION_LOG.md, TRACEABILITY_MATRIX.md
- **Approval evidence:** Per-item; source "Owner brief 2026-08-17" = Jacob's V2 mandate; "Round A 2026-08-17" = explicit interview answer

Notes: acceptance criteria marked "→ Round X" are defined and owner-approved in
that round — a TBD acceptance criterion means the requirement is not yet
testable, never that it is accepted. Design/test references live in the
Traceability Matrix. Priorities: M = must, S = should.

## BUS — Business

| ID | Requirement (with rationale) | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|------------------------------|--------|-----|--------|---------|----------------------|-------|
| BUS-001 | Backtests are trustworthy indicators of realistic expectations under real trading conditions — the product's first commercial goal | Owner brief 2026-08-17 | M | PROPOSED | Q-009 | Measurable backtest-vs-live degradation tolerance defined and met → Round F | P1 |
| BUS-002 | Find and operate profitable portfolios within explicitly approved risk limits | Owner brief 2026-08-17 | M | PROPOSED | D-001 | Live books operate within approved caps; breaches trigger documented Gate 8 action | P1 |
| BUS-003 | Evidence and safety standards are hard constraints — never weakened to improve an apparent result | Owner brief 2026-08-17 | M | PROPOSED | — | Adversarial review finds no standard relaxed in favour of performance → Exit Review | All |
| BUS-004 | Profitability is never guaranteed; uncertainty, confidence intervals, and degradation are always reported | Owner brief 2026-08-17 | M | PROPOSED | — | Every performance artefact carries uncertainty measures | All |
| BUS-005 | Sole user is Jacob (personal capital); no customers/subscribers/copy-trading | Round A 2026-08-17 | M | **OWNER_APPROVED** | D-008 | n/a (scope decision) | All |
| BUS-006 | Implementation MVP = full Priority 1; P2/P3 planning-only until P1 live-validated | Round A 2026-08-17 | M | **OWNER_APPROVED** | D-010 | n/a (scope decision) | All |

## DATA — Data platform

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| DATA-001 | ≥5 years (target 10) of history for strategy and book testing | Owner brief 2026-08-17 | M | PROPOSED | D-002 | Coverage report per symbol/class meets approved depth → Gate 1 | P1 |
| DATA-002 | Greatest practical per-minute detail across the target period | Owner brief 2026-08-17 | M | PROPOSED | Round D | Granularity per class approved; truth lost at each level documented | P1 |
| DATA-003 | Price plus realistic trading costs captured: bid/ask spread, commission, slippage, swaps/financing, other execution-relevant costs | Owner brief 2026-08-17 | M | PROPOSED | Round D | Cost fields present and validated per approved data contract → Gate 1 | P1 |
| DATA-004 | Point-in-time fundamental/macro events (rate decisions, inflation releases, …) with scheduled+actual time, consensus, previous, revision vintage, surprise, region, severity, provenance | Owner brief 2026-08-17 | M | PROPOSED | Round D | Events keyed by actual release timestamp + vintage; PIT audit passes | P1 |
| DATA-005 | Automated checks for missing, duplicate, malformed, stale, inconsistent, out-of-order, suspicious data; quarantine before repair | Owner brief 2026-08-17 | M | PROPOSED | Round D | Quality thresholds + quarantine policy approved and demonstrated | P1 |
| DATA-006 | Continuous update and monitoring of prices, news, spreads, commissions, slippage observations, and all production inputs | Owner brief 2026-08-17 | M | PROPOSED | Round D | Freshness SLAs defined, monitored, alerting demonstrated | P1 |
| DATA-007 | FMP evaluated against the complete data contract — never assumed adequate | Owner brief 2026-08-17 | M | PROPOSED | A-004 | Dated evaluation vs contract, with gaps and fallbacks → Round D | Discovery |
| DATA-008 | Eight-class CFD universe designed-for from day one; per-class session/cost/gap models; phased rollout FX-first, each class gated on its data contract | Round A 2026-08-17 | M | **OWNER_APPROVED** (universe+phasing) | D-009 | Per-class contract passes Gate 1 before that class enters implementation | P1+ |

## QUANT — Quantitative research

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| QUANT-001 | Every strategy/configuration attempted is tracked so multiple-testing risk cannot be hidden | Owner brief 2026-08-17 | M | PROPOSED | Round G | Experiment registry captures full research breadth; audit reproduces counts | P1 |
| QUANT-002 | Strategies require an economic/microstructure rationale, not only a discovered pattern | Owner brief 2026-08-17 | M | PROPOSED | Round G | Rationale recorded and reviewed at Gate 3 | P1 |
| QUANT-003 | A data-period ledger records which dates served research/fitting/selection/stress vs untouched testing | Legacy conflict #2 | M | PROPOSED | D-002 | Ledger exists; final holdout provably selection-untouched → Round H | P1 |
| QUANT-004 | Truncation (early candidate elimination) is an explicit, owner-approved, visible policy | Legacy conflict #3 | M | PROPOSED | D-003 | Policy documented with effect measurement → Round G/H | P1 |

## VAL — Validation and fidelity

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| VAL-001 | Backtest-to-live fidelity is a core pillar with measurable degradation tolerances | Owner brief 2026-08-17 | M | PROPOSED | Q-009 | Tolerances approved (Round F); shadow/paper degradation inside them → Gate 6 | P1 |
| VAL-002 | Bid/ask execution (never mid-price); time-varying spread, commissions, swaps, slippage, latency, partial fills, rejections, lot rules, margin, conversions | Owner brief 2026-08-17 | M | PROPOSED | Round F | Backtest truth model approved; golden scenarios pass | P1 |
| VAL-003 | Deterministic reproducibility: immutable inputs, seeds, code/data/config hashes, event logs, exact reruns | Owner brief 2026-08-17 | M | PROPOSED | Round F | Any result exactly reproducible from recorded versions | P1 |
| VAL-004 | Crisis validation on measured historical episodes with explicit criteria; synthetic stresses complement, never replace | Legacy conflict #4 | M | PROPOSED | D-004 | Episodes chosen before outcomes seen; per-strategy + portfolio scores → Round H | P1 |
| VAL-005 | News/market-calendar exclusion is deterministic and replay-tested; news intelligence never substitutes | Legacy conflict #7 | M | PROPOSED | D-007 | Replay tests demonstrate enforcement incl. fail-closed on missing news | P1 |

## RISK — Risk and accounting

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| RISK-001 | User inputs: symbols, timeframes, max acceptable portfolio drawdown, risk per trade | Owner brief 2026-08-17 | M | PROPOSED | D-001 | Inputs drive generation and are recomputed independently of the optimiser | P1 |
| RISK-002 | Standard comparison configuration: USD 100,000 starting capital, 1% risk per trade | Owner brief 2026-08-17 | M | PROPOSED | D-001 | Every book also evaluated at the standard configuration | P1 |
| RISK-003 | Position risk compounds from current portfolio size based on closed positions | Owner brief 2026-08-17 | M | PROPOSED | Round E | Canonical sizing formula approved and shared by backtest/live | P1 |
| RISK-004 | Portfolio drawdown measured from prior portfolio peak, not starting capital | Owner brief 2026-08-17 | M | PROPOSED | D-001 | Canonical formula per Glossary; verified in golden scenarios | P1 |
| RISK-005 | Book-level cap applies to whole book; a constituent may exceed it alone only if book stays within cap — prominently flagged and separately risk-assessed | Owner brief 2026-08-17 | M | PROPOSED | D-001, D-005 | Flag + separate assessment visible in approval evidence pack | P1 |
| RISK-006 | Realised peak-relative drawdown is the canonical approval metric; MTM excursion and heat are separate always-visible live controls | Round A 2026-08-17 (D-001 direction) | M | **OWNER_APPROVED** (direction; numbers → Round E, Q-005) | D-001 | Round E signs off formulas + default numbers | P1 |
| RISK-007 | Each account has its own position-risk percentage | Owner brief 2026-08-17 | M | PROPOSED | Round J | Per-account overlay revalidated per live configuration | P1 |
| RISK-008 | USD accounts initially; documented path to multi-currency preserved | Owner brief 2026-08-17 | S | PROPOSED | A-001 | Multi-currency path documented in architecture, not blocked | P1 |

## EXEC — Execution and live safety

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| EXEC-001 | cTrader integration via its supported API messages (auth, discovery, symbols, quotes, orders, reconnects, idempotency) | Owner brief 2026-08-17 | M | PROPOSED | A-002, Round J | Integration spec approved; message flows replay-tested | P1 |
| EXEC-002 | Approved books disabled by default; live-marking is separate and links to multiple demo/live accounts | Owner brief 2026-08-17 | M | PROPOSED | Gate 5/7 | Activation requires version-specific explicit approval | P1 |
| EXEC-003 | Live engine uses live market and news inputs before entry and throughout monitoring | Owner brief 2026-08-17 | M | PROPOSED | Round J/K | Demonstrated in shadow/paper → Gate 6 | P1 |
| EXEC-004 | Every trade has a stop loss; if protection cannot attach atomically, fail-closed compensating sequence with maximum unprotected interval incl. immediate closure | Owner brief 2026-08-17 | M | PROPOSED | Round J | No unprotected position beyond approved interval, evidenced in paper/live logs | P1 |
| EXEC-005 | Every open trade (incl. with TP) actively monitored; controlled earlier exits possible; deterministic exit-reason hierarchy | Owner brief 2026-08-17 | M | PROPOSED | Round K | Monitor spec approved; exit reasons deterministic in replay | P1 |
| EXEC-006 | FX positions never open while FX market closed (incl. weekends); crypto sessions treated explicitly (maintenance, liquidity, gaps) | Owner brief 2026-08-17 | M | PROPOSED | D-007 | Forced-flattening replay tests pass per class | P1 |
| EXEC-007 | No trades opened or held through approved high-volatility news exclusion windows | Owner brief 2026-08-17 | M | PROPOSED | D-007 | Replay tests + live enforcement evidence | P1 |
| EXEC-008 | One authoritative sizing engine (AutoFX or Jacob's cBot); no double-sizing or divergent formulas | Owner brief 2026-08-17 | M | PROPOSED | Q-002, Round J | Single engine designated; parity test backtest↔live | P1 |
| EXEC-009 | Broker truth authoritative for live positions/orders/fills/balance/margin; continuous reconciliation with discrepancy handling | Legacy conflict #6 | M | PROPOSED | D-006 | Reconciliation spec approved; discrepancies alert and fail closed | P1 |
| EXEC-010 | Kill switches (global/environment/account/book/strategy/symbol) and fail-closed breakers demonstrably reachable at runtime | Owner brief + legacy #6 | M | PROPOSED | D-006 | Reachability demonstrated in paper before any live approval → Gate 6 | P1 |

## FR — Functional (platform)

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| FR-001 | Candidate-book approval workflow moving approved books to an Approved Books register | Owner brief 2026-08-17 | M | PROPOSED | Gate 4/5 | Version-specific, timestamped, expiring/reviewable approvals | P1 |
| FR-002 | Multi-day book-generation jobs: checkpoints, resumability, cancellation, deterministic seeds, status reporting | Owner brief 2026-08-17 | M | PROPOSED | A-003, Round I | Kill/resume mid-run reproduces identical results | P1 |
| FR-003 | "No suitable book" is a first-class, honest outcome — never force a book | Owner brief 2026-08-17 | M | PROPOSED | D-005 | Generation can end with zero candidates without error or coercion | P1 |
| FR-004 | Trade ledger documents every trade in painful detail: entry/exit reasons, monitor observations, all order/fill events, reproducible provenance | Owner brief 2026-08-17 | M | PROPOSED | Round K | Event-sourced record; any trade decision reproducible | P1 |
| FR-005 | Trading-account management across multiple demo and live accounts | Owner brief 2026-08-17 | M | PROPOSED | Round J | Multi-account fan-out with partial-failure handling | P1 |
| FR-006 | A book spans multiple strategies, symbols, and timeframes with an approved minimum-composition/diversity rule | Owner brief + legacy #5 | M | PROPOSED | D-005 | Minimum composition rule owner-approved → Round I | P1 |

## SEC — Security

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| SEC-001 | No credentials, tokens, account identifiers, or private data exposed or committed — anywhere, ever | Owner brief 2026-08-17 | M | PROPOSED | — | Pre-commit verification; audits find zero exposures | All |
| SEC-002 | All discovery database access is read-only and deliberately bounded (timeouts, sampling, schema-first) | Owner brief 2026-08-17 | M | PROPOSED | Q-001 | Read-only account; no writes/locks on production data | Discovery |
| SEC-003 | Environments, secrets management, RBAC, least privilege, encryption, audit, supply-chain policy, threat model specified before implementation | Owner brief 2026-08-17 | M | PROPOSED | Round N | SECURITY_AND_THREAT_MODEL.md owner-approved → Exit Review | P1 |

## OPS — Operations

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| OPS-001 | Production observability, alerting, incident response, and safe-state/restart rules for live trading | Owner brief 2026-08-17 | M | PROPOSED | Round J/N | Incident runbook exercised before live → Gate 7 | P1 |
| OPS-002 | Backup, recovery, and disaster-rebuild objectives for the data platform; restore tests | Owner brief 2026-08-17 | M | PROPOSED | Round D/N | RPO/RTO approved; restore demonstrated | P1 |
| OPS-003 | Failure recovery and resumability for all long-running jobs; session/checkpoint/resume discipline for the discovery work itself | Owner brief 2026-08-17 | M | PROPOSED | A-003 | Resume drill passes (also 19. of Exit Review) | All |

## UX — User experience

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| UX-001 | Demo/live environment, data freshness, broker connection, active risk, enabled/disabled status, kill-switch state are impossible to overlook | Owner brief 2026-08-17 | M | PROPOSED | Round O | Visual review checklist passes on wireframes | P1 |
| UX-002 | Book detail exposes assumptions, constituents, diversification, realised + MTM drawdown, heat, costs, regimes, crises, sensitivity, statistical evidence, failures, approval history | Owner brief 2026-08-17 | M | PROPOSED | Round O | Traceability: every listed element present in page spec | P1 |
| UX-003 | Page inventory and end-to-end flows defined before screens; wireframes gated by `AUTHORISE WIREFRAME ONLY` (mock data, no backend) | Owner brief 2026-08-17 | M | PROPOSED | Round O | IA approved before any wireframe work starts | P1 |

## RES — Deep Research Centre (planning-only until P1 live-validated)

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| RES-001 | Multi-model orchestration where it materially improves quality; model agreement is never equated with truth — source evidence + independent challenge pass required | Owner brief 2026-08-17 | S | PROPOSED | Round L | Provenance shows challenge pass on every consequential finding | P2 |
| RES-002 | Full research provenance: question, decision served, plan, prompts/versions, models/providers, tool calls, sources, citations, retrieval dates, reviewer, confidence, cost, approval status | Owner brief 2026-08-17 | M | PROPOSED | Round L | Catalogue entries carry all fields; no fabricated citations | P2 |
| RES-003 | Actual-trade review may recommend experiments but can never directly modify a live strategy or book | Owner brief 2026-08-17 | M | PROPOSED | Gate 8 | No write-path from research output to live configuration | P2 |
| RES-004 | Headless automation of paid consumer AI UIs is `BLOCKED` unless provider terms and Jacob's legal/security review explicitly permit it | Owner brief 2026-08-17 | M | PROPOSED | Q-003 | Dated terms research + explicit owner/legal sign-off before any design relies on it | P2 |

## CONTENT — Content and AI-media business (planning-only until P1 live-validated)

| ID | Requirement | Source | Pri | Status | Depends | Acceptance criterion | Phase |
|----|-------------|--------|-----|--------|---------|----------------------|-------|
| CONTENT-001 | Research-led content for YouTube long/shorts, TikTok, Facebook, Instagram with human approval before publish | Owner brief 2026-08-17 | S | PROPOSED | Round M | Approval gate in workflow; nothing auto-publishes | P3 |
| CONTENT-002 | Repeatable AI characters and brand assets with a character bible, consent/ownership, disclosure, version control | Owner brief 2026-08-17 | S | PROPOSED | Round M | Character bible exists; provider licensing verified before use | P3 |
| CONTENT-003 | Financial-promotion and performance-claim controls, risk/backtest disclosures, synthetic-media disclosure, provenance, recordkeeping, jurisdiction-specific legal review | Owner brief 2026-08-17 | M | PROPOSED | Q-006, Round M | Compliance checklist per jurisdiction owner-approved before first publish | P3 |
| CONTENT-004 | Scenario-based business plan: audience, value proposition, competition, operating model, build/buy, costs, revenue, CAC/LTV, break-even, risks, milestones, kill criteria | Owner brief 2026-08-17 | S | PROPOSED | Round M | BUSINESS_PLAN.md owner-approved | P3 |
