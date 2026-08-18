# Question Register

- **Owner:** Jacob Depares
- **Status:** Living register
- **Version:** 0.1.2
- **Last reviewed:** 2026-08-18
- **Dependencies:** DECISION_LOG.md, ASSUMPTION_REGISTER.md
- **Approval evidence:** n/a (register)

Safety-critical ambiguity fails closed and lands here as a blocking question.
`BLOCKED` marks items that halt dependent work until resolved.

| ID | Question | Raised | Blocks | Status | Resolution path |
|----|----------|--------|--------|--------|-----------------|
| Q-001 | Secure path for a dedicated **read-only** V1 PostgreSQL account (host, credential delivery outside chat/repo)? | 2026-08-17 | Depth of Phase 1 V1 audit (schema/data lessons) | OPEN | Jacob to provide via secure channel; see `.claude/rules/security-and-secrets.md` |
| Q-002 | Location/access for Jacob's cTrader **cBot** code (for sizing-engine review, Round J)? | 2026-08-17 | Round J sizing decision | OPEN | Jacob to provide repo/path |
| Q-003 | Headless automation of paid consumer ChatGPT/Claude UIs — permitted by current provider terms? | 2026-08-17 | Research Centre architecture (Round L) | **BLOCKED** pending provider-terms research + Jacob's legal/security review; do not assume permitted | Dated research brief per `.claude/rules/quantitative-evidence.md` |
| Q-004 | Lawful access boundary for user-supplied YouTube strategy videos (metadata, captions, transcripts, audio)? | 2026-08-17 | Round L video-analysis workflow | OPEN — compliant fallback available (user-supplied notes/transcripts) | Dated research brief; never evade platform controls |
| Q-005 | D-001 remainder: default drawdown numbers; does the 15% heat cap survive; fate of the 10k translation rule? | 2026-08-17 | Round E canonical accounting sign-off | OPEN | V1 audit evidence + Round E decision |
| Q-006 | Target jurisdictions / legal entity for Jacob's trading and (later) the content business? | 2026-08-17 | Charter finalisation; P3 compliance planning | OPEN | Round A continuation |
| Q-007 | Budget, delivery horizon, weekly availability, team capability, infrastructure constraints? | 2026-08-17 | Delivery roadmap realism (09-delivery) | OPEN | Round A continuation |
| Q-008 | Measurable business KPIs and explicit non-goals? | 2026-08-17 | PROJECT_CHARTER.md | OPEN | Round A continuation |
| Q-009 | Precise, measurable definition of backtest "accuracy" (backtest-vs-live degradation tolerance) Jacob will accept? | 2026-08-17 | BACKTEST_FIDELITY_SPEC.md acceptance thresholds | OPEN | Round A continuation → refined Round F |
| Q-010 | Has any historical data already been used for repeated selection in V1 (and is therefore ineligible as final holdout)? | 2026-08-17 | D-002; LEAKAGE_AND_HOLDOUT_POLICY.md | OPEN | V1 audit + Round B |
| Q-011 | Rules-file naming (D-014): keep both the six mandate topic files and the three numbered entry points, or consolidate? | 2026-08-18 | Nothing (non-blocking, layout only) | OPEN | Jacob's preference |
| Q-012 | Location and content of the migration-runbook "Prompt 6A" specification for the project-local AutoFX model-governance package (not present in this repository)? | 2026-08-18 | D-017 package creation/validation — which itself gates Round A resumption, the V1 forensic audit, subagent use, and acceptance of critical discovery artifacts | **RESOLVED 2026-08-18** — specification supplied verbatim by Jacob in-session; captured in MODEL_ROUTING_POLICY.md v0.2.0 and the package files; package created and validated against Claude Code 2.1.234 | Package and validation results `OWNER_APPROVED` by Jacob 2026-08-18; commit made manually by Jacob |
