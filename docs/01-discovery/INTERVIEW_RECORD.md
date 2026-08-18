# Interview Record

- **Owner:** Jacob Depares
- **Status:** Living register — Round A in progress
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-18
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

### Batch 2 — asked 2026-08-17, answers pending (6 questions)

**Q5 (Q-006). Jurisdictions and legal entity.** Where is Jacob tax-resident
and trading from, under personal name or a company?
Options offered: (a) personal name — recommended, record current reality now;
(b) existing company; (c) defer entity questions until the content business.
Noted: does not block P1; hard-blocks Round M financial-promotion compliance.

**Q6 (Q-007). Budget, horizon, availability, team, infrastructure.**
Free-form: monthly budget range for data + infrastructure; target date for
first *paper* trading; hours/week available; other people involved; existing
servers (this Windows Server? the V1 VPS?). Calibrates roadmap estimate
ranges.

**Q7 (Q-008). Measurable KPIs and explicit non-goals.** Candidates to be
proposed for editing; two seed non-goals put forward for confirmation:
no high-frequency/latency-sensitive trading; no manual discretionary trades
routed through AutoFX (it executes approved books only).

**Q8 (Q-009). Measurable meaning of backtest "accuracy".**
Options offered: (a) tolerance bands — live/paper stays within an agreed band
of backtest expectations on return, drawdown, cost-per-trade; (b) distribution
tests — live outcomes statistically consistent with backtest distributions;
(c) both, bands as the headline gate — recommended. Numbers set in Round F;
only the *form* asked now.

**Q9 (Q-001). PostgreSQL read-only access path.**
Options offered: (a) Jacob creates a dedicated read-only role (e.g.
`autofx_readonly`) with connection details in a local file outside the repo,
never echoed or committed — recommended; (b) Jacob runs drafted queries and
pastes results; (c) skip the DB audit.

**Q10 (Q-002). cBot location.** Repo or machine path of Jacob's cTrader cBot,
for Round J's single-authoritative-sizing-engine decision.

**Answers:** none received as of 2026-08-18.

Round A domain summary status: `PROPOSED` — becomes `OWNER_APPROVED` only when
Jacob approves the completed Round A summary.
