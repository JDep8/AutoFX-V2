# User Roles and Journeys

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — journeys defined in Round O)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** DECISION_LOG.md (D-008), 02-product-and-ux/*
- **Approval evidence:** D-008 (sole user) OWNER_APPROVED 2026-08-17

## Users

Per D-008, Jacob is the sole human user. Even so, V2 distinguishes *roles* he
occupies at different times — because permissions, safety interlocks, and
audit differ per role:

| Role | What it may do | What it may never do |
|------|----------------|----------------------|
| Owner/approver | Approve decisions, books, live activation; own kill switches | Bypass gates it defined |
| Researcher | Run experiments, propose strategies/books | Touch the locked holdout; modify live config |
| Operator | Monitor live/paper trading, trigger controlled exits and kill switches, run incident response | Approve books; change risk definitions |
| Auditor (retrospective) | Read everything; reproduce any result | Modify anything |

Automated agents (research, monitoring) act under the most restrictive role
that suffices and never hold approval authority.

## Journeys (inventory — detailed in Round O / PAGE_AND_WORKFLOW_SPEC.md)

1. Ingest and verify data → data health review
2. Research a strategy → experiment registration → Gate 2/3
3. Generate a book (multi-day job) → candidate review → Gate 4
4. Approve a book (evidence pack) → Approved Books, disabled → Gate 5
5. Paper/shadow validation → Gate 6
6. Live activation on selected accounts → Gate 7
7. Monitor open trades → controlled exit / incident / kill switch
8. Post-trade review → trade ledger evidence → research feedback (Gate 8)
9. (P2) Research intake → review → knowledge catalogue
10. (P3) Approved research → content production → compliance → publish

## Open questions

Notification channels, mobile use, accessibility → Round O (see
QUESTION_REGISTER as new items are raised).
