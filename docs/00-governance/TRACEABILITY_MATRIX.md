# Traceability Matrix

- **Owner:** Jacob Depares
- **Status:** Living register (seeded)
- **Version:** 0.3.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** REQUIREMENTS_CATALOGUE.md, DECISION_LOG.md
- **Approval evidence:** n/a (register)

Maps every requirement to its design home, evidence, status, and governing
decision. Seeded from the Requirements Catalogue (2026-08-17); design and
evidence references fill in as domain documents mature — a blank cell means
"not yet designed/tested", never "done".

| Requirement | Design reference (doc) | Test/evidence reference | Status | Decision(s) |
|-------------|------------------------|-------------------------|--------|-------------|
| BUS-001…BUS-011 | PROJECT_CHARTER.md, SCOPE_AND_PRIORITIES.md, 09-delivery/* | INTERVIEW_RECORD.md § Batch 2 answers (verbatim, 2026-08-18) | PROPOSED (BUS-005/006 OWNER_APPROVED via D-008/D-010; BUS-007…011 OWNER_APPROVED via D-018/D-019/D-020) | D-008, D-010, D-018, D-019, D-020 |
| DATA-001…DATA-009 | 04-data/* | INTERVIEW_RECORD.md § Batch 2 (DATA-009) | PROPOSED (DATA-008 OWNER_APPROVED via D-009; DATA-009 direction via D-022) | D-009, D-022 |
| QUANT-001…QUANT-004 | 05-research-and-validation/* | — | PROPOSED | D-002, D-003 |
| VAL-001…VAL-008 | 05-research-and-validation/*, BACKTEST_FIDELITY_SPEC.md, 06-execution-and-risk/TRADING_SIMULATION_AND_CERTIFICATION_SPEC.md (VAL-008) | INTERVIEW_RECORD.md § Batch 2 (VAL-006/007); D-034 record (VAL-008) | PROPOSED (VAL-006/007 form OWNER_APPROVED via D-021; VAL-008 intent OWNER_APPROVED via D-034; values → Rounds F/J) | D-004, D-007, D-021, D-034 |
| RISK-001…RISK-008 | 06-execution-and-risk/RISK_AND_DRAWDOWN_SPEC.md | — | PROPOSED (RISK-005/006 direction via D-001) | D-001, D-005 |
| EXEC-001…EXEC-014 | 06-execution-and-risk/* incl. TRADING_SIMULATION_AND_CERTIFICATION_SPEC.md (EXEC-012…014) | INTERVIEW_RECORD.md § Batch 2 (EXEC-011); D-034 record (EXEC-012…014) | PROPOSED (EXEC-011 OWNER_APPROVED via D-023; EXEC-012…014 intent OWNER_APPROVED via D-034, design values → Rounds F/J; V1 behaviour UNKNOWN until audited) | D-006, D-007, D-023, D-034 |
| FR-001…FR-006 | 02-product-and-ux/*, 06-execution-and-risk/* | — | PROPOSED | D-005, D-010 |
| SEC-001…SEC-005 | 03-architecture/SECURITY_AND_THREAT_MODEL.md | INTERVIEW_RECORD.md § Batch 2 (SEC-004/005) | PROPOSED (SEC-004 direction, SEC-005 OWNER_APPROVED via D-022) | D-022 |
| OPS-001…OPS-005 | 09-delivery/*, 06-execution-and-risk/INCIDENT_AND_RECOVERY_RUNBOOK.md | INTERVIEW_RECORD.md § Batch 2 (OPS-004/005) | PROPOSED (OPS-004 OWNER_APPROVED, OPS-005 direction via D-019) | A-003, D-019 |
| UX-001…UX-003 | 02-product-and-ux/* | — | PROPOSED | — |
| RES-001…RES-004 | 07-research-centre/* | — | PROPOSED (RES automation boundary BLOCKED per Q-003) | D-010 |
| CONTENT-001…CONTENT-004 | 08-content-and-business/* | — | PROPOSED | D-010 |

Governance artefacts (process controls, not product requirements):

| Artefact | Design reference | Evidence reference | Status | Decision(s) |
|----------|------------------|--------------------|--------|-------------|
| Model routing + acceptance governance (discovery) | MODEL_ROUTING_POLICY.md; .claude/skills/autofx-model-governor/SKILL.md; .claude/agents/autofx-*.md (4) | MODEL_ROUTING_POLICY.md § Package validation record (VERIFIED vs Claude Code 2.1.234, 2026-08-18); SESSION_LOG.md Session 4 | OWNER_APPROVED 2026-08-18 (package + validation results approved by Jacob) | D-012, D-017 |
| GitHub remote + git operating model | TOOLING_REGISTER.md § Git conventions; DECISION_LOG.md D-024 | SESSION_LOG.md Session 5 (creation + push verification); INTERVIEW_RECORD.md § Batch 2 (authorisation verbatim). Visibility now PUBLIC — recorded CONFLICT vs the D-024 PRIVATE clause, tracked Q-014 | OWNER_APPROVED 2026-08-18 (explicit written authorisation by Jacob) | D-024, Q-014 |
| KPI framework (measurement definitions, 22 items, headline/supporting) | PROJECT_CHARTER.md § KPI framework (incl. KPI → requirement-ID mapping table) | INTERVIEW_RECORD.md § Batch 2 (D-020 mandate); D-028 approval record; independent challenge review 2026-08-18 | **OWNER_APPROVED at form level (D-028, 2026-08-18)** — labels are measurement definitions, not requirement IDs; all numerical thresholds remain with Rounds D–N | D-019, D-020, D-021, D-028, D-034 |
| Owner interaction + repository-output rules | `.claude/rules/discovery-and-authorisation.md` § Owner interaction rule; `.claude/rules/documentation-and-traceability.md` § Repository-output rule | DECISION_LOG D-025/D-026 (owner instruction 2026-08-18) | OWNER_APPROVED 2026-08-18 | D-025, D-026 |
| Repository visibility decision | TOOLING_REGISTER.md § Repository visibility; DECISION_LOG D-033 (supersedes D-024 PRIVATE clause) | `gh` visibility verification 2026-08-18; owner instruction (USER-STATED) | OWNER_APPROVED 2026-08-18 (temporarily public; return-to-private on owner authorisation) | D-024, D-033 |
| Claude Code command runbook | CLAUDE_CODE_COMMAND_RUNBOOK.md (v0.2.0 + § 10 errata) | Official docs (raw commands page, 105 rows, 2026-08-18); local read-only verification; D-035 rejection record | v0.1.0 catalogue REJECTED by Jacob (D-035); v0.2.0 policies PROPOSED, one-at-a-time approval pending | D-035, D-012, D-025 |

Row-level (per-requirement) expansion happens as each domain round completes;
this seed intentionally groups by prefix to avoid fabricating detail.
