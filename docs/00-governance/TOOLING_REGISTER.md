# Tooling Register

- **Owner:** Jacob Depares
- **Status:** `OWNER_APPROVED` (policy stated by Jacob 2026-08-18; evidence class USER-STATED)
- **Version:** 0.4.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** DECISION_LOG.md (D-011, D-013, D-015, D-017, D-024), MODEL_ROUTING_POLICY.md
- **Approval evidence:** Owner handoff instruction, 2026-08-18

## Workspaces (D-011)

| Surface | Role |
|---------|------|
| Claude Code — terminal (CLI) | **Primary workspace** for all discovery and (later, if authorised) implementation work |
| Claude Desktop | Visual review and wireframes only |

## Plugin policy (D-013) — install state by gate

| Plugin(s) | Policy | Trigger / gate |
|-----------|--------|----------------|
| product-management | **INSTALLED 2026-08-18** (enabled in `.claude/settings.json`, commit `39e2730`, authorised by Jacob) | — |
| claude-md-management | **INSTALLED 2026-08-18** (enabled in `.claude/settings.json`, commit `39e2730`, authorised by Jacob) | — |
| session-report | **INSTALLED 2026-08-18** (enabled in `.claude/settings.json`, commit `39e2730`, authorised by Jacob) | — |
| data | Deferred | Only after the read-only database decision (Q-001) is resolved |
| design | Deferred | At the wireframe round (Round O, after `AUTHORISE WIREFRAME ONLY`) |
| engineering / security / LSP / review | Deferred | Only after `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>` |
| marketing | Deferred | Priority 3 (content business) work only |
| ECC | **Do not install now** | Revisit only on Jacob's explicit instruction |

Rules: no plugin may weaken the no-build gate; plugin installation is not
implementation authorisation; record any newly installed plugin here with
date and reason.

## Environment-visible external tooling (D-015, OWNER_APPROVED 2026-08-18)

Tooling configured at user or account scope (outside this repository) may be
visible in terminal sessions. Classification:
**ENVIRONMENT-VISIBLE / OUT-OF-SCOPE / NOT AUTHORISED FOR AUTOFX USE** —
never authenticate, invoke, remove, or modify it from AutoFX sessions.

| Tooling (observed 2026-08-18) | Scope | Ruling |
|-------------------------------|-------|--------|
| Figma plugin (skills + MCP tools) | User-level plugin configuration | Not authorised; Figma remains deferred until the approved wireframe phase (Round O) |
| claude.ai connectors: HubSpot, Lucid, Microsoft 365, Productive.io, Thomax Knowledge Platform | claude.ai account | Not authorised for AutoFX use |

Only project-scoped tools explicitly approved in this register are authorised
for AutoFX work.

## Model-governance package (D-017, created 2026-08-18)

Project-local Claude configuration implementing MODEL_ROUTING_POLICY.md —
created from Jacob's specification (supplied in-session 2026-08-18,
resolving Q-012); validated against Claude Code 2.1.234 (see
MODEL_ROUTING_POLICY.md § Package validation record); **package and
validation results `OWNER_APPROVED` by Jacob 2026-08-18** (commit made
manually by Jacob).

| File | Role |
|------|------|
| `.claude/skills/autofx-model-governor/SKILL.md` | Routing governor: classifies tasks, selects lowest permitted model, escalation + acceptance discipline |
| `.claude/agents/autofx-fable-critical-governor.md` | Fable · max · plan · Read/Glob/Grep — critical judgment and acceptance review |
| `.claude/agents/autofx-opus-reviewer.md` | Opus · xhigh · plan · Read/Glob/Grep — bounded reasoning, spec/traceability review, independent challenge |
| `.claude/agents/autofx-sonnet-analyst.md` | Sonnet · high · plan · Read/Glob/Grep — deterministic analysis against approved criteria |
| `.claude/agents/autofx-haiku-extractor.md` | Haiku · plan · Read/Glob/Grep — extraction/formatting only, never interpretation |

Constraints honoured at creation: no third-party model-routing plugin
installed; no global or user Claude settings altered;
`CLAUDE_CODE_SUBAGENT_MODEL` not set (verified unset at process, user, and
machine scope 2026-08-18); agents read-only in plan mode; no write, shell,
network, MCP, database, or cTrader tools. Capability changes require the
implementation-authorisation phrase for a named phase plus a separately
reviewed configuration change.

## Git conventions (updated 2026-08-18 per D-024)

- **Remote:** GitHub repository `JDep8/AutoFX-V2` —
  **https://github.com/JDep8/AutoFX-V2** — created 2026-08-18 as PRIVATE
  under Jacob's explicit written authorisation (D-024; verbatim in
  INTERVIEW_RECORD.md § Batch 2). VERIFIED at creation: private visibility;
  default branch `main`; branches `main` + `planning/discovery-handoff`
  pushed. **Visibility changed to PUBLIC by Jacob later the same day**
  (VERIFIED; see § Repository visibility, Q-014). Completely separate from
  `JDep8/AutoFX` (V1) — no V1 content is ever pushed here. Details:
  SESSION_LOG.md Session 5.
