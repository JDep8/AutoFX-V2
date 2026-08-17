# V1 Reuse Register

- **Owner:** Jacob Depares
- **Status:** Living register (empty — populated by the V1 audit)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-17
- **Dependencies:** V1_AUDIT.md
- **Approval evidence:** Per-item

Every V1 asset assessed gets exactly one classification, with evidence and
risk. Nothing is copied whose licence, provenance, validity, or holdout status
is unknown. "It ran in V1" is not evidence of correctness.

## Classification scale

| Label | Meaning |
|-------|---------|
| `REUSE_AS_IS` | Proven correct with evidence; licence clean; may be reused unchanged (still requires owner approval + no-build gate) |
| `REFACTOR` | Sound concept, implementation needs rework |
| `RE_DERIVE` | The idea is right; re-derive from first principles rather than port code |
| `REFERENCE_ONLY` | Useful to read for lessons; never executed or ported |
| `DISCARD` | Wrong, unsafe, or superseded |
| `UNKNOWN` | Not yet assessed — the default for everything |

## Register

| V1 asset | Classification | Evidence | Risk | Decision ref |
|----------|----------------|----------|------|--------------|
| *(entire V1 repository)* | `UNKNOWN` | Audit not started | — | — |
| `101005649.rdp` (repo root) | `DISCARD` (security flag) | RDP file in version control; contents never read | Credential exposure | See V1_AUDIT.md § Security flags |
