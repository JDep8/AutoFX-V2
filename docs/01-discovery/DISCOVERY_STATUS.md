# Discovery Status

- **Owner:** Jacob Depares
- **Status:** Living register
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** INTERVIEW_RECORD.md, DECISION_LOG.md
- **Approval evidence:** n/a (register)

## Phase status

| Phase | Status | Notes |
|-------|--------|-------|
| Phase 0 — Discovery repository scaffold | COMPLETE 2026-08-17 | 78 planning files created; completeness-verified (53 domain skeletons checked: 0 missing, 0 header violations, 0 overclaims) |
| Phase 1 — Read-only V1 forensic assessment | NOT STARTED | Repo access verified (gh, read-only); DB access blocked on Q-001 |
| Interview rounds A–O | Round A in progress | See below |
| Discovery Exit Review | NOT STARTED | Requires all rounds complete |
| Implementation | **GATED** | Requires `AUTHORISE AUTOFX V2 IMPLEMENTATION — PHASE <number/name>` |

## Interview rounds

| Round | Theme | Status |
|-------|-------|--------|
| A | Vision, users, business boundaries, success | IN PROGRESS — 4 decisions captured (D-001 direction, D-008, D-009, D-010); batch 2 pending (Q-001/002/006/007/008/009) |
| B | V1 outcomes and migration stance | NOT STARTED (feeds from V1 audit) |
| C | Markets, instruments, sessions, operating scope | NOT STARTED |
| D | Data acquisition, rights, quality, operations | NOT STARTED |
| E | Canonical accounting, drawdown, risk | NOT STARTED (Q-005 queued) |
| F | Backtest truth model | NOT STARTED |
| G | Strategy discovery, ML, experiment governance | NOT STARTED |
| H | Holdout, crises, regimes, acceptance gates | NOT STARTED (D-002 queued) |
| I | Book generation and approval | NOT STARTED (D-005 queued) |
| J | Accounts, cTrader, execution, reconciliation | NOT STARTED (D-006, Q-002 queued) |
| K | Open-trade monitor and trade ledger | NOT STARTED |
| L | Deep Research Centre | NOT STARTED (Q-003, Q-004 queued) |
| M | Content Studio, AI characters, business plan | NOT STARTED |
| N | Architecture, security, operations, delivery | NOT STARTED |
| O | UX, information architecture, wireframe | NOT STARTED (wireframes need `AUTHORISE WIREFRAME ONLY`) |

## Verified facts (dated)

- 2026-08-17: `C:\AutoFXV2.0` was empty at engagement start; git initialised
  same day; documentation-only content.
- 2026-08-17: V1 repo `JDep8/AutoFX` is private, accessible read-only via
  authenticated `gh` CLI (account JDep8). Python, branch `main`, updated
  2026-07-30, 247 tree entries, extensive root-level review docs.
- 2026-08-17: V1 repo root contains `101005649.rdp` — recorded as a security
  flag for the V1 audit; contents never read.
- 2026-08-17: Unauthenticated access to the V1 repo returns 404 — all V1
  inspection must use `gh`.
