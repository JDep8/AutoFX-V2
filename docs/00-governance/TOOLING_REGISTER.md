# Tooling Register

- **Owner:** Jacob Depares
- **Status:** `OWNER_APPROVED` (policy stated by Jacob 2026-08-18; evidence class USER-STATED)
- **Version:** 0.1.1
- **Last reviewed:** 2026-08-18
- **Dependencies:** DECISION_LOG.md (D-011, D-013, D-015), MODEL_ROUTING_POLICY.md
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

## Git conventions

- Local repository only; **never push** and never create a remote without
  Jacob's explicit instruction.
- Documentation-only commits during discovery; verify no secrets before every
  commit.
- Branch `planning/discovery-handoff` created 2026-08-18 for the terminal
  handoff. Jacob reviewed and committed the handoff change set as `fcde457`
  and the plugin enablement as `39e2730` (authorship confirmed by Jacob in
  the terminal recovery session, 2026-08-18). Standing rule unchanged: no
  automatic commits — every commit is reviewed or explicitly authorised by
  Jacob.

## Open items

- Q-011: rules-file naming overlap (three numbered entry points vs six
  mandate topic files) — Jacob to confirm keep-both or consolidation.
