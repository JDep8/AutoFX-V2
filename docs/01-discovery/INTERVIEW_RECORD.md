# Interview Record

- **Owner:** Jacob Depares
- **Status:** Living register — Round A in progress
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** DISCOVERY_STATUS.md, DECISION_LOG.md
- **Approval evidence:** Answers below are Jacob's explicit selections/text

## Round A — Vision, users, business boundaries, and success

### Batch 1 — 2026-08-17 (asked during plan review; 6 questions)

**Q1. Who is AutoFX V2 for — business model?**
Options offered: Jacob-only personal (recommended) / personal now, customer-ready later / customer-facing from start / internal team.
**Answer:** "Jacob-only, personal trading" → D-008 `OWNER_APPROVED`.

**Q2. Asset classes for first release?**
Options offered: FX only (recommended) / FX + crypto day one / FX + other CFDs.
**Answer (free text, verbatim):** "Forex, Indices, Metals CFD, Crypto CFD, Agriculture, Equities CFD, Cash CFD, Commodities."

**Q2b (clarification). Full target universe with phased rollout, or all eight end-to-end at first release?**
Options offered: target universe, phased FX-first (recommended) / all eight at first release / decide per class in Round C/D with cost evidence.
**Answer:** "Target universe; phased rollout, FX first" → D-009 `OWNER_APPROVED`.

**Q3. Drawdown-model conflict (D-001)?**
First response: "Can you explain please" → plain-language explanation provided
(realised vs mark-to-market drawdown; peak-relative measurement; V1's linked
25% cap / 15% heat / 10k translation package; V2 brief's configurable cap +
$100k/1% standard; why the definition drives approvals, kill switches, sizing).
**Answer after explanation:** "Configurable cap, keep V1's measurement
discipline" → D-001 direction `OWNER_APPROVED`; numbers → Round E (Q-005).

**Q4. Priority 1 MVP boundary?**
Options offered: P1 full, P2/P3 planning-only (recommended) / P1 staged demo-first / P1 + minimal Research Centre.
**Answer:** "Yes — P1 full, P2/P3 planning-only" → D-010 `OWNER_APPROVED`.

### Batch 2 — pending (≤8 questions per batch)

Remaining Round A topics: jurisdictions/legal entity (Q-006); budget, horizon,
availability, team, infrastructure (Q-007); measurable KPIs and non-goals
(Q-008); measurable meaning of backtest "accuracy" (Q-009); PostgreSQL
read-only access path (Q-001); cBot location (Q-002).

Round A domain summary status: `PROPOSED` — becomes `OWNER_APPROVED` only when
Jacob approves the completed Round A summary.
