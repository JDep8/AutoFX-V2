# Video and External Content Policy
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-004), [DATA_LICENSING_AND_RETENTION.md](../04-data/DATA_LICENSING_AND_RETENTION.md), [RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md), [MODEL_AND_PROVIDER_GOVERNANCE.md](MODEL_AND_PROVIDER_GOVERNANCE.md)
- **Approval evidence:** None yet

## Purpose

Jacob sometimes finds trading-strategy ideas in YouTube videos and wants the
Research Centre to analyse them. This document defines what the system may
lawfully access, process and retain from user-supplied videos and other
external content, and what it must never do. The governing principle: the
Research Centre never evades platform controls, and where lawful access is
uncertain, the compliant fallback is content Jacob supplies himself.

## Scope and decisions this document will own

- The lawful-access boundary for user-supplied video content: metadata,
  captions, transcripts, audio, screenshots, and derived content (Q-004).
- The compliant-fallback workflow (user-supplied notes/transcripts or
  otherwise authorised access).
- Retention and provenance rules for external content used in research.
- It does **not** own general data-source licensing (see
  [DATA_LICENSING_AND_RETENTION.md](../04-data/DATA_LICENSING_AND_RETENTION.md))
  or the content-publishing business (Priority 3, Round M).

## Structure skeleton

### 1. Lawful-access boundary per content type

For each content type — video metadata, captions, transcripts, audio,
screenshots, derived summaries — what may be accessed and retained under
current platform terms and applicable law. Known constraint to verify: the
official captions API does not generally grant arbitrary caption downloads
for videos the user does not control. Resolved by the Q-004 dated research
brief in Round L; nothing is assumed permitted here.

### 2. Prohibited techniques

Hard rule: never evade platform controls — no scraping behind
authentication walls, no circumvention of rate limits, bot detection, DRM,
or region restrictions, regardless of how useful the content would be.
This rule is fixed now; Round L only details detection and enforcement.

### 3. Compliant fallback workflow

When direct access is not clearly lawful: Jacob supplies his own notes, a
transcript he is entitled to provide, or access through an authorised route.
The workflow's steps, templates and quality expectations are resolved in
Round L.

### 4. Provenance and epistemic handling of video-derived claims

Strategy claims extracted from videos are recorded with full provenance
(source video identity, retrieval route, date) and classified as hypothesis —
never fact — until independently evidenced, per
[RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md).
Classification detail resolved in Round L.

### 5. Retention and snapshot rules

What external content may be stored, for how long, and whether
snapshots/hashes are permitted under the platform's terms. Resolved in
Round L with the Q-004 brief and
[DATA_LICENSING_AND_RETENTION.md](../04-data/DATA_LICENSING_AND_RETENTION.md).

### 6. Other external content classes

The same boundary questions applied to non-video content the Research Centre
may encounter (articles, forums, papers, paid research). Scope and per-class
rules resolved in Round L; paywalled and licensed content is never accessed
outside its licence.

### 7. Review and change control

How this policy is re-verified when platform terms change, and who signs off
changes (Jacob). Cadence resolved in Round L.

## Known inputs

- Q-004 (OPEN): the lawful access boundary for user-supplied YouTube strategy
  videos is unresolved; a compliant fallback (user-supplied notes/transcripts)
  exists and is usable meanwhile.
- Owner mandate: never evade platform controls — fixed rule, not open for
  optimisation.
- RES-002 (`PROPOSED`): all external-content-derived findings carry full
  provenance; citations are never fabricated.
- D-010 (`OWNER_APPROVED`): planning-only until P1 is live-validated.

## Open questions

- Exactly which YouTube content types are lawfully accessible and retainable
  for videos Jacob does not control? → Q-004 dated research brief; Round L.
- What authorised access routes (official APIs, licensed services, owner
  authorisation) exist and at what cost? → Round L.
- Retention periods and snapshot permissions per content class? → Round L.
- How are terms-of-service changes monitored and this policy re-reviewed? →
  Round L.
