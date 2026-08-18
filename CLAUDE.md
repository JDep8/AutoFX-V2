# AutoFX V2.0 — Discovery & Planning Repository

This repository contains discovery, research, specification, and planning for
AutoFX V2. It contains **no application code, by design**. V1 failed by starting
implementation before the end-to-end product and evidence model were defined.
V2 does not repeat that sequence.

## Absolute no-build gate

Until Jacob Depares completes the Discovery Exit Review and explicitly writes:

`AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>`

do **not**:

- implement application or infrastructure code;
- create or alter production database objects or data;
- run database migrations or data backfills;
- place demo or live orders;
- connect an execution process to a live or demo account;
- deploy services, scheduled jobs, agents, websites, or publishing workflows;
- copy V1 code into V2;
- install dependencies merely to begin implementation;
- interpret approval of a document, wireframe, research task, or any prompt
  as approval to build.

Wireframes have a separate gate: `AUTHORISE WIREFRAME ONLY` permits a static or
mock-data prototype with no backend, database, broker, secrets, publishing
access, or live actions. See `.claude/rules/discovery-and-authorisation.md`.

## Source of truth and authority hierarchy

The repository documents are the source of truth. Conversational memory is not.
Never reconstruct project state from chat history when a register or handoff
file exists. Authority (highest wins): 1. Jacob's explicit written decisions
(Decision Log, gate phrases) · 2. this file + `.claude/rules/` · 3. governance
registers · 4. domain documents · 5. conversation content (no force until
captured into the documents above).

## Workspace, models, plugins (D-011/D-012/D-013, 2026-08-18)

- Terminal (CLI) is the primary workspace; Desktop for visual review and
  wireframes only.
- Main terminal sessions launch `claude --model best --effort ultracode`;
  verify `/status` → Fable and `/effort` → Ultracode before critical work.
  Routing: `docs/00-governance/MODEL_ROUTING_POLICY.md`.
- Plugin install gates: `docs/00-governance/TOOLING_REGISTER.md`.

## Quality gates

All promotion follows the acceptance-gate architecture (Gates 1–8: data →
experiment → strategy → book → approved-but-disabled → shadow/paper → live →
continue/reduce/pause/retire), mapped in
`docs/09-delivery/TEST_AND_EVIDENCE_STRATEGY.md`.

## Session start (every session)

1. Read `docs/00-governance/DOCUMENT_INDEX.md`.
2. Read `docs/handoffs/CURRENT_STATE.md`, `NEXT_ACTIONS.md`, `RESUME_PROMPT.md`.
3. Read only the domain documents required for the active task.
4. Inspect repository/branch/working-tree state.
5. Restate the active phase, last completed checkpoint, current objective,
   blockers, and no-build status before continuing.
6. Never repeat completed interview questions unless a recorded answer is
   contradictory or explicitly reopened by Jacob.

## Session end / before compaction or usage exhaustion

Update `docs/handoffs/` (`CURRENT_STATE.md`, `NEXT_ACTIONS.md`,
`RESUME_PROMPT.md`, append to `SESSION_LOG.md`) and every register affected by
the session's work. Work in small atomic units; update registers as decisions
occur, not at session end only. Detailed protocol:
`.claude/rules/documentation-and-traceability.md`.

## Status vocabulary (use only these labels for governed items)

`PROPOSED`, `OWNER_APPROVED`, `IMPLEMENTED`, `TESTED`, `PAPER_VALIDATED`,
`LIVE_VALIDATED`, `REJECTED`, `SUPERSEDED` — for governed items:
requirements, decisions, strategies, books, implementation components,
tests, validation evidence. Per D-032, descriptive progress states (e.g.
`Living register`, `In progress`, `Complete`, `Gated`, `Paused`) are
permitted for document headers, discovery rounds, registers, gates, and
operational workflow status, and must never imply `IMPLEMENTED`,
`TESTED`, `PAPER_VALIDATED`, or `LIVE_VALIDATED`.

- Never describe proposed or implemented work as tested.
- Never describe a backtest as live-validated.
- A decision is `OWNER_APPROVED` only when Jacob has explicitly approved it;
  a full interview-round summary is `OWNER_APPROVED` only after Jacob approves
  the completed domain summary.

## Traceability

Every material requirement has a unique ID with one of the prefixes
`BUS` `FR` `NFR` `DATA` `QUANT` `VAL` `RISK` `EXEC` `SEC` `OPS` `UX` `RES`
`CONTENT`, and traceability to design, tests, evidence, status, owner, and
decision. Registers live in `docs/00-governance/` and
`docs/01-discovery/REQUIREMENTS_CATALOGUE.md`.

## Security and data access

- Never expose or commit credentials, tokens, account identifiers, or private
  data. Never read secrets into output. Never copy `.env` or connection files.
- All V1 database access during discovery is read-only and deliberately
  bounded: schema/catalogue first, bounded queries, statement timeouts,
  sampling. Never write to or lock production data.
- Details: `.claude/rules/security-and-secrets.md`.

## Evidence honesty

- Profitability is never guaranteed. Report uncertainty, confidence intervals,
  and degradation tolerances.
- Safety-critical ambiguity **fails closed** and becomes a blocking entry in
  `docs/00-governance/QUESTION_REGISTER.md`.
- Details: `.claude/rules/quantitative-evidence.md`.

## Git

Documentation-only commits during discovery. Verify no secrets or unintended
files before every commit. **Never push without Jacob's explicit instruction.**

## Topic rules (read the one relevant to the active task)

Numbered entry points (start here):

- `.claude/rules/00-discovery-gate.md` — the gate + authority hierarchy
- `.claude/rules/10-evidence-and-traceability.md` — status + evidence labels
- `.claude/rules/20-session-continuity.md` — session/rollover/resume protocol

Detailed topic rules:

- `.claude/rules/discovery-and-authorisation.md`
- `.claude/rules/quantitative-evidence.md`
- `.claude/rules/data-integrity.md`
- `.claude/rules/execution-and-risk.md`
- `.claude/rules/security-and-secrets.md`
- `.claude/rules/documentation-and-traceability.md`
