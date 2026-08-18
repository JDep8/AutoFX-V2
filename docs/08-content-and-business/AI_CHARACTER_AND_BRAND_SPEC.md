# AI Character and Brand Specification

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-008, D-010), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (CONTENT-002, CONTENT-003), [CONTENT_STUDIO_PRODUCT_SPEC.md](CONTENT_STUDIO_PRODUCT_SPEC.md), [CONTENT_COMPLIANCE_AND_APPROVAL.md](CONTENT_COMPLIANCE_AND_APPROVAL.md)
- **Approval evidence:** None yet

## Purpose

This document will define the repeatable AI character(s) and brand assets used
in the content business, in the form of a character bible, plus the evidence-
based evaluation that selects the media-generation provider(s). It exists so
that character identity, rights, disclosure, and consistency are decided and
owner-approved before any media is generated. It is planning-only until
Priority 1 is live-validated (D-010).

## Scope and decisions this document will own

- The character bible: everything needed to reproduce the character
  consistently and to prohibit misuse.
- Brand asset inventory (logos, palettes, typography, motion/audio identity)
  and its version control.
- The provider evaluation framework and, later, the evidenced provider
  selection. **No provider — including Higgsfield or any other named vendor —
  may be hard-coded or assumed before a dated comparative evaluation is
  completed and owner-approved** (open Round M research).
- Out of scope: publishing mechanics
  ([CHANNEL_PUBLISHING_PLAN.md](CHANNEL_PUBLISHING_PLAN.md)) and the legal
  checklist itself
  ([CONTENT_COMPLIANCE_AND_APPROVAL.md](CONTENT_COMPLIANCE_AND_APPROVAL.md)),
  though consent, disclosure, and rights entries here must satisfy it.

## Structure skeleton

### 1. Character bible — identity

Name, role, backstory boundaries, and what the character may and may not claim
to be (e.g. never a licensed adviser). Defined in Round M; claim boundaries
must align with CONTENT_COMPLIANCE_AND_APPROVAL.md.

### 2. Character bible — appearance, voice, wardrobe

Canonical visual description, reference imagery policy, voice characteristics,
and wardrobe rules that keep the character recognisable across formats.
Drafted in Round M once provider capabilities are known.

### 3. Character bible — personality and tone

Personality traits, speech patterns, humour boundaries, and how tone flexes by
channel without breaking character. Tone is an open Round M question shared
with CONTENT_STUDIO_PRODUCT_SPEC.md.

### 4. Prohibited uses

Explicit list of contexts the character must never appear in (e.g. guarantees
of profit, impersonation of real people, undisclosed advertising). Seeded from
CONTENT-003 obligations; finalised in Round M with the compliance document.

### 5. Consistency assets

The concrete artefacts that make the character repeatable: reference sets,
prompts/seeds or provider-native identity assets, style guides, and how they
are stored and versioned. Depends on the provider evaluation (Round M).

### 6. Consent, ownership, and rights

Who owns the generated character and outputs; confirmation that no real
person's likeness or voice is used without documented consent; provider
licence terms for commercial use. Evidence-gathering is Round M research;
legal confirmation is tied to the D-018 review (BUS-008).

### 7. Disclosure

How synthetic-media/AI-generation disclosure is presented per channel, and how
the character self-identifies as AI where required. Rules owned by
CONTENT_COMPLIANCE_AND_APPROVAL.md; placement defined here in Round M.

### 8. Version control

Character and brand-asset versioning: what constitutes a version change, how
versions are approved, and how published content records the character version
used. Process defined in Round M.

### 9. Provider evaluation framework

Comparative, dated-evidence evaluation of candidate media-generation providers
against at minimum: output quality, character consistency, rights and
commercial terms, API/automation support, pricing, content moderation
constraints, and provenance/watermarking support. Method approved in Round M;
results recorded with retrieval dates before any selection.

### 10. Provider selection record

The eventual decision entry: options compared, evidence cited, decision, and
status. Empty until the Round M evaluation completes and Jacob approves.

## Known inputs

- Repeatable AI characters and brand assets with a character bible,
  consent/ownership, disclosure, and version control are required
  (CONTENT-002).
- Provider licensing must be verified before use (CONTENT-002 acceptance
  criterion).
- Synthetic-media disclosure, provenance, and impersonation-risk controls are
  compliance requirements (CONTENT-003).
- Priority 3 is planning-only until P1 is live-validated (D-010, BUS-006).

## Open questions

- Which providers to evaluate, and the evaluation results — Round M (dated
  evidence required; no vendor pre-selected).
- Character concept, count, and identity — Round M.
- Voice sourcing and any voice-consent requirements — Round M (legal aspects
  → the D-018 review, BUS-008).
- Ownership position on AI-generated character IP per provider terms —
  Round M (legal confirmation via the D-018 review, BUS-008).
- Disclosure wording and placement per channel — Round M, with
  CONTENT_COMPLIANCE_AND_APPROVAL.md.
- Brand asset inventory and naming — Round M, with BUSINESS_PLAN.md brand
  position.
