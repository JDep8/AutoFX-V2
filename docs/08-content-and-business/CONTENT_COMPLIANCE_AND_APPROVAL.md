# Content Compliance and Approval

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-008, D-010), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (CONTENT-001, CONTENT-003, BUS-004), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-006), [CONTENT_STUDIO_PRODUCT_SPEC.md](CONTENT_STUDIO_PRODUCT_SPEC.md), [AI_CHARACTER_AND_BRAND_SPEC.md](AI_CHARACTER_AND_BRAND_SPEC.md)
- **Approval evidence:** None yet

## Purpose

This document will define the compliance controls and the human approval gate
that every piece of content must pass before publication. It covers financial-
promotion rules, performance and backtest claims, rights and licensing, and
synthetic-media disclosure. The jurisdiction-specific legal content is blocked
on Q-006 and cannot be filled in until the target countries are decided and a
legal review is obtained; nothing publishes before this document is
owner-approved (CONTENT-003).

## Scope and decisions this document will own

- The compliance checklist applied at the compliance-review stage of the
  content workflow, and the pass/fail rules.
- Performance-claim and backtest-disclosure policy for all channels.
- Rights, licensing, and consent requirements for all media inputs.
- The human approval gate: who approves, what evidence is recorded, and the
  rule that nothing ever auto-publishes (CONTENT-001).
- Out of scope: workflow stage sequencing
  ([CONTENT_STUDIO_PRODUCT_SPEC.md](CONTENT_STUDIO_PRODUCT_SPEC.md)) and
  account/permission mechanics
  ([CHANNEL_PUBLISHING_PLAN.md](CHANNEL_PUBLISHING_PLAN.md)).

## Structure skeleton

### 1. Financial-promotion controls

Whether and where content constitutes a financial promotion, and the resulting
obligations per jurisdiction. Entirely dependent on the jurisdiction-specific
legal review — **blocked on Q-006**; target countries are a Round M input.

### 2. Performance-claim controls

Rules for any statement about trading results: sourcing from the claim
register, mandatory uncertainty framing, and the standing rule that
profitability is never guaranteed (BUS-004). Claim taxonomy defined with
CONTENT_STUDIO_PRODUCT_SPEC.md in Round M; legal wording → Q-006.

### 3. Risk disclosures

Required risk-warning content, prominence, and per-channel placement.
Jurisdiction-specific wording blocked on Q-006; placement mechanics in Round M.

### 4. Backtest disclosures

How backtested or simulated results are labelled, the required caveats, and
the prohibition on presenting backtests as live results (consistent with the
status vocabulary: a backtest is never described as live-validated).
Disclosure text finalised in Round M / Q-006.

### 5. Affiliate and sponsorship disclosure

Disclosure rules for any affiliate links, sponsorships, or paid promotions,
per platform policy and applicable advertising law. Whether affiliation is
part of the model at all is a BUSINESS_PLAN.md Round M question.

### 6. Copyright, licences, and platform rules

Licensing requirements for music, stock media, fonts, and third-party footage;
per-platform content-policy summaries with retrieval dates. Evidence gathered
in Round M research; no licence status may be assumed without a dated record.

### 7. Voice, likeness, and impersonation

Consent requirements for any real voice or likeness; controls preventing the
AI character from impersonating real people (CONTENT-003; character rules in
AI_CHARACTER_AND_BRAND_SPEC.md). Legal confirmation → Q-006.

### 8. Synthetic-media disclosure and provenance

AI-generation disclosure per channel, plus provenance recording for every
published asset: source research, claim IDs, character version, provider,
approval evidence. Mechanism designed in Round M.

### 9. Recordkeeping

What is retained for every published item (approval record, final asset,
disclosures shown, claim register extract) and for how long. Retention rules
depend on the jurisdiction review (Q-006).

### 10. Human approval gate

The mandatory pre-publish approval: approver, checklist confirmation, recorded
evidence, and rejection/rework loop. The rule itself is fixed (CONTENT-001:
human approval before publish, always); its artefact format is defined in
Round M.

### 11. Jurisdiction matrix

Per-country legal findings and the resulting obligations. Empty until target
countries are chosen (Round M) and the legal review completes — **blocked on
Q-006**.

## Known inputs

- Human approval before publish is mandatory; nothing auto-publishes
  (CONTENT-001).
- Financial-promotion and performance-claim controls, risk/backtest
  disclosures, synthetic-media disclosure, provenance, recordkeeping, and
  jurisdiction-specific legal review are required before first publish
  (CONTENT-003, priority M).
- The compliance checklist must be owner-approved per jurisdiction before the
  first publish (CONTENT-003 acceptance criterion).
- Profitability is never guaranteed; uncertainty is always reported (BUS-004).
- The content business is assessed separately for its own compliance needs
  (D-008); Priority 3 is planning-only until P1 is live-validated (D-010).

## Open questions

- Target jurisdictions and the legal review of each — **Q-006** (blocking),
  countries chosen in Round M.
- Whether any content constitutes a regulated financial promotion in each
  target jurisdiction — Q-006.
- Approved wording for risk and backtest disclosures — Round M / Q-006.
- Whether affiliate/sponsorship revenue is in the model (drives section 5) —
  Round M (BUSINESS_PLAN.md).
- Platform-policy evidence per channel, with retrieval dates — Round M
  research.
- Retention periods for compliance records — Q-006.
