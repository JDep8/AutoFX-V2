# Model Routing Policy

- **Owner:** Jacob Depares
- **Status:** `OWNER_APPROVED` (policy stated by Jacob 2026-08-18; evidence class USER-STATED)
- **Version:** 0.1.1
- **Last reviewed:** 2026-08-18
- **Dependencies:** DECISION_LOG.md (D-012), .claude/rules/20-session-continuity.md
- **Approval evidence:** Owner handoff instruction, 2026-08-18

## Launch requirement (main terminal sessions)

Every main terminal session launches with:

```bash
claude --model best --effort ultracode
```

Before any critical work in the session:

- `/status` must resolve `best` to **Fable**;
- `/effort` must confirm **Ultracode**.

If either check fails, fix the session configuration before proceeding with
critical judgment or acceptance work.

**Verification record (2026-08-18, first terminal session — VERIFIED):**
`--effort ultracode` is supported on this machine's CLI. The session
resolved `best` to Fable 5 (`claude-fable-5`) and confirmed Ultracode
effort. Recovery item 1 (CURRENT_STATE.md) is closed; Jacob approved the
recovered state 2026-08-18. The per-session `/status` + `/effort` check
remains mandatory before critical work.

## Routing table

| Model | Use for |
|-------|---------|
| **Fable** | Critical judgment and acceptance: cross-domain architecture, risk/drawdown definitions, leakage/holdout rulings, gate decisions, adversarial reviews, anything safety- or evidence-critical |
| **Opus** | Substantial bounded reasoning: deep single-domain analysis, structured research synthesis within an approved frame |
| **Sonnet** | Deterministic work from approved specifications: mechanical drafting, formatting to a fixed template, applying an already-approved rule |
| **Haiku** | Extraction, search, and formatting only |

## Escalation rules

- Uncertainty always escalates **upward** — a smaller model never resolves an
  ambiguity; it hands it up.
- Never change models merely to evade a subscription-wide usage cap
  (master-prompt rule, retained).
- Acceptance decisions (any Gate, any `OWNER_APPROVED` transition) are
  prepared on Fable and made by Jacob.
