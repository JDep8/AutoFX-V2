# GitHub Project Operating Model

- **Owner:** Jacob Depares
- **Status:** `OWNER_APPROVED` (model and authorisation per D-037,
  2026-08-18, evidence USER-STATED; this document records it)
- **Version:** 1.0.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** DECISION_LOG.md (D-025, D-026, D-033, D-037),
  GITHUB_PROJECT_REGISTER.md, TOOLING_REGISTER.md,
  `.claude/rules/documentation-and-traceability.md`
- **Approval evidence:** Owner instruction 2026-08-18 (roadmap setup
  authorisation)

## Authority model

1. **Repository documentation is the detailed source of truth.** The
   registers, specifications, and handoffs in this repository outrank
   every GitHub Project field, issue body, label, or comment. When they
   disagree, the repository wins and the drift is fixed on the board —
   never the other way around without an owner decision.
2. **The GitHub Project is the visual control plane** — a status surface
   ("AutoFX V2 — Project Roadmap", owner JDep8, kept **private**; the
   D-033 public ruling covers the repository only).
3. **Issue-backed cards are the integration surface.** Both Claude
   (terminal, `gh`) and ChatGPT (GitHub connector) read and maintain the
   repository issues; the Project draws from those issues.
4. **Conflicts are raised to Jacob and never silently resolved** (the
   standing conflict rule). Decisions are presented **one at a time in
   plain English** (D-025); **"Noted" does not mean "Approved."**

## Stage and approval meanings

- **Stage** (exactly one `stage:` label per tracked issue): Idea — Not
  Approved · Backlog · Ready · In Progress · Owner Decision · Blocked ·
  Review / Validation · Done · Deferred · Rejected / Superseded. Stages
  are descriptive workflow states (D-032); they never imply
  `IMPLEMENTED`/`TESTED`/`PAPER_VALIDATED`/`LIVE_VALIDATED`.
- **Approval**: IDEA_NOT_APPROVED · PROPOSED · OWNER_APPROVED ·
  EVIDENCE_REQUIRED · BLOCKED · DEFERRED · REJECTED · SUPERSEDED —
  mirroring the repository's lifecycle/evidence discipline. Only Jacob
  moves something to OWNER_APPROVED.
- **Creating a card never authorises the work.** Nothing moves to Ready
  or In Progress across an unpassed gate; implementation cards stay
  Backlog + gated until the Discovery Exit Review **and** the exact
  implementation-authorisation phrase.

## Idea intake

New ideas are captured immediately (so they are not lost) as `type:idea`
issues titled `IDEA — NOT APPROVED: …`, starting at Stage = Idea — Not
Approved and Approval = IDEA_NOT_APPROVED, using the idea template
(`.github/ISSUE_TEMPLATE/idea.md`). They remain outside approved scope
until Jacob reviews each as a separate plain-English decision. Rejected,
deferred, and superseded ideas stay visible for history (labels
`stage:rejected-superseded` / `stage:deferred`) — never deleted.

## Retention of blockers, deferrals, rejection, supersession

History is never erased. Blocked cards carry `stage:blocked` plus the
blocker in the body; deferred cards `stage:deferred` with the deferral
reason and owning round; rejected/superseded cards
`stage:rejected-superseded` with a pointer to their replacement —
mirroring Decision Log practice.

## How each Claude prompt updates the roadmap (D-037 standing rule)

Every future **substantive** AutoFX prompt finishes by:

1. updating canonical repository documentation;
2. updating affected GitHub issues;
3. updating issue `stage:` and `approval:` labels;
4. reconciling Project custom fields when `gh project` access is
   available;
5. adding the latest verified commit to affected cards;
6. recording blockers and owner decisions without assumptions;
7. preserving rejected, superseded, deferred, and not-approved items;
8. validating consistency between the repository and the Project;
9. committing and pushing permitted repository changes
   (`planning/discovery-handoff`; never `main`); and
10. reporting any drift or unsupported Project operation honestly.

Trivial conversation or side questions do not require a board update.

## How ChatGPT participates

ChatGPT, through its GitHub connection to the public repository, may
update **issue bodies, comments, labels, and open/closed state** using
the label families as its full state vocabulary. It cannot edit Project
custom fields; **Project custom-field reconciliation may still require
Claude/`gh`** — Claude reconciles fields to labels at the next
substantive prompt. ChatGPT edits are subject to the same rules: the
repository documents outrank the board, no approval is ever inferred,
and no gate is bypassed.

## Drift detection and reconciliation

At each substantive prompt (and at any explicit reconciliation request):
compare each tracked issue's `stage:`/`approval:` labels, body status
line, and latest-verified-commit against the registers and
GITHUB_PROJECT_REGISTER.md; fix the board to match the repository;
record material drift in SESSION_LOG.md; raise to Jacob (one at a time)
anything that looks like an unapproved state change rather than simple
staleness.

## Gates and prohibitions on the board

The no-build gate is quoted only by exact phrase and remains ACTIVE. No
board state authorises: Round B, either V1 audit, database access,
wireframes, implementation, infrastructure, trading, deployment, paid
GitHub features, GitHub Actions, workflows, loops, schedules, or
external broker activity. No card may imply a profitability promise or
live-readiness claim.

## Public-repository sensitivity rules (D-033)

Before every issue creation or update, and before every push: check that
no secrets, credentials, connection strings, private account data,
expected-return claims, or unpublished strategy details would become
public. If later-round content would expose dangerous security detail,
credentials, protected strategy IP, or legally sensitive material — stop
and raise one owner decision before committing it publicly.

## Returning the repository to private (procedure, D-033)

1. Jacob decides an authenticated external-review path exists and
   explicitly authorises the change (one-at-a-time decision).
2. Jacob (or Claude on his explicit instruction in that decision) flips
   visibility; Claude alone never changes visibility.
3. Verify via authenticated `gh` (metadata only); record in
   TOOLING_REGISTER, DECISION_LOG pointer note, and SESSION_LOG.
4. Re-check whether the private GitHub Project and any collaborator
   access still serve the review workflow; adjust only on owner
   instruction. Public history remains public — record that fact, never
   claim it was retracted.
