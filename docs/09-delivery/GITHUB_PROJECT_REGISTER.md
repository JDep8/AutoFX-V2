# GitHub Project Register

- **Owner:** Jacob Depares
- **Status:** Living register (roadmap surface inventory; D-037)
- **Version:** 1.0.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** GITHUB_PROJECT_OPERATING_MODEL.md, DECISION_LOG.md
  (D-033, D-036, D-037), TOOLING_REGISTER.md
- **Approval evidence:** D-037 owner authorisation 2026-08-18

## GitHub Project

| Field | Value |
|---|---|
| Title | AutoFX V2 — Project Roadmap |
| Number | 1 |
| ID | `PVT_kwHOBEQovs4Bgrk6` |
| URL | https://github.com/users/JDep8/projects/1 |
| Visibility | **PRIVATE** — VERIFIED at creation and after population (`public: false`), 2026-08-18. Jacob completed the `project`-scope device flow the same day |
| Linked repository | JDep8/AutoFX-V2 (linked) |
| Description / README | Set per D-037 (repo docs = source of truth; one-at-a-time decisions; "noted" ≠ "approved"; IDEA — NOT APPROVED intake; cards ≠ authorisation; no-build gate active; reconciliation duty) |
| Items | 52/52 issues added 2026-08-18; Stage, Approval, Priority, Round / Phase, Evidence set on every item mirroring the table below (Evidence: Owner Approved for #1/#3, Proposed for #19, Not Started elsewhere; Round / Phase = Implementation for #22–#51, Operations for #19/#52) |
| Fields | All 11 created 2026-08-18 exactly as specified below (5 single-select + 6 text) |
| Paid features / Actions / automation | None; prohibited |

### Fields (created 2026-08-18)

Single-select **Stage** (Idea — Not Approved · Backlog · Ready · In
Progress · Owner Decision · Blocked · Review / Validation · Done ·
Deferred · Rejected / Superseded); single-select **Approval**
(IDEA_NOT_APPROVED · PROPOSED · OWNER_APPROVED · EVIDENCE_REQUIRED ·
BLOCKED · DEFERRED · REJECTED · SUPERSEDED); single-select **Priority**
(Governance · P1 · P2 · P3); single-select **Round / Phase** (Phase 0 ·
Phase 1 / V1 Audit · Rounds A–O · Discovery Exit Review · Implementation ·
Operations); single-select **Evidence** (Not Started · Evidence Pending ·
Proposed · Verified · Owner Approved · Validated); text fields
**Workstream · Gate · Requirement IDs · Dependencies · Latest Verified
Commit · Target Range**. Issues #1–#52 added as items with select fields
set to mirror the labels below; **Latest Verified Commit** is maintained
by the D-037 reconciliation rule. No dates, thresholds, or costs are
invented to fill fields; Workstream/Gate/Dependencies/Requirement-IDs
text fields stay empty where the issue body already carries the detail.

### Views (manual UI steps — `gh` 2.96.0 cannot create Project views)

In the Project UI: **New view** → choose Board or Table → then per view:
1. **Executive Overview** — Board, group by `Stage`, filter `label:type:milestone`.
2. **Discovery A–O** — Table, filter `Round / Phase` is any Round A…O, sort by Round.
3. **P1 Platform** — Board, filter `Priority = P1`, group by `Stage`.
4. **P2 Research Centre** — Table, filter `Priority = P2`.
5. **P3 Content and Brand** — Table, filter `Priority = P3`.
6. **Decisions Required** — Table, filter `Stage = Owner Decision`.
7. **Blockers** — Table, filter `Stage = Blocked`.
8. **Ideas — Not Approved** — Table, filter `Stage = Idea — Not Approved`.
9. **Roadmap / Timeline** — Roadmap layout, date field = none until real
   dates exist (Target Range stays text; no dates are invented).
10. **Completed and Superseded History** — Table, filter `Stage = Done`
    OR `Stage = Rejected / Superseded` OR `Stage = Deferred`.

## Issue-backed cards (created 2026-08-18; latest verified commit at creation: `e98c852`)

Stage/Approval are carried as labels (exactly one `stage:` label each).
Round/Phase and key requirement IDs are recorded in each body.

| # | Card | Stage | Approval | Round/Phase | Key IDs |
|---|------|-------|----------|-------------|---------|
| [1](https://github.com/JDep8/AutoFX-V2/issues/1) | Phase 0 — Discovery repository scaffold | Done | OWNER_APPROVED | Phase 0 | D-011…D-017 |
| [2](https://github.com/JDep8/AutoFX-V2/issues/2) | Phase 1 — Read-only V1 forensic assessment | Owner Decision | PROPOSED | Phase 1 / V1 Audit | Q-010, D-022, D-023 |
| [3](https://github.com/JDep8/AutoFX-V2/issues/3) | Round A — Vision, users, boundaries, success | Done | OWNER_APPROVED | Round A | D-001…D-036 |
| [4](https://github.com/JDep8/AutoFX-V2/issues/4) | Round B — V1 outcomes and migration stance | Backlog | PROPOSED | Round B | D-002, D-003, Q-010 |
| [5](https://github.com/JDep8/AutoFX-V2/issues/5) | Round C — Markets, instruments, sessions | Backlog | PROPOSED | Round C | D-007, D-009 |
| [6](https://github.com/JDep8/AutoFX-V2/issues/6) | Round D — Data acquisition and quality | Backlog | PROPOSED | Round D | DATA-001…009 |
| [7](https://github.com/JDep8/AutoFX-V2/issues/7) | Round E — Accounting, drawdown, risk | Backlog | PROPOSED | Round E | D-001, Q-005, RISK-* |
| [8](https://github.com/JDep8/AutoFX-V2/issues/8) | Round F — Backtest truth and simulation fidelity | Backlog | PROPOSED | Round F | D-021, D-034, VAL-* |
| [9](https://github.com/JDep8/AutoFX-V2/issues/9) | Round G — Strategy, ML, experiment governance | Backlog | PROPOSED | Round G | D-003, D-030, QUANT-* |
| [10](https://github.com/JDep8/AutoFX-V2/issues/10) | Round H — Holdout, crises, acceptance gates | Backlog | PROPOSED | Round H | D-002, D-004, D-030 |
| [11](https://github.com/JDep8/AutoFX-V2/issues/11) | Round I — Book generation and approval | Backlog | PROPOSED | Round I | D-005, FR-* |
| [12](https://github.com/JDep8/AutoFX-V2/issues/12) | Round J — cTrader, execution, certification | Backlog | PROPOSED | Round J | D-006, D-034, EXEC-* |
| [13](https://github.com/JDep8/AutoFX-V2/issues/13) | Round K — Monitoring, reconciliation, ledger | Backlog | PROPOSED | Round K | FR-004, EXEC-005 |
| [14](https://github.com/JDep8/AutoFX-V2/issues/14) | Round L — Deep Research Centre | Backlog | PROPOSED | Round L | Q-003, Q-004, RES-* |
| [15](https://github.com/JDep8/AutoFX-V2/issues/15) | Round M — Content, characters, business plan | Backlog | PROPOSED | Round M | D-018, CONTENT-* |
| [16](https://github.com/JDep8/AutoFX-V2/issues/16) | Round N — Architecture, security, operations | Backlog | PROPOSED | Round N | D-029, SEC-*, OPS-* |
| [17](https://github.com/JDep8/AutoFX-V2/issues/17) | Round O — UX, wireframes, readiness | Backlog | PROPOSED | Round O | UX-001…003 |
| [18](https://github.com/JDep8/AutoFX-V2/issues/18) | Discovery Exit Review | Backlog | PROPOSED | Discovery Exit Review | 20-item checklist |
| [19](https://github.com/JDep8/AutoFX-V2/issues/19) | Command-runbook v0.2.0 review | Owner Decision | PROPOSED | Operations | D-035, D-025 |
| [20](https://github.com/JDep8/AutoFX-V2/issues/20) | Provision autofx_v1_readonly | Owner Decision | PROPOSED | Phase 1 / V1 Audit | D-022, SEC-002 |
| [21](https://github.com/JDep8/AutoFX-V2/issues/21) | Authorisation: repo-side V1 audit | Owner Decision | PROPOSED | Phase 1 / V1 Audit | D-023, Q-010 |
| [22](https://github.com/JDep8/AutoFX-V2/issues/22)–[39](https://github.com/JDep8/AutoFX-V2/issues/39) | P1 implementation workstreams (18 planning cards: foundation, data platform, quality/lineage, backtest engine, Mode A replay, Mode B shadow, Mode C certification, research/ML, book generation, accounting/risk, approved-books, cTrader routing, monitoring, ledger, paper validation, live gates, UI, security/ops) | Backlog | PROPOSED | Implementation | per body (EXEC/DATA/VAL/RISK/FR/SEC/OPS/KPI) |
| [40](https://github.com/JDep8/AutoFX-V2/issues/40)–[44](https://github.com/JDep8/AutoFX-V2/issues/44) | P2 workstreams (5 cards) | Deferred | PROPOSED | Round L / Implementation (deferred) | RES-*, Q-003/004 |
| [45](https://github.com/JDep8/AutoFX-V2/issues/45)–[51](https://github.com/JDep8/AutoFX-V2/issues/51) | P3 workstreams (7 cards incl. the mandatory legal gate) | Deferred | PROPOSED | Round M / Implementation (deferred) | CONTENT-*, D-018 |
| [52](https://github.com/JDep8/AutoFX-V2/issues/52) | Ideas Inbox — IDEA / NOT APPROVED | Idea — Not Approved | IDEA_NOT_APPROVED | Operations | D-025, D-037 |

Counts: 52 cards — Stage: Done 2 · Owner Decision 4 · Backlog 33 ·
Deferred 12 · Idea — Not Approved 1. Approval: OWNER_APPROVED 2 ·
PROPOSED 49 · IDEA_NOT_APPROVED 1. No card is Ready or In Progress; every
implementation card is Backlog/Deferred and gated.

## Reconciliation rule

At every substantive prompt (D-037 standing rule): reconcile this
register + issue labels/bodies against the repository registers; update
"latest verified commit" on touched cards; record drift in
SESSION_LOG.md. Idea template: `.github/ISSUE_TEMPLATE/idea.md`.
