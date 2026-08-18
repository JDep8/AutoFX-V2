# Decision Log

- **Owner:** Jacob Depares
- **Status:** Living register
- **Version:** 0.1.1
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
  consolidation (tracked as Q-011).
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
  on Jacob's separate inputs (NEXT_ACTIONS B-3/B-5).
- **Affects:** discovery sequencing, session discipline, subagent use,
  acceptance quality. Registers: QUESTION_REGISTER.md (Q-012);
  NEXT_ACTIONS.md § B-2.
