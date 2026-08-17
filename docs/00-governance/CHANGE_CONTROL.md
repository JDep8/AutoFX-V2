# Change Control

- **Owner:** Jacob Depares
- **Status:** `PROPOSED`
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** DECISION_LOG.md, DOCUMENT_INDEX.md
- **Approval evidence:** None yet

## Rules

1. Repository documents are the source of truth; changes happen by editing
   documents, never by chat-only agreement.
2. Any change to an `OWNER_APPROVED` item requires a new Decision Log entry;
   the old item is marked `SUPERSEDED` with a pointer — history is never
   erased.
3. Changes affecting leakage, holdout integrity, risk, drawdown, sizing, live
   safety, or legal/compliance exposure require Jacob's explicit approval
   before the document status changes.
4. Every material change updates: the owning document's header (version, last
   reviewed), the Decision Log (if a decision), the Requirements Catalogue and
   Traceability Matrix (if requirements move), and `DOCUMENT_INDEX.md` (if
   files are added/renamed).
5. Version numbers: MAJOR.MINOR.PATCH per document — MAJOR on owner-approved
   scope change, MINOR on content addition, PATCH on corrections.
6. Documentation-only commits during discovery; commit messages reference the
   decision/question IDs they touch. Never push without Jacob's explicit
   instruction.
