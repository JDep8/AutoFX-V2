# Assumption Register

- **Owner:** Jacob Depares
- **Status:** Living register
- **Version:** 0.1.1
- **Last reviewed:** 2026-08-18
- **Dependencies:** DECISION_LOG.md, QUESTION_REGISTER.md
- **Approval evidence:** Per-assumption

Provisional defaults are always `PROPOSED`, never treated as approved.
Uncertainty is never silently converted into an assumption — it is recorded
here or in the Question Register.

| ID | Assumption | Basis | Status | Risk if wrong | Review point |
|----|-----------|-------|--------|---------------|--------------|
| A-001 | V2 initially assumes USD-denominated accounts, preserving a documented path to multi-currency | Owner brief 2026-08-17 | PROPOSED | Sizing/conversion rework if non-USD accounts arrive early | Round E/J |
| A-002 | cTrader is the execution venue via its supported API messages | Owner brief 2026-08-17 | PROPOSED | Integration spec rework if broker/platform changes | Round J |
| A-003 | Book generation may run for several days → jobs must be checkpointed/resumable | Owner brief 2026-08-17 | PROPOSED | Orchestration redesign | Round I/N |
| A-004 | FMP is a candidate data source only; adequacy unproven until evaluated against the data contract | Owner brief 2026-08-17 | PROPOSED | Data platform rework if assumed and wrong | Round D / Gate 1 |
| A-005 | Ten years of minute-level history is the preferred target (five-year minimum) | Owner brief 2026-08-17 | PROPOSED | Storage/cost/licensing scale-up | Round D |
| A-006 | Git identity/hosting: V2 remains local-only until Jacob explicitly instructs a push/remote | Session 2026-08-17 | **SUPERSEDED 2026-08-18** → D-024: private remote `JDep8/AutoFX-V2` explicitly authorised by Jacob; pushes governed by the D-024 operating model (approved branches only, validation + secret checks first, no force-push, no unapproved main merges) | n/a (superseded) | n/a |
