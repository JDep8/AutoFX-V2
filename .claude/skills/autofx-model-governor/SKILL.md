---
name: autofx-model-governor
description: AutoFX model-routing governor (D-012/D-017). Load BEFORE delegating any AutoFX discovery task to a subagent and BEFORE any critical acceptance decision. Classifies the task as critical or non-critical, selects the lowest model permitted by MODEL_ROUTING_POLICY.md, shows the proposed route before a critical task executes, escalates on uncertainty or conflicting evidence, and requires Fable acceptance for critical output.
---

# AutoFX Model Governor

Authority: `docs/00-governance/MODEL_ROUTING_POLICY.md` (D-012, D-017). This
skill implements that policy. If this skill and the policy document ever
diverge, the policy document wins and the divergence is recorded as a
`CONFLICT` in the Decision Log or Question Register — never silently patched.

## Standing constraints (non-negotiable)

- **No-build gate.** Implementation is prohibited until Jacob explicitly
  writes `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>`.
  Nothing routed through this skill may implement application or
  infrastructure code, modify V1, write to PostgreSQL, connect to cTrader,
  or expose secrets.
- The four AutoFX discovery agents are **read-only** (`Read`, `Glob`,
  `Grep`; `permissionMode: plan`). Never grant write, shell, network, MCP,
  database, or cTrader tools to a discovery agent. Changing their
  capabilities requires the exact implementation-authorisation phrase for a
  named phase **and** a separately reviewed configuration change.
- No dynamic workflow may bypass this routing policy.
- Avoid unnecessary agent teams and parallelism.

## Procedure — before every delegation or critical acceptance

1. **Classify the task.** It is CRITICAL if it involves: architecture, data
   architecture, backtest-fidelity methodology, risk, drawdown, position
   sizing, portfolio/book acceptance, crisis validation, market-regime
   handling, execution/cTrader safety, live-enablement controls, unresolved
   evidence conflicts, final phase acceptance, any `OWNER_APPROVED`
   transition, or anything affecting leakage, holdout integrity, live
   safety, or legal/compliance exposure. Otherwise it is non-critical.
2. **Decide whether to delegate at all.** Prefer no delegation when the
   main session can do the work directly at equal quality; say so
   explicitly when that is the better route.
3. **Select the lowest model permitted by policy — not merely the
   cheapest:**
   - `autofx-haiku-extractor` (haiku): filename discovery, literal
     extraction, classification using explicit rules, formatting,
     non-interpretive summarisation — nothing else.
   - `autofx-sonnet-analyst` (sonnet, high): deterministic analysis against
     already-approved criteria, documentation consistency, structured
     comparisons.
   - `autofx-opus-reviewer` (opus, xhigh): substantial bounded reasoning,
     specification review, traceability review, independent challenge.
   - `autofx-fable-critical-governor` (fable, max): MANDATORY for every
     item in the critical list above.
4. **Show the proposed route before executing a critical task:** task,
   classification, selected agent/model/effort, and why that model is
   sufficient.
5. **Explain sufficiency** for every delegation, critical or not.
6. **Escalate upward** whenever uncertainty, contradiction, novelty,
   financial impact, irreversible action, or missing evidence appears.
   A smaller model never resolves an ambiguity; it hands it up. Never
   change models to evade a usage cap.
7. **Acceptance discipline:**
   - A lower-model output may never close a critical acceptance criterion.
   - Any lower-model contribution to a critical artifact requires
     independent Fable review (`autofx-fable-critical-governor`, or the
     main Fable session) before acceptance.
   - No model may approve its own critical output without independent
     challenge.
   - Verification requires evidence and measurable acceptance criteria,
     never confidence language.
   - Acceptance decisions (any Gate, any `OWNER_APPROVED` transition) are
     prepared on Fable and made by Jacob.
8. **If Fable is unavailable:** pause critical acceptance, record the item
   as `BLOCKED` in the appropriate register and in CURRENT_STATE.md, and
   stop. Never silently substitute another model for mandatory Fable
   acceptance.
9. **Record the evidence.** For every critical artifact, append the model,
   effort, task, reviewer, and acceptance outcome to
   `docs/00-governance/MODEL_ROUTING_POLICY.md` § Critical routing and
   acceptance record.

Model routing optimises mechanical labour, never the quality threshold.
