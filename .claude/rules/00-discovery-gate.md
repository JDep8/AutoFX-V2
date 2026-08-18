# 00 — Discovery Gate (read first, every session)

This file is the authoritative entry point for the no-build gate. Detailed
interview and authorisation rules: [discovery-and-authorisation.md](discovery-and-authorisation.md).

## The gate (verbatim — do not paraphrase when enforcing)

Until Jacob Depares completes the Discovery Exit Review and explicitly writes:

`AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>`

do **not**: implement application or infrastructure code; create or alter
production database objects or data; run database migrations or data
backfills; place demo or live orders; connect an execution process to a live
or demo account; deploy services, scheduled jobs, agents, websites, or
publishing workflows; copy V1 code into V2; install dependencies merely to
begin implementation; or interpret approval of a document, wireframe,
research task, or any prompt as approval to build.

Wireframes have a separate gate: `AUTHORISE WIREFRAME ONLY` (static/mock-data
prototype only — no backend, database, broker, secrets, publishing access, or
live actions).

Additional standing prohibitions (owner handoff instruction, 2026-08-18): do
not modify V1; do not write to PostgreSQL; do not connect to or trade through
cTrader; never expose, print, store, or commit secrets.

## Authority hierarchy (highest wins)

1. Jacob's explicit written decisions (Decision Log entries and gate phrases).
2. Root `CLAUDE.md` and `.claude/rules/`.
3. Governance registers (`docs/00-governance/`).
4. Domain documents (`docs/01…09`).
5. Conversation content — has **no force** until captured into the documents
   above.

## Fail-closed rule

Safety-critical ambiguity fails closed and becomes a blocking entry in
[QUESTION_REGISTER.md](../../docs/00-governance/QUESTION_REGISTER.md).
