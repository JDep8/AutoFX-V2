# Traceability Matrix

- **Owner:** Jacob Depares
- **Status:** Living register (seeded)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** REQUIREMENTS_CATALOGUE.md, DECISION_LOG.md
- **Approval evidence:** n/a (register)

Maps every requirement to its design home, evidence, status, and governing
decision. Seeded from the Requirements Catalogue (2026-08-17); design and
evidence references fill in as domain documents mature — a blank cell means
"not yet designed/tested", never "done".

| Requirement | Design reference (doc) | Test/evidence reference | Status | Decision(s) |
|-------------|------------------------|-------------------------|--------|-------------|
| BUS-001…BUS-006 | PROJECT_CHARTER.md, SCOPE_AND_PRIORITIES.md | — | PROPOSED (BUS-005/006 OWNER_APPROVED via D-008/D-010) | D-008, D-010 |
| DATA-001…DATA-008 | 04-data/* | — | PROPOSED | D-009 |
| QUANT-001…QUANT-004 | 05-research-and-validation/* | — | PROPOSED | D-002, D-003 |
| VAL-001…VAL-005 | 05-research-and-validation/* | — | PROPOSED | D-004, D-007 |
| RISK-001…RISK-008 | 06-execution-and-risk/RISK_AND_DRAWDOWN_SPEC.md | — | PROPOSED (RISK-005/006 direction via D-001) | D-001, D-005 |
| EXEC-001…EXEC-010 | 06-execution-and-risk/* | — | PROPOSED | D-006, D-007 |
| FR-001…FR-006 | 02-product-and-ux/*, 06-execution-and-risk/* | — | PROPOSED | D-005, D-010 |
| SEC-001…SEC-003 | 03-architecture/SECURITY_AND_THREAT_MODEL.md | — | PROPOSED | — |
| OPS-001…OPS-003 | 09-delivery/*, 06-execution-and-risk/INCIDENT_AND_RECOVERY_RUNBOOK.md | — | PROPOSED | A-003 |
| UX-001…UX-003 | 02-product-and-ux/* | — | PROPOSED | — |
| RES-001…RES-004 | 07-research-centre/* | — | PROPOSED (RES automation boundary BLOCKED per Q-003) | D-010 |
| CONTENT-001…CONTENT-004 | 08-content-and-business/* | — | PROPOSED | D-010 |

Row-level (per-requirement) expansion happens as each domain round completes;
this seed intentionally groups by prefix to avoid fabricating detail.
