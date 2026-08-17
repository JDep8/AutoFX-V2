# Content Studio Product Specification

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-008, D-010), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (CONTENT-001, CONTENT-003), [AI_CHARACTER_AND_BRAND_SPEC.md](AI_CHARACTER_AND_BRAND_SPEC.md), [CONTENT_COMPLIANCE_AND_APPROVAL.md](CONTENT_COMPLIANCE_AND_APPROVAL.md), [CHANNEL_PUBLISHING_PLAN.md](CHANNEL_PUBLISHING_PLAN.md), [BUSINESS_PLAN.md](BUSINESS_PLAN.md)
- **Approval evidence:** None yet

## Purpose

This document will specify the Content Studio: the workflow that turns approved
research output into published social-media content. It defines each stage of
the pipeline, the artefacts each stage produces, and the human gates that sit
between them. It is a planning document only — Priority 3 remains
planning-and-architecture until Priority 1 is live-validated (D-010), and
nothing here authorises building or deploying any publishing workflow.

## Scope and decisions this document will own

- The canonical research-to-content workflow and its stage definitions.
- The claim register concept: how a factual or performance claim is extracted
  from approved research and tracked to every piece of content that uses it.
- Channel formats in scope (per CONTENT-001) and what each format requires
  from the pipeline.
- Content KPIs and the analytics-to-learning feedback loop — definitions only;
  targets are Round M decisions.
- Out of scope: legal/compliance rules (owned by
  [CONTENT_COMPLIANCE_AND_APPROVAL.md](CONTENT_COMPLIANCE_AND_APPROVAL.md)),
  character/brand assets (owned by
  [AI_CHARACTER_AND_BRAND_SPEC.md](AI_CHARACTER_AND_BRAND_SPEC.md)),
  platform accounts and publishing mechanics (owned by
  [CHANNEL_PUBLISHING_PLAN.md](CHANNEL_PUBLISHING_PLAN.md)), and commercial
  strategy (owned by [BUSINESS_PLAN.md](BUSINESS_PLAN.md)).

## Structure skeleton

### 1. Workflow overview

End-to-end stage map: approved research → claim register → compliance review →
script/storyboard → media generation → human approval → publish → analytics →
learning. Each stage will name its inputs, outputs, owner, and gate. Stage
definitions drafted here; owner sign-off in Round M.

### 2. Stage: approved research intake

What qualifies as "approved research" that may enter the content pipeline, and
how provenance is preserved from research artefact to content artefact.
Depends on the Research Centre planning (RES-002 provenance model); alignment
resolved in Rounds L/M.

### 3. Stage: claim register

How claims are extracted, classified (factual, performance, forward-looking),
and given IDs so compliance review and recordkeeping can trace every published
statement to its evidence. Register design resolved in Round M; performance-
claim rules themselves belong to CONTENT_COMPLIANCE_AND_APPROVAL.md.

### 4. Stage: compliance review

The hand-off point into the compliance checklist. This section will define
when review happens and what a pass/fail means for the pipeline; the checklist
content is owned by CONTENT_COMPLIANCE_AND_APPROVAL.md and is blocked on Q-006.

### 5. Stage: script and storyboard

Script, storyboard, and shot-list artefacts per channel format; tone and voice
constraints inherited from the character/brand spec. Tone itself is an open
Round M question.

### 6. Stage: media generation

How generated video/audio/image assets are requested, versioned, and linked to
the character bible's consistency assets. Provider selection is an open Round M
research task (see AI_CHARACTER_AND_BRAND_SPEC.md) — no vendor is assumed here.

### 7. Stage: human approval

Human approval before publish, always (CONTENT-001). Defines the approval
artefact, who approves (Jacob, per D-008 sole-operator context), and what a
rejection loop looks like. Gate mechanics shared with CHANNEL_PUBLISHING_PLAN.md.

### 8. Stage: publish

Interface to the publishing plan: what the studio hands over (approved asset,
metadata, disclosures) and what it receives back (publish confirmation,
failure states). Mechanics owned by CHANNEL_PUBLISHING_PLAN.md.

### 9. Stage: analytics and learning

Which signals are ingested per channel, how they are attributed back to
claims/formats/topics, and how learning proposals are made without bypassing
human approval. KPI definitions and targets are Round M decisions.

### 10. Channel format matrix

YouTube long-form, YouTube Shorts, TikTok, Facebook, Instagram (CONTENT-001):
per-format requirements (length, aspect, captioning, disclosure placement).
Format-specific rules confirmed in Round M against platform policies gathered
in CONTENT_COMPLIANCE_AND_APPROVAL.md.

## Known inputs

- Channels in scope: YouTube long-form and Shorts, TikTok, Facebook, Instagram
  (CONTENT-001).
- Human approval before publish is mandatory; nothing auto-publishes
  (CONTENT-001 acceptance criterion).
- Priority 3 is planning-only until P1 is live-validated (D-010, BUS-006).
- The content business is assessed separately for its own compliance needs
  (D-008).
- Compliance controls and jurisdiction review are prerequisites to any first
  publish (CONTENT-003, blocked on Q-006).

## Open questions

- Target audience definition — Round M.
- Brand position and differentiators — Round M.
- Target countries/markets (also drives jurisdiction review) — Round M / Q-006.
- Tone of voice and editorial style — Round M.
- Funnel design, offers, and monetisation model — Round M (with
  BUSINESS_PLAN.md; no revenue figures may be assumed).
- Content KPIs and their targets — Round M.
- Cadence and volume per channel — Round M.
- How Research Centre provenance (RES-002) maps onto the claim register —
  Rounds L/M.
