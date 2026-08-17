# Channel Publishing Plan

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (skeleton — no content owner-approved)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** [DECISION_LOG.md](../00-governance/DECISION_LOG.md) (D-008, D-010), [REQUIREMENTS_CATALOGUE.md](../01-discovery/REQUIREMENTS_CATALOGUE.md) (CONTENT-001, CONTENT-003, SEC-001), [CONTENT_STUDIO_PRODUCT_SPEC.md](CONTENT_STUDIO_PRODUCT_SPEC.md), [CONTENT_COMPLIANCE_AND_APPROVAL.md](CONTENT_COMPLIANCE_AND_APPROVAL.md)
- **Approval evidence:** None yet

## Purpose

This document will plan how approved content actually reaches each platform:
accounts, permissions, security, scheduling, failure handling, and analytics
ingestion. It is the operational counterpart to the Content Studio workflow.
Planning only — the no-build gate explicitly forbids deploying publishing
workflows, and Priority 3 remains planning-and-architecture until Priority 1
is live-validated (D-010).

## Scope and decisions this document will own

- Platform account structure and API/permission model per channel.
- Account security posture for all publishing credentials and access.
- The draft-versus-publish rights split and how the human approval gate is
  technically enforced at the platform boundary.
- Scheduling, failure handling, and analytics ingestion design.
- Out of scope: what content is made and why
  ([CONTENT_STUDIO_PRODUCT_SPEC.md](CONTENT_STUDIO_PRODUCT_SPEC.md)) and the
  compliance checklist content
  ([CONTENT_COMPLIANCE_AND_APPROVAL.md](CONTENT_COMPLIANCE_AND_APPROVAL.md)).

## Structure skeleton

### 1. Channel and account inventory

The accounts/brand channels per platform (YouTube long-form and Shorts,
TikTok, Facebook, Instagram — CONTENT-001) and how they relate to the brand
defined in [AI_CHARACTER_AND_BRAND_SPEC.md](AI_CHARACTER_AND_BRAND_SPEC.md).
Account structure decided in Round M.

### 2. Platform permissions and API capabilities

Per platform: what its API permits for upload, draft, schedule, and publish;
required app review/approval processes; and rate or policy constraints.
Evidence gathered with retrieval dates in Round M research — no capability is
assumed.

### 3. Account security

Credential storage, multi-factor authentication expectations, least-privilege
access, and recovery planning for each platform account, consistent with
SEC-001 (no credentials ever exposed or committed). Detailed posture aligned
with the security round (Round N); channel specifics in Round M.

### 4. Draft-versus-publish rights

The permission split that makes auto-publish impossible: automated processes
may at most stage drafts; the publish right is reserved to the human approver
(CONTENT-001). How each platform's permission model supports or limits this
split is a Round M research finding.

### 5. Approval gate enforcement

How the human approval recorded in
[CONTENT_COMPLIANCE_AND_APPROVAL.md](CONTENT_COMPLIANCE_AND_APPROVAL.md) is
technically bound to the publish action, and what evidence is captured at
publish time. Designed in Round M.

### 6. Scheduling

How approved content is scheduled per channel, timezone handling, and rules
for withdrawing or amending scheduled items before they go live. Cadence
itself is a Round M decision in CONTENT_STUDIO_PRODUCT_SPEC.md.

### 7. Failure handling

Behaviour on upload failure, partial publish across channels, platform
rejection or moderation flags, and takedown/correction procedures for content
found defective after publish. Policies defined in Round M; correction
procedures must align with compliance recordkeeping.

### 8. Analytics ingestion

Which metrics are collected per platform, via what interface, at what
frequency, and how they feed the learning stage of the content workflow.
Metric availability is per-platform Round M research; KPI definitions live in
CONTENT_STUDIO_PRODUCT_SPEC.md.

### 9. Operational calendar and roles

Who does what in the publishing cycle. Under D-008 the operator is Jacob;
whether any function is ever delegated or contracted is a BUSINESS_PLAN.md
Round M question.

## Known inputs

- Channels in scope: YouTube long-form and Shorts, TikTok, Facebook, Instagram
  (CONTENT-001).
- Human approval before publish, always; nothing auto-publishes (CONTENT-001).
- No publishing workflow may be deployed under the no-build gate; Priority 3
  is planning-only until P1 is live-validated (D-010, BUS-006).
- No credentials, tokens, or account identifiers are ever exposed or committed
  (SEC-001).
- Compliance sign-off per jurisdiction precedes any first publish
  (CONTENT-003, blocked on Q-006).

## Open questions

- Per-platform API capabilities and permission models, with dated evidence —
  Round M research.
- Whether each platform can technically enforce a draft-only automation role,
  and the fallback control where it cannot — Round M.
- Account structure (single brand account per platform vs. any split) —
  Round M.
- Scheduling and cadence policy — Round M.
- Failure, rejection, and takedown procedures — Round M.
- Analytics metrics, ingestion method, and retention — Round M.
- Delegation of any publishing role beyond Jacob — Round M
  ([BUSINESS_PLAN.md](BUSINESS_PLAN.md) operating model).
