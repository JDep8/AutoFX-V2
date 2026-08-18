# Document Index

- **Owner:** Jacob Depares
- **Status:** Living register — the navigation map; read this first each session
- **Version:** 0.2.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** every document below
- **Approval evidence:** n/a (register)

All documents are `PROPOSED` skeletons dated 2026-08-17 unless a status is
noted. Read only what the active task needs.

## Root

| File | Purpose |
|------|---------|
| [CLAUDE.md](../../CLAUDE.md) | Project constitution: no-build gate, authority hierarchy, quality gates, workspace/model/plugin policies, links |
| `.claude/settings.json` | Committed project permissions (read-only git/gh allowlist, V1-inspection scope; secret-file reads denied) + the three enabled discovery plugins (D-013). D-024 git/GitHub operations run under per-session approvals — allowlist extension is a separately reviewable change (TOOLING_REGISTER § Git conventions) |
| `.gitignore` | Ignore rules blocking secret patterns and local artefacts (a backstop, not a licence — see security rules) |
| `.claude/rules/00-…, 10-…, 20-…` | Numbered entry points: discovery gate, evidence + traceability labels, session continuity (D-014/Q-011: naming overlap with the six topic files awaits Jacob) |
| `.claude/rules/` (6 topic files) | Detail: discovery/authorisation, quantitative evidence, data integrity, execution/risk, security/secrets, documentation/traceability |
| `.claude/skills/autofx-model-governor/SKILL.md` | Model-routing governor skill (D-017): task classification, lowest-permitted-model selection, escalation + Fable acceptance discipline |
| `.claude/agents/` (4 discovery agents) | autofx-fable-critical-governor · autofx-opus-reviewer · autofx-sonnet-analyst · autofx-haiku-extractor — all read-only (Read/Glob/Grep), plan mode (D-017; roster in TOOLING_REGISTER.md) |

## 00-governance

| File | Purpose |
|------|---------|
| DOCUMENT_INDEX.md | This navigation map |
| [PROJECT_CHARTER.md](PROJECT_CHARTER.md) | Mission, owner, priorities; KPIs/non-goals pending Round A |
| [GLOSSARY.md](GLOSSARY.md) | Canonical terms, plain + technical; formulas finalised Round E |
| [DECISION_LOG.md](DECISION_LOG.md) | D-001…D-024 — legacy conflicts, Round A decisions (both batches), workspace/tooling policies, governance rulings, git/GitHub model |
| [ASSUMPTION_REGISTER.md](ASSUMPTION_REGISTER.md) | A-001…A-006 provisional defaults (A-006 `SUPERSEDED` by D-024) |
| [QUESTION_REGISTER.md](QUESTION_REGISTER.md) | Q-001…Q-013 (Q-001/002/006–009 resolved 2026-08-18 per D-018…D-023; Q-003 BLOCKED; Q-004/005/010/011/013 open) |
| [CHANGE_CONTROL.md](CHANGE_CONTROL.md) | How approved content changes without erasing history |
| [TRACEABILITY_MATRIX.md](TRACEABILITY_MATRIX.md) | Requirement → design → evidence → status → decision |
| [TOOLING_REGISTER.md](TOOLING_REGISTER.md) | Workspace roles (terminal primary), plugin install gates, git/GitHub conventions incl. private remote `JDep8/AutoFX-V2` (D-011/D-013/D-015/D-024) |
| [MODEL_ROUTING_POLICY.md](MODEL_ROUTING_POLICY.md) | Launch flags, Fable/Opus/Sonnet/Haiku routing, upward escalation (D-012) |

## 01-discovery

| File | Purpose |
|------|---------|
| [DISCOVERY_STATUS.md](../01-discovery/DISCOVERY_STATUS.md) | Phase + round A–O status; verified facts |
| [INTERVIEW_RECORD.md](../01-discovery/INTERVIEW_RECORD.md) | Verbatim interview record (Round A batches 1+2 answered; batch 2 answers verbatim 2026-08-18; Round A summary `PROPOSED`) |
| [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) | ~50 ID'd requirements from the owner brief + Round A |
| [SCOPE_AND_PRIORITIES.md](../01-discovery/SCOPE_AND_PRIORITIES.md) | P1/P2/P3 boundaries; asset universe (D-009) |
| [USER_ROLES_AND_JOURNEYS.md](../01-discovery/USER_ROLES_AND_JOURNEYS.md) | Sole-user role model + journey inventory |
| [V1_AUDIT.md](../01-discovery/V1_AUDIT.md) | Read-only V1 forensic audit (access verified; findings pending) |
| [V1_REUSE_REGISTER.md](../01-discovery/V1_REUSE_REGISTER.md) | Per-asset REUSE_AS_IS…UNKNOWN classifications |

