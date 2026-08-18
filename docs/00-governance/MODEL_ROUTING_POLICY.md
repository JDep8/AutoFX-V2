# Model Routing Policy

- **Owner:** Jacob Depares
- **Status:** `OWNER_APPROVED` (D-012 policy stated by Jacob 2026-08-18; D-017 package specification supplied verbatim by Jacob 2026-08-18; evidence class USER-STATED)
- **Version:** 0.2.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** DECISION_LOG.md (D-012, D-017), TOOLING_REGISTER.md, .claude/rules/20-session-continuity.md
- **Approval evidence:** Owner handoff instruction 2026-08-18 (D-012); owner model-governance specification supplied in-session 2026-08-18 (D-017, resolving Q-012); **package and validation results `OWNER_APPROVED` by Jacob 2026-08-18** (terminal session; commit made manually by Jacob).

## Launch requirement (main terminal sessions)

Every main terminal session launches with:

```bash
claude --model best --effort ultracode
```

Before any critical work in the session:

- `/status` must resolve `best` to **Fable**;
- `/effort` must confirm **Ultracode**.

If either check fails, fix the session configuration before proceeding with
critical judgment or acceptance work.

**Verification record (2026-08-18, first terminal session — VERIFIED):**
`--effort ultracode` is supported on this machine's CLI. The session
resolved `best` to Fable 5 (`claude-fable-5`) and confirmed Ultracode
effort. Recovery item 1 (CURRENT_STATE.md) is closed; Jacob approved the
recovered state 2026-08-18. The per-session `/status` + `/effort` check
remains mandatory before critical work.

## Model-governance package (D-017, created 2026-08-18)

Project-local package implementing this policy — no third-party
model-routing plugin, no global settings changes, `CLAUDE_CODE_SUBAGENT_MODEL`
not set. All agents are read-only and in `plan` permission mode during
discovery.

| Artefact | Model | Effort | Permission mode | Tools |
|----------|-------|--------|-----------------|-------|
| `.claude/skills/autofx-model-governor/SKILL.md` | (governs routing; runs in main session) | — | — | — |
| `.claude/agents/autofx-fable-critical-governor.md` | fable | max | plan | Read, Glob, Grep |
| `.claude/agents/autofx-opus-reviewer.md` | opus | xhigh | plan | Read, Glob, Grep |
| `.claude/agents/autofx-sonnet-analyst.md` | sonnet | high | plan | Read, Glob, Grep |
| `.claude/agents/autofx-haiku-extractor.md` | haiku | (default) | plan | Read, Glob, Grep |

Agents remain read-only until the exact implementation-authorisation phrase
is provided for a named phase **and** a separately reviewed configuration
change updates their capabilities. Write, shell, network, MCP, database,
and cTrader tools are never enabled for these discovery agents.

## Routing policy

- The main discovery session runs on `best` with Ultracode.
- Before critical acceptance, `/status` must confirm `best` resolved to
  Fable and `/effort` must confirm Ultracode.
- **Fable is mandatory** for: architecture, data architecture,
  backtest-fidelity methodology, risk, drawdown, position sizing,
  portfolio/book acceptance, crisis validation, market-regime handling,
  execution/cTrader safety, live-enablement controls, unresolved evidence
  conflicts, and final phase acceptance.
- **Opus** may produce or review substantial but bounded specifications and
  implementation designs under accepted criteria.
- **Sonnet** may perform mechanical or deterministic work where
  specifications and acceptance tests are already approved.
- **Haiku** may only extract, locate, classify using explicit rules, or
  format information. Haiku must not infer profitability, approve
  strategies, interpret ambiguous evidence, or change requirements.
- Uncertainty, contradiction, novelty, financial impact, irreversible
  action, or missing evidence always escalates upward.
- A lower-model output may not close a critical acceptance criterion.
- Any lower-model contribution to a critical artifact requires independent
  Fable review before acceptance.
- Record the model, effort, task, reviewer, and acceptance outcome for
  critical artifacts (§ Critical routing and acceptance record).
- Model routing optimises mechanical labour, never the quality threshold.
- Never change models merely to evade a usage cap (master-prompt rule,
  retained).
- Acceptance decisions (any Gate, any `OWNER_APPROVED` transition) are
  prepared on Fable and made by Jacob.

## Quality rules

- No model may approve its own critical output without independent
  challenge.
- Verification requires evidence and measurable acceptance criteria, not
  confidence language.
- If Fable is unavailable, critical acceptance pauses and is recorded as
  `BLOCKED`.
- Never silently substitute another model for mandatory Fable acceptance.
- The no-build gate is preserved in every agent definition.
- Avoid unnecessary agent teams and parallelism.
- No dynamic workflow may bypass this routing policy.

## Critical routing and acceptance record

Append one row per critical artifact (skill § Procedure step 9).

| Date | Artifact / task | Model | Effort | Reviewer | Acceptance outcome |
|------|-----------------|-------|--------|----------|--------------------|
| 2026-08-18 | Round A batch 2 recording (D-018…D-024, Q-001/002/006–009), register updates, Round A summary preparation — governor dry-run classified CRITICAL (legal/compliance, fidelity methodology, DB security, `OWNER_APPROVED` transitions); no delegation (interview + owner-decision recording must run in the main session) | fable (main session, `claude-fable-5`) | ultracode | Main Fable session; independent consistency check delegated to autofx-sonnet-analyst (non-critical, deterministic criteria) | Records written; Round A summary `PROPOSED` — acceptance is Jacob's (pending) |

## Package validation record (2026-08-18, VERIFIED against Claude Code 2.1.234)

Validated by read-only string inspection of the installed CLI binary
(`claude --version` → 2.1.234; `C:\Users\Administrator\.local\bin\claude.exe`):

- Agent frontmatter `model` accepts `["sonnet","opus","haiku","fable"]` —
  `fable` valid.
- Agent/skill frontmatter `effort` accepts
  `["low","medium","high","xhigh","max"]` or an integer — `max`, `xhigh`,
  `high` valid.
- Agent frontmatter `permissionMode` accepts
  `["acceptEdits","auto","bypassPermissions","default","dontAsk","plan"]` —
  `plan` valid.
- `tools` accepts a comma-separated list — `Read, Glob, Grep` valid.
- Skill frontmatter known keys include `name` and `description` (the only
  keys the skill uses).
- No unsupported field is used; nothing was approximated or substituted.
- Nuance recorded for completeness: the *session-level* persisted effort
  setting tops out at `xhigh` (Ultracode = `xhigh` effort plus standing
  dynamic-workflow orchestration); *agent-level* `effort: max` is valid
  agent-scope configuration.
