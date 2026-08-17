# Current State

- **Owner:** Jacob Depares
- **Status:** Living handoff (refreshed every checkpoint)
- **Last updated:** 2026-08-17, timezone UTC (server local: Windows Server 2022)

## Phase and authorisation

- Phase 0 (discovery repository scaffold) — IN PROGRESS.
- **No-build gate ACTIVE.** No implementation authorisation given. Wireframes
  also gated (`AUTHORISE WIREFRAME ONLY` not given).

## Last completed atomic task

Scaffold folders `00-governance`, `01-discovery`, `02-product-and-ux`,
`03-architecture`, `handoffs` (this file set), `wireframes/`, root `CLAUDE.md`,
`.claude/rules/` (6 files), `.gitignore` — all written 2026-08-17.

## Interruption record

A 9-agent drafting workflow for docs/02–09 was interrupted by the **weekly
usage limit** (interface showed: "resets 11pm (UTC)" — recorded, not guessed).
Agents for 02 and 03 completed their files before failing; agents for 04–09
and the completeness critic never ran. Jacob instructed continuation after the
limit event.

## Known partial / unsafe-to-assume state

- `docs/02-product-and-ux/*` (4 files) and `docs/03-architecture/*` (6 files,
  ADR_INDEX.md written inline afterwards) exist but have **not yet passed the
  completeness-critic verification** — treat as unverified skeletons.
- Folders `docs/04-data` … `docs/09-delivery` (44 files) NOT yet created.
- `docs/00-governance/DOCUMENT_INDEX.md` NOT yet written (waits for full tree).

## Decisions captured (all 2026-08-17, see DECISION_LOG.md / INTERVIEW_RECORD.md)

- D-001 direction `OWNER_APPROVED` (configurable cap; realised peak-relative
  canonical; MTM+heat separate; $100k/1% standard; numbers → Round E, Q-005)
- D-008 `OWNER_APPROVED` (Jacob-only personal trading)
- D-009 `OWNER_APPROVED` (8 CFD classes, phased FX-first, Gate 1 per class)
- D-010 `OWNER_APPROVED` (P1 full = MVP; P2/P3 planning-only)
- D-002…D-007 seeded OPEN in DECISION_LOG.md

## Verified facts and evidence

See `docs/01-discovery/DISCOVERY_STATUS.md` § Verified facts (V2 dir was
empty; V1 repo private but gh-accessible, 247 entries; `.rdp` security flag;
DB access + cBot location open as Q-001/Q-002).

## Repository state

- Branch `main` (fresh init), no remote. Working tree: all files above,
  uncommitted at time of writing (checkpoint commit is the next action).
- Checks run: file-tree listing vs mandated structure (04–09 missing, known);
  no other verification yet.

## Contradictions / blockers

- None new. Open blockers are Q-001 (DB credentials) and Q-002 (cBot
  location) — they block V1 audit depth and Round J respectively, not the
  scaffold.
