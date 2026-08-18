# Tooling Register

- **Owner:** Jacob Depares
- **Status:** `OWNER_APPROVED` (policy stated by Jacob 2026-08-18; evidence class USER-STATED)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** DECISION_LOG.md (D-011, D-013), MODEL_ROUTING_POLICY.md
- **Approval evidence:** Owner handoff instruction, 2026-08-18

## Workspaces (D-011)

| Surface | Role |
|---------|------|
| Claude Code — terminal (CLI) | **Primary workspace** for all discovery and (later, if authorised) implementation work |
| Claude Desktop | Visual review and wireframes only |

## Plugin policy (D-013) — install state by gate

| Plugin(s) | Policy | Trigger / gate |
|-----------|--------|----------------|
| product-management | **Install now** | — |
| claude-md-management | **Install now** | — |
| session-report | **Install now** | — |
| data | Deferred | Only after the read-only database decision (Q-001) is resolved |
| design | Deferred | At the wireframe round (Round O, after `AUTHORISE WIREFRAME ONLY`) |
| engineering / security / LSP / review | Deferred | Only after `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>` |
| marketing | Deferred | Priority 3 (content business) work only |
| ECC | **Do not install now** | Revisit only on Jacob's explicit instruction |

Rules: no plugin may weaken the no-build gate; plugin installation is not
implementation authorisation; record any newly installed plugin here with
date and reason.

## Git conventions

- Local repository only; **never push** and never create a remote without
  Jacob's explicit instruction.
- Documentation-only commits during discovery; verify no secrets before every
  commit.
- Branch `planning/discovery-handoff` created 2026-08-18 for the terminal
  handoff; commits on it are left for Jacob's review per the handoff
  instruction (no automatic commit).

## Open items

- Q-011: rules-file naming overlap (three numbered entry points vs six
  mandate topic files) — Jacob to confirm keep-both or consolidation.