- **Standing operating model (D-024):** Claude may autonomously create
  commits and push validated work to explicitly approved branches, after
  running the relevant tests, documentation validation, and secret checks.
  Approved branch during discovery: `planning/discovery-handoff`. `main`
  receives work only with Jacob's explicit approval (prefer pull requests).
- **Prohibitions:** no force pushes; no history rewrite; no branch
  deletion; no direct merge into `main` without Jacob's explicit approval;
  pushing never implies deployment; no paid GitHub features without
  approval; no credentials in commands, output, logs, or documentation.
- Documentation-only commits during discovery; verify no secrets before
  every commit.
- **Permissions note (2026-08-18):** the committed `.claude/settings.json`
  allowlist remains read-only git/gh (V1-inspection scope) and predates
  D-024; commit/push/repository-creation operations under D-024 run under
  per-session approvals in the terminal harness. Extending the committed
  allowlist to match the D-024 operating model is a separately reviewable
  configuration change for Jacob — not made unilaterally.
- History: branch `planning/discovery-handoff` created 2026-08-18 for the
  terminal handoff (`fcde457`, `39e2730`, `d2f0d3a`, `00ad2cc` — all
  Jacob-reviewed/authorised). Local-only rule (superseded assumption A-006)
  applied until D-024. The D-024 branch procedure (fast-forward `master` to
  the validated planning state via `--ff-only`, rename to `main`, push, set
  default) was executed 2026-08-18 — VERIFIED; SESSION_LOG.md Session 5.

## Repository visibility (Q-014 RESOLVED 2026-08-18 → D-033)

- 2026-08-18 (creation): `JDep8/AutoFX-V2` created **PRIVATE** — VERIFIED at
  the time (`isPrivate: true`); that evidence was accurate when recorded.
- 2026-08-18 (later, same day): visibility VERIFIED as **PUBLIC**
  (`isPrivate: false`, authenticated `gh`, metadata-only check — the check
  verifies the state, not the actor). Attribution: **changed by Jacob**
  after Claude's creation report — USER-STATED (Jacob's closure-assurance
  instruction, 2026-08-18). Claude has not changed and will not change
  visibility (Q-014 is Jacob's decision). Recorded as a CONFLICT against
  D-024's PRIVATE requirement (pointer note in DECISION_LOG.md D-024).
- **Security and IP implications while public:** current content is
  documentation-only and secret-free (verified scans), but it already
  exposes business plans, budget ceilings, timelines, and personal context
  (owner name, Australian tax residency, weekly availability). As discovery
  progresses, strategy research (Rounds G–I), architecture and threat-model
  detail (Round N), execution safety design (Round J), and cost data would
  accumulate publicly — giving away trading IP, revealing security posture
  before implementation, and enabling scraping. Public git history is
  effectively irrevocable once cloned or indexed, even if the repo later
  returns to private. Until Q-014 is decided, sensitive-material placement
  is a standing consideration for every new document.
- **DECIDED 2026-08-18 (D-033, Q-014 RESOLVED):** temporarily public so
  ChatGPT can independently review committed outputs; returns to private
  once an authenticated review path exists **and Jacob explicitly
  authorises the change** (Claude never changes visibility);
  already-public history is irretrievably public; strict secret and
  sensitivity checks continue before every push; sensitive later-round
  content (security detail, credentials, strategy IP, legally sensitive
  material) triggers a stop-and-ask before any public commit. D-024's
  PRIVATE clause is superseded; all other D-024 controls stand.

## Claude Code command governance (research 2026-08-18)

- Catalogue, availability evidence, per-command AutoFX policies, session
  sequences, and the post-upgrade revalidation procedure live in
  [CLAUDE_CODE_COMMAND_RUNBOOK.md](CLAUDE_CODE_COMMAND_RUNBOOK.md).
- Researched against Claude Code **2.1.234** (VERIFIED 2026-08-18) on this
  Windows Server 2022 machine, using only official documentation
  (code.claude.com/docs: commands, sessions, scheduled-tasks) plus
  read-only local verification (binary token scan; session skill roster;
  in-session observations). No mutating command was exercised.
- **v0.1.0 catalogue REJECTED by Jacob 2026-08-18 (D-035)** for factual
  errors; corrected v0.2.0 (full 105-row official catalogue, two-axis
  evidence model, § 10 errata) remains **`PROPOSED`** and returns to Jacob
  for one-at-a-time approval (D-025). Standing regardless of approval
  state: no command bypasses the no-build gate, D-015 boundary, D-017
  routing, or D-024/D-033 git rules; mutating/installing/connecting/
  cloud/billing commands are never treated as routine.
- Revalidate the runbook after every Claude Code upgrade (runbook § 9).

## Open items

- Data plugin: its D-013 gate ("after the read-only database decision") is
  now satisfiable — Q-001 resolved via D-022 — but installation still
  requires Jacob's explicit instruction and a register entry here. Not
  installed.
- (Resolved 2026-08-18: Q-011 rules-file naming → D-031, keep both with
  the topic files authoritative; Q-014 visibility → D-033.)
