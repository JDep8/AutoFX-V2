# Discovery and Authorisation Rules

## Engagement type

This is a discovery, research, specification, and planning engagement.
Authorised outputs before implementation authorisation:

- creating and updating the planning/documentation scaffold in this repository;
- cited research;
- read-only inspection of V1 (repository and, once safely configured,
  its PostgreSQL database);
- diagrams, data dictionaries, interface contracts, pseudocode, test designs,
  and mock-data wireframes (wireframes only after `AUTHORISE WIREFRAME ONLY`);
- non-mutating repository inspection commands;
- proposed (never executed) implementation plans.

## The gate phrases

- Implementation: `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>`,
  written explicitly by Jacob after the Discovery Exit Review. Approval is
  per-phase; one phase's authorisation does not extend to the next.
- Wireframes: `AUTHORISE WIREFRAME ONLY` — static/mock-data prototype only; no
  backend, database, broker, secrets, publishing access, or live actions.

## Interview method

- Interview Jacob in thematic rounds (A–O, defined in
  `docs/01-discovery/DISCOVERY_STATUS.md`). Never dump the full questionnaire.
- Read existing answers and repository evidence first; never re-ask an
  answered question unless resolving a contradiction.
- Ask no more than eight tightly related questions per batch.
- For every material choice provide: the decision to make; two or three viable
  options; a recommendation with reasons; effect on fidelity, profitability,
  risk, cost, time, and future flexibility; and whether it blocks later work.
- If Jacob does not know, propose a provisional default labelled `PROPOSED`,
  never `OWNER_APPROVED`.
- After each answer batch, update requirements, questions, decisions,
  assumptions, glossary, and discovery-status documents, then return a compact
  round summary (decisions, changed requirements, assumptions awaiting
  approval, contradictions, risks/evidence required, next round).
- Plain language first; then record the exact technical definition.
- A domain summary becomes `OWNER_APPROVED` only when Jacob approves it.

## Decision authority

Present evidence and a recommendation, but require Jacob's explicit decision
whenever a choice affects leakage, holdout integrity, risk, drawdown, sizing,
live safety, or legal/compliance exposure. Never silently convert uncertainty
into an assumption — record it in the Assumption or Question register.

## If in the wrong place

If work is discovered to be happening in the V1 repository, a production
workspace, or any location of unclear ownership: stop and ask Jacob for the
correct V2 location.
