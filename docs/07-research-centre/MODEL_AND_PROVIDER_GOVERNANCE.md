# Model and Provider Governance
- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [RESEARCH_CENTRE_PRODUCT_SPEC.md](RESEARCH_CENTRE_PRODUCT_SPEC.md), [RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md), [QUESTION_REGISTER.md](../00-governance/QUESTION_REGISTER.md) (Q-003), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (RES-001, RES-004)
- **Approval evidence:** None yet

## Purpose

This document governs how AI models and providers are selected, combined and
constrained inside the Research Centre. It exists so that model choice is a
deliberate, recorded decision — never a habit — and so that legally or
contractually risky access patterns are blocked until Jacob explicitly clears
them. It is distinct from
[MODEL_GOVERNANCE.md](../05-research-and-validation/MODEL_GOVERNANCE.md),
which governs quantitative/statistical models in the P1 research pipeline.

## Scope and decisions this document will own

- The criteria and process for selecting a model/provider per research task.
- Rules for multi-model orchestration and independent challenge (RES-001).
- The headless consumer-AI boundary and its resolution path (Q-003, RES-004).
- The comparison and approval of permitted access approaches (API/SDK, managed
  agent, user-operated/manual, other licensed routes).
- It does **not** own provenance record structure (see
  [RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md)).

## Structure skeleton

### 1. Selection criteria

The per-task dimensions on which a model/provider is chosen: task quality,
independence from other models used on the same question, cost, latency,
privacy, data retention, and permitted automation under the provider's terms.
How the dimensions are weighted and evidenced is resolved in Round L.

### 2. Multi-model orchestration rules

When multiple models may be used on one question and how their outputs are
combined. Hard rule carried from RES-001: agreement between models is **never**
equated with truth — every consequential finding requires source evidence plus
an independent challenge pass. Orchestration patterns resolved in Round L.

### 3. Independence and challenge-pass requirements

What makes a verifier "independent" (different model, provider, prompt
lineage, or human), and which findings are consequential enough to require the
challenge pass. Definitions resolved in Round L; the requirement itself is
fixed by RES-001.

### 4. Headless consumer-AI boundary

Automating paid ChatGPT/Claude consumer UIs headlessly is `BLOCKED` (Q-003,
RES-004) unless current provider terms **and** Jacob's legal/security review
explicitly permit it. The review must cover: the provider's terms for research
use, authorised integration surfaces, data handling, automation restrictions,
account risk, anti-bot behaviour, and reproducibility. This section records
the dated terms research and the sign-off when they exist. Resolution path:
Q-003 dated research brief, then Jacob's explicit decision in Round L.

### 5. Comparison of access approaches

A structured comparison — no approach pre-selected — of: official API/SDK
access, managed agent platforms, user-operated/manual workflows, and other
licensed approaches. Criteria mirror Section 1 plus terms compliance.
Comparison performed and decided in Round L; nothing here names a preferred
vendor.

### 6. Privacy and data-retention constraints

What research content may be sent to which provider class, what retention the
provider applies, and what must never leave the environment (credentials,
account identifiers, private data — SEC-001). Provider-specific retention
facts require dated terms research in Round L; never assumed.

### 7. Change management for models and providers

How a model/provider/version change is proposed, evaluated against the
benchmark set (see
[RESEARCH_PROVENANCE_AND_EVALUATION.md](RESEARCH_PROVENANCE_AND_EVALUATION.md))
and approved before it can affect outputs that feed trading decisions.
Process resolved in Round L.

### 8. Register of approved models and providers

The living register (identity, version, permitted tasks, access approach,
approval status using only the repository status vocabulary). Empty until
Round L decisions exist — no provider is listed speculatively.

## Known inputs

- RES-001 (`PROPOSED`): multi-model use only where it materially improves
  quality; agreement never equals truth; challenge pass required.
- RES-004 (`PROPOSED`) / Q-003 (`BLOCKED`): headless automation of paid
  consumer AI UIs is blocked pending dated terms research and Jacob's
  legal/security review.
- D-010 (`OWNER_APPROVED`): all of this is planning-only until P1 is
  live-validated.
- SEC-001 (`PROPOSED`): no credentials, tokens, account identifiers, or
  private data exposed to any external party.

## Open questions

- Which providers' terms permit which automation, at what retention, for
  research use? → Q-003 dated research brief; Round L.
- Weighting and evidence standard for the selection criteria? → Round L.
- What counts as an "independent" challenge pass in practice? → Round L.
- Which access approach (API/SDK, managed agent, user-operated, other
  licensed) per task class? → Round L.
- Cost and latency envelopes acceptable to Jacob? → Round L, within the
  D-019 ceiling (AUD 400/month, per-expense approval).
