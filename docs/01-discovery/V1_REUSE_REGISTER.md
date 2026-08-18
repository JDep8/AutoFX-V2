# V1 Reuse Register

- **Owner:** Jacob Depares
- **Status:** Living register — **populated by the repository-side V1 audit
  2026-08-18** (Issue #21). Classifications are Claude recommendations
  `PROPOSED` for later rounds; none is owner-approved. No V1 code copied.
- **Version:** 1.0.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** V1_AUDIT.md
- **Approval evidence:** Per-item; audit authorisation Issue #21

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

## Disposition vocabulary mapping

The Issue #21 disposition codes map onto this register's scale:
`RETAIN_CONCEPT`→`RE_DERIVE`/`REFERENCE_ONLY`; `REDESIGN`→`REFACTOR`;
`REPLACE`→`RE_DERIVE` (rebuild, do not port); `REMOVE`→`DISCARD`;
`INVESTIGATE_IN_ROUND_B`→`UNKNOWN` (pending a named round);
`NO_V2_RELEVANCE`→`REFERENCE_ONLY`/`DISCARD`. Evidence strength: Direct /
Corroborated / Inferred / Insufficient (per V1_AUDIT.md).

## Register (all rows `PROPOSED` — recommendations for later rounds)

| V1 asset | Classification | Disposition (Issue #21) | Evidence | Risk if reused wrong | Round |
|----------|----------------|-------------------------|----------|----------------------|-------|
| **Overall V1 codebase** | `REFERENCE_ONLY` | RETAIN_CONCEPT / REPLACE | Corroborated: unpublished state (HEAD 60 ahead of origin, CI never ran); no validated profitability | Inheriting an unvalidated platform | B/N |
| `portfolio_backtest/engine.py` (backtester) | `RE_DERIVE` | REPLACE | Direct: trailed-stop look-ahead sizing; −1R clamp; static QUOTE_USD; compounding-default vs artifacts-at-False | Fabricated backtest edge carried into V2 | F |
| Engine realism features (quote→USD, per-bar spread, stop-exit slippage, gap-through-stop, lot-round+risk-recompute) | `REFERENCE_ONLY` | RETAIN_CONCEPT | Direct: each proven load-bearing by V1 getting it wrong | Missing a realism dimension | F |
| `generator.py` `ParametricStrategy` families | `REFACTOR` | REDESIGN | Direct: family taxonomy sound; carries the sizing defect + hand-mirrored live copy | Signal/exit drift; look-ahead | F/G |
| `pipeline.py` selection/assembly + robustness gate | `RE_DERIVE` | REPLACE | Corroborated: PBO-on-survivors, DSR mis-count, per-symbol holdout cut, ranking carries no OOS info | Leakage; false acceptance | G/H |
| `universe.py` measured-eligibility rule | `RE_DERIVE` | RETAIN_CONCEPT | Direct: no hand-list; measured hour-presence + provenance | — (good pattern) | C/D |
| Per-(symbol,month) coverage table + provenance fingerprint | `RE_DERIVE` | RETAIN_CONCEPT | Corroborated | — | D |
| Data platform (`data_feeds/data_prep/dukascopy_*/surface_*/bar_disposition`) | `RE_DERIVE` | REPLACE | Corroborated: contamination, cost look-ahead, stub fundamentals, no `tf` column, no quarantine state | Contaminated/lookahead data into V2 | D |
| Dukascopy real-per-bar-spread backfill | `REFERENCE_ONLY` | RETAIN_CONCEPT | Direct | — | D |
| `metrics.py` drawdown definitions | `RE_DERIVE` | REDESIGN | Direct: base-relative still shipped vs decided peak-relative (D80) | Divergent DD numbers | E |
| Canonical drawdown direction (D80: closed-realised, peak-relative) | `REFERENCE_ONLY` | RETAIN_CONCEPT | Corroborated: corroborates V2 D-001 | — | E |
| Runtime risk controls / heat / survivability | `RE_DERIVE` | REDESIGN | Corroborated: heat bounds 0/8 mechanisms, in-sample only, "Off" disables; DD limit not a runtime gate | Undetected catastrophic loss | E/J |
| ML pipeline (`ml_method`/`ml_meta`) | `REFERENCE_ONLY` | INVESTIGATE_IN_ROUND_B | Corroborated: embargo<horizon leakage, train-on-self drove selection | Leakage | G |
| `statarb`/`xsec` (validation-only) | `REFERENCE_ONLY` | INVESTIGATE_IN_ROUND_B | Corroborated: synthetic-envelope realism, zero-swap pairs, never live-wired | Unrealistic pair fills | G/I |
| `live/` layer (signal_service/strategy_live/ctrader_client) | `RE_DERIVE` | REPLACE | Direct: latest-bar-only eval, no reconciliation, no weekend flatten, dead kill-switch | Live-safety failure | J |
| `code/TradingViewBridge.cs` (order bridge) | `RE_DERIVE` | REPLACE | Direct: naked-SL, tp=0, phantom-close, 200-before-trade, all-interfaces bind, token logged | Naked/duplicate/phantom live orders | J |
| Bridge fail-closed patterns + read-only `sizecheck` | `REFERENCE_ONLY` | RETAIN_CONCEPT | Direct: fail-closed auth/`riskMult`; sizecheck = certification precursor (D-034 Mode C) | — | J |
| Per-symbol `riskMult` percentage weighting | `DISCARD` | REMOVE | Direct: disabled in V1 (anti-correlated, cap-breaching); D-023/EXEC-011 excludes it | Divergent sizing | J |
| `code/PriceBridge.cs` (bar server) | `RE_DERIVE` | REPLACE | Direct: read-only price feed; same infra weaknesses | — | J |
| Test/hermetic harness + `guard_live_paths` hook | `RE_DERIVE` | RETAIN_CONCEPT | Direct: reproducibility harness good; gate misses `code/*.cs`; CI never authoritative | False "green" | F/N |
| Governance vocabulary + gate-quality clauses | `REFERENCE_ONLY` | RETAIN_CONCEPT | Corroborated: most reusable single artefact | — | all |
| 26-gate scoreboard (as built) | `RE_DERIVE` | REDESIGN | Corroborated: zero gates can refuse a book | Unenforced gates | H/I/N |
| `run_backtest.py` demo path, `_d3c.py`/`_d3probe.py`, 6 zero-caller control modules | `DISCARD` | REMOVE | Corroborated: dead/scratch/superseded | Dead-code inheritance | B |
| Hard-coded constants (account/risk/universe/QUOTE_USD/close_hour/paths) | `DISCARD` | REDESIGN | Direct: must be versioned config/data | Hidden assumptions | C/D/E |
| `101005649.rdp` (repo root) | `DISCARD` | REMOVE | Direct: RDP file in version control; contents never read | Credential exposure | owner action |
| V1 profitability figures / reference book | `DISCARD` (as evidence) | NO_V2_RELEVANCE | Corroborated: retired/corrected/untrusted by V1's own later measurement | Citing a fabricated edge | B (Q-010) |