## 02-product-and-ux

| File | Purpose |
|------|---------|
| PRODUCT_REQUIREMENTS.md | Product-level view over catalogue IDs |
| INFORMATION_ARCHITECTURE.md | Page inventory (16 areas) and navigation model → Round O |
| PAGE_AND_WORKFLOW_SPEC.md | Per-page content + end-to-end flows → Round O |
| WIREFRAME_REVIEW.md | Visual self-review + journey traceability checklist; gate `AUTHORISE WIREFRAME ONLY` |

## 03-architecture

| File | Purpose |
|------|---------|
| SYSTEM_CONTEXT.md | External actors/systems and P1 boundary |
| LOGICAL_ARCHITECTURE.md | Modular service boundaries → Round N |
| SERVICE_AND_EVENT_CATALOGUE.md | Services + events inventory → Round N |
| INTEGRATION_CONTRACTS.md | External interface contracts (cTrader, data, news) |
| SECURITY_AND_THREAT_MODEL.md | Secrets, RBAC, encryption, threat model → Round N |
| ADR_INDEX.md | ADR template + index (empty; first ADRs Round N/J) |

## 04-data

| File | Purpose |
|------|---------|
| DATA_SOURCE_REGISTER.md | Provider evaluation vs data contract (FMP = candidate only) → Round D |
| DATA_LICENSING_AND_RETENTION.md | Licences, redistribution, retention → Round D |
| POINT_IN_TIME_DATA_POLICY.md | Release-timestamp/vintage keying; no lookahead → Round D |
| CANONICAL_DATA_MODEL.md | Entities, fields, granularity per class → Round D |
| DATA_QUALITY_AND_QUARANTINE.md | Quality checks, quarantine-before-repair → Round D |
| DATA_LINEAGE_AND_VERSIONING.md | Immutable versions, hashing, rebuildability → Round D |
| MARKET_AND_NEWS_CALENDARS.md | Sessions, DST, weekend flattening, fail-closed news windows (D-007) → Rounds C/D |
| BACKUP_RECOVERY_AND_REBUILD.md | RPO/RTO, restore tests → Rounds D/N |

## 05-research-and-validation

| File | Purpose |
|------|---------|
| RESEARCH_PROTOCOL.md | Hypothesis-first research method (QUANT-001/002) → Round G |
| STRATEGY_TAXONOMY.md | Strategy families to research before selection → Round G |
| EXPERIMENT_REGISTRY_SPEC.md | Immutable experiments; multiple-testing accounting → Round G |
| LEAKAGE_AND_HOLDOUT_POLICY.md | Data-period ledger; locked holdout (D-002, Q-010) → Round H |
| BACKTEST_FIDELITY_SPEC.md | One deterministic lifecycle; bid/ask; conservative intrabar policy → Round F |
| STATISTICAL_VALIDATION_PLAN.md | Nested validation; PBO/DSR/RC/SPA candidates with limitations → Round G |
| CRISIS_AND_STRESS_FRAMEWORK.md | Measured episodes + synthetic complements; worst-period servicing (D-004) → Round H |
| STRATEGY_ACCEPTANCE_CRITERIA.md | Gate 3 criteria; truncation visibility (D-003) → Rounds G/H |
| BOOK_ACCEPTANCE_CRITERIA.md | Gate 4; minimum composition, no-suitable-book (D-005) → Round I |
| MODEL_GOVERNANCE.md | ML lifecycle; no live self-modification → Round G |

## 06-execution-and-risk

| File | Purpose |
|------|---------|
| RISK_AND_DRAWDOWN_SPEC.md | Canonical accounting per D-001 direction; numbers → Round E (Q-005) |
| ACCOUNT_AND_SIZING_SPEC.md | One authoritative sizing engine (EXEC-008, Q-002) → Rounds E/J |
| ORDER_AND_FILL_LIFECYCLE.md | Order types, SL attachment atomicity, fail-closed protection (EXEC-004) → Round J |
| CTRADER_INTEGRATION_SPEC.md | cTrader API flows, multi-account fan-out, demo/live labelling → Round J |
| OPEN_TRADE_MONITOR_SPEC.md | Monitoring signals, deterministic exit hierarchy → Round K |
| BROKER_RECONCILIATION.md | Broker-truth reconciliation, orphaned positions (EXEC-009) → Round J |
| CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md | Six-scope switches, fail-closed breakers (EXEC-010) → Round J |
| INCIDENT_AND_RECOVERY_RUNBOOK.md | Incident declaration, safe state, restart evidence → Rounds J/N |

## 07-research-centre (P2 — planning-only)

| File | Purpose |
|------|---------|
| RESEARCH_CENTRE_PRODUCT_SPEC.md | Intake, roles, budgets, ideas backlog → Round L |
| MODEL_AND_PROVIDER_GOVERNANCE.md | Provider selection; consumer-UI automation `BLOCKED` (Q-003) → Round L |
| RESEARCH_PROVENANCE_AND_EVALUATION.md | Full provenance model; fact/inference separation → Round L |
| TRADE_REVIEW_WORKFLOW.md | Trade review recommends, never modifies live (RES-003) → Round L |
| VIDEO_AND_EXTERNAL_CONTENT_POLICY.md | Lawful video-content access; compliant fallbacks (Q-004) → Round L |
| KNOWLEDGE_CATALOGUE_SPEC.md | Durable findings catalogue → Round L |

## 08-content-and-business (P3 — planning-only)

| File | Purpose |
|------|---------|
| CONTENT_STUDIO_PRODUCT_SPEC.md | Research-to-publish workflow with human approval → Round M |
| AI_CHARACTER_AND_BRAND_SPEC.md | Character bible; no vendor hard-coding → Round M |
| CONTENT_COMPLIANCE_AND_APPROVAL.md | Fin-prom, synthetic-media disclosure, likeness/copyright → Round M (Q-006) |
| CHANNEL_PUBLISHING_PLAN.md | Platform permissions, approval gates, analytics → Round M |
| BUSINESS_PLAN.md | Scenario-based plan with kill criteria → Round M |

## 09-delivery

| File | Purpose |
|------|---------|
| DELIVERY_ROADMAP.md | Staged roadmap; history-preserving backlogs → Round N (Q-007) |
| WORK_BREAKDOWN_AND_DEPENDENCIES.md | Dependency graph, critical path → Rounds B–O |
| TEST_AND_EVIDENCE_STRATEGY.md | Gates 1–8 mapped to test types → Rounds F/N |
| ENVIRONMENT_AND_RELEASE_PLAN.md | Environments, staged live ramp (Gate 7) → Round N |
| OPERATING_COST_MODEL.md | Cost scenario ranges → Rounds D/N (Q-007) |
| IMPLEMENTATION_READINESS_REVIEW.md | Exit Review 20-item checklist + adversarial self-review; READY/CONDITIONALLY_READY/NOT_READY |

## handoffs

| File | Purpose |
|------|---------|
| CURRENT_STATE.md | Phase, last checkpoint, verified facts, partial work |
| NEXT_ACTIONS.md | Exact next action first, then ordered follow-ups |
| RESUME_PROMPT.md | Copy/paste prompt for a fresh session |
| SESSION_LOG.md | Append-only chronology |

## wireframes/

Gated: empty until IA approval + `AUTHORISE WIREFRAME ONLY` (see its README).

## Diagrams (planned minimum set — Mermaid, owned by the named document)

1. End-to-end data lineage → DATA_LINEAGE_AND_VERSIONING.md
2. Strategy research and experiment lifecycle → EXPERIMENT_REGISTRY_SPEC.md
3. Book generation and approval flow → BOOK_ACCEPTANCE_CRITERIA.md
4. Shadow/paper/live promotion state machine → TEST_AND_EVIDENCE_STRATEGY.md
5. cTrader order/fill/reconciliation sequence → CTRADER_INTEGRATION_SPEC.md
6. Open-trade monitoring and exit flow → OPEN_TRADE_MONITOR_SPEC.md
7. Incident/kill-switch flow → CIRCUIT_BREAKERS_AND_KILL_SWITCHES.md
8. Research Centre orchestration and approval → RESEARCH_CENTRE_PRODUCT_SPEC.md
9. Content research-to-publish flow → CONTENT_STUDIO_PRODUCT_SPEC.md
10. Session/checkpoint/resume flow → handoffs (documentation-and-traceability rule)
