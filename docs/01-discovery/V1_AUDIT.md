# V1 Forensic Audit (read-only)

- **Owner:** Jacob Depares
- **Status:** `OWNER_APPROVED` authorisation to run (Issue #21, 2026-08-18);
  audit **PERFORMED** 2026-08-18 (repository-side, read-only); findings are
  evidence records, not owner decisions. Every V2 disposition below is a
  Claude recommendation `PROPOSED` for a later round — none is approved.
- **Version:** 1.0.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** V1_REUSE_REGISTER.md, `.claude/rules/security-and-secrets.md`,
  DECISION_LOG.md (D-022, D-023, D-036), QUESTION_REGISTER.md (Q-010, Q-005)
- **Approval evidence:** Owner go for the repository-side audit (Issue #21)

V1 is inspected for **lessons, not authority**. Three things are kept
separate: what exists, what is proven, and what is recommended. V1 tests
are never treated as proof of correctness — only what each test actually
demonstrates is recorded. No V1 file was modified; nothing was cloned into
V2; no code was copied; no database, broker, or network was touched.

## Method and evidence base

- **Access:** read-only via authenticated `gh` (contents API + git trees +
  commits API). Two refs inspected: `main` (default; 244 commits) and
  `statgate-integration` (104 commits ahead of `main`; the last active
  work, dated 2026-07-27 → 2026-08-15). Neither ref is a published state —
  the statgate corpus records HEAD as **60 commits ahead of origin** with CI
  never having seen the tree.
- **Corpus:** ~230 files in the `main` tree (137 `.py`, 55 `.md`, 2 `.cs`,
  plus json/yml/bat); a curated 94-file evidence subset was fetched locally
  read-only for close reading (both cBots, the live layer, the engine and
  key `portfolio_backtest/` modules, the config/deploy surface, and ~40 V1
  review/decision/spec documents across both refs).
- **Delegation (governor-routed, read-only):** `autofx-sonnet-analyst`
  produced the deterministic code catalogue (strategies, hidden
  assumptions, duplication, tests, config); `autofx-opus-reviewer` produced
  the prior-review-claims inventory and challenge pass. The main Fable
  session read the fidelity- and safety-critical evidence directly
  (contamination, look-ahead sizing, canonical drawdown, the bridge,
  gate status, forward-test protocol) and performed final acceptance.
- **Evidence strength labels used below:** **Direct** (verified in fetched
  code this session), **Corroborated** (multiple V1 documents agree, or a
  document claim matched to fetched code), **Inferred** (reasoned from
  evidence), **Insufficient** (documented but not verifiable from the
  fetched set). Line-number citations are against the fetched copies and
  should be re-confirmed against V1 HEAD before reuse.

## Access state (verified 2026-08-18)

| Asset | State |
|-------|-------|
| Repository `JDep8/AutoFX` | Private; read-only VERIFIED via `gh`. Python/C#/JS/Batch; default branch `main`; second branch `statgate-integration`; no tags; pushed 2026-08-15. |
| PostgreSQL database | **Not accessed** — DB-side audit deferred (D-022 provisioning of `autofx_v1_readonly` outstanding). All DB-state claims below are `Insufficient` by construction and taken from V1's own documents. |
| cBot / execution bridge | **Located and read** (D-023): `code/TradingViewBridge.cs` (order submission) + `code/PriceBridge.cs` (bar serving). |
| Broker statements / live fills | None exist to request — V1 records **zero real fills** (all 158 `trade_history` rows are `dry_run`). |

## Security flags (recorded; contents never read)

- `101005649.rdp` committed at V1 root (1,102 bytes) — remote-desktop
  connection file in version control. Never opened/echoed; recommend Jacob
  rotates any embedded credential and removes it from V1 history at his
  discretion.
- **Secret material found in-repo (locations only, values never
  reproduced):** the cBot prints the full incoming JSON — including the
  shared auth token — to its log on every signal
  (`code/TradingViewBridge.cs:225`); the cTrader access token is logged by
  `live/ctrader_client.py:45`; the FMP key is passed in a URL query string
  (`webui.py:1193`); a V1 demo **account identifier** appears in several
  `.md` files. None copied into V2.

---

## System map (Area 1 — architecture)

V1 is a single-Windows-VPS Python research platform. **Direct/Corroborated.**

- **UI/orchestration:** `webui.py` + `ui_panels.py` (Streamlit); `jobs.py`
  runs symbol×timeframe generation units on a process pool with
  checkpoint/resume; `store.py` is the single Postgres(+DuckDB-fallback)
  data-access layer.
- **Generation/backtest:** `portfolio_backtest/` — `engine.py` (the
  backtester), `generator.py` (`ParametricStrategy` families + exits),
  `pipeline.py` (orchestration + the one robustness gate + book assembly),
  `robustness.py` (DSR/PBO/bootstrap/walk-forward), `metrics.py`,
  `instruments.py` (67-symbol universe + per-symbol cost table),
  `ml_method.py`/`ml_meta.py`/`statarb.py`/`xsec.py`. Nine methods:
  `technical, meanrev, seasonal, regime, newsrx, ml, ml_meta, statarb,
  xsec` (live-tradeable: the first six minus newsrx; validation-only:
  statarb/xsec/newsrx).
- **Data platform:** `data_feeds.py` (FRED rates + COT + calendar),
  `data_prep.py`/`dukascopy_*`/`import_*`/`surface_*`/`bar_disposition.py`
  (ingestion, repair, coverage), `data_health.py`/`data_audit.py`
  (monitoring), `deep_coverage.py`.
- **Live layer:** `live/signal_service.py` (poll loop), `live/strategy_live.py`
  (bar-by-bar evaluators mirroring `ParametricStrategy`), `live/ctrader_client.py`
  (HTTP client to the cBot), `live/config.py`.
- **Execution bridge (cTrader cBots, C#):** `TradingViewBridge` (orders,
  `localhost:6000`) + `PriceBridge` (bars, `localhost:6001`); a Cloudflare
  tunnel exposes a hostname to `localhost:6000`.
- **Governance-in-code:** `.claude/hooks/guard_live_paths.py`,
  `tools/decisions_lint.py`, a 26-gate scoreboard, a hermetic test harness.

**Structural weaknesses V1 itself records (Corroborated):** four competing
configuration sources needing unification (ROADMAP.md:274); generation
orchestration duplicated between `jobs.run_job` and
`pipeline.generate_portfolio` and "already drifted" (ROADMAP.md:279); 55
bare `except: pass` blocks, implicated in a bars-corruption incident
(ROADMAP.md:261). → **V2 disposition: REDESIGN** the architecture around
the V2 pillars; **RETAIN_CONCEPT** for the module decomposition and the
in-code governance idea; do not inherit the config sprawl or the duplicated
generation path.

## Data platform (Area 2) and point-in-time integrity

**Critical, safety-material. Corroborated by multiple V1 documents; several
items Direct.**

- **No timeframe/resolution column** in `bars` (PK `symbol, ts`), so daily
  bars can pollute an M1 store and a partial daily fill can look complete
  (DATA_AND_GENERATOR_REVIEW). → V2 must key bars by resolution and
  provenance.
- **Cost look-ahead:** today's spreads/swaps were applied across five years
  of history; measured real spread covers only **23.94% of 2020+ bars —
  3.91% for FX majors**; every crypto spread in `spread_samples` is a
  zero-variance placeholder ("no crypto cost has ever been measured").
- **Fundamentals were stubs:** FRED stored `limit:1` (latest only, wiped
  each refresh) → `rate_trend` literally a dead method; COT last-730-days
  and wiped.
- **Point-in-time defects:** inception stamped on truncated/error imports
  (`_confirm_inception`); UTC not enforced on save/load; D/W bars binned on
  UTC midnight while cTrader opens on the broker server-day (~21–22:00 UTC),
  shifting every daily OHLC by ~2–3h with `D` on by default.
- **Data contamination (the load-bearing finding):** **ADAUSD's bars are
  Litecoin's — 40.3% of the series, 1,041,385 identical rows**; **BCHUSD
  2026-04 is 98.4% Solana**; **SOLUSD ran on fabricated one-bar-per-day
  data** for ~5 of 6.5 in-sample years. The equality-matching scan
  understated contamination ~7× (statarb legs are named `LEG1~LEG2`). A
  CONTAMINATED disposition state **does not exist** in `bar_disposition.py`;
  the quarantine mechanism was designed but **not enacted**. LTCUSD — the
  donor — is the only crypto **not** excluded from generation.
- **Reproducibility:** generation output is not reproducible (100% of
  re-scored candidates showed changed trade counts within 12 days because
  bars/calendar were rewritten underneath jobs); the book of record has no
  bars manifest, no cost snapshot, 3 of 48 config keys, no code revision.
  V1's own verdict: everything before the manifest work is "permanently
  unreproducible — a taken loss, not a gap."

→ **V2 disposition: REPLACE** the data platform; **RETAIN_CONCEPT** for the
per-(symbol,month) coverage table, the measured-universe rule
(`universe.py`), the Dukascopy real-per-bar-spread backfill, and the
provenance fingerprint. **INVESTIGATE_IN_ROUND_B/D**: whether any V1 stored
data is clean enough to seed V2's point-in-time archive, or whether V2
re-acquires from scratch (contract-first, DATA-004/005).

## Backtest fidelity (Area 3) — and backtest-to-live divergence

See the dedicated ranking below; this is the single most important area for
the V2 backtest-fidelity pillar. **Direct on the two headline defects.**

## Strategies and signals (Area 4)

Real generation+live engine is `ParametricStrategy` (`generator.py`), which
`live/strategy_live.py` re-implements bar-by-bar (documented duplication →
drift risk). Families: trend_ma, breakout, rsi_reversion,
bollinger_reversion, momentum, vol_breakout, plus meanrev/seasonal/regime/
newsrx groups and optional carry/COT filters; ML (triple-barrier),
ml_meta, statarb (cointegration pairs), xsec (cross-sectional). Enable/
disable is an `enabled` flag on the approved-strategy DB row. `news_react`
and `xsec` are dead in live (skipped). **Direct.** → **RETAIN_CONCEPT** for
the parametric family taxonomy and the live/backtest-parity intent;
**REDESIGN** to a single shared strategy implementation (no hand-mirrored
second copy) per the V2 one-authoritative-engine principle.

## Optimisation / model selection (Area 5)

Multiple-testing machinery exists (Deflated Sharpe, PBO/CSCV, purged k-fold
with embargo, block bootstrap, walk-forward) but V1's own reviews found
each **mis-applied**: PBO ran on post-selection survivors; DSR undercounted
trials and ignored skew/kurtosis; the CV embargo (0.01) was shorter than
the 24-bar label horizon (leakage); the bootstrap resampled the merged
trade list; the holdout cut was per-symbol fractional, not one calendar
date. The later corpus is blunter: the shipped per-trade Sharpe ranking
"carries zero out-of-period information" (pseudo-OOS median = population
median; 32 of 38 shipped members were top-150 by `sr` and **none** by any
other measure), and DSR was **retired** (D89) with generation blocked until
seven unmet conditions hold. **Corroborated.** → **REDESIGN** entirely for
V2's leakage/holdout policy; **RETAIN_CONCEPT** for the method families as
candidates to research (with limitations), not as a validated pipeline;
**INVESTIGATE_IN_ROUND_G/H**.

## Risk and portfolio management (Area 6)

**Safety-material.** V1 converged (statgate D80–D95) on a canonical
drawdown definition close to V2's stated direction: **closed-position
realised, peak-relative, previous-realised-peak denominator, anchored at
starting capital, one implementation, no module may redefine it** — but
that is a **decision, not code**: the live tree still carries base-relative
drawdown as a gate statistic and multiple divergent computations, and
blocking CI asserts the superseded constant. Findings: the declared DD
limit was generation/approval-only, never a runtime gate; the only runtime
stop is 5% daily on the full 100k (≈67 full-risk losses) — "a catastrophic-
malfunction detector, not risk management"; **heat bounds 0 of 8
account-risk mechanisms** and is enforced in-sample only (breached in 21.8%
of cells; a UI "Off" silently disables it); Catastrophic Survivability is
decided but 1 of 10 chain elements exists. On EURCHF 2015-01-15 (−29.16%)
the engine books −1.00R in 26 of 36 cells against an honest −1.12R to
−116.63R. **Corroborated; canonical-definition ruling Direct in the
statgate register.** → **RETAIN_CONCEPT** for the canonical peak-relative
drawdown direction (it corroborates D-001) and the MTM/heat-as-separate-
controls idea; **REDESIGN** the runtime risk controls; the exact numbers
are Round E (Q-005). This area strongly corroborates the V2 rule that
closed-only drawdown is never sufficient for live safety.

## Execution / cTrader (Area 7) and the TradingView bridge (Area 8)

See the dedicated bridge section below. Headline: **zero real fills ever
recorded**; `store.record_execution` has no callers; the live evaluator
processes only the latest bar per poll (one frozen bar produced 9 entries +
9 exits); no persisted live position state or broker reconciliation on
startup (a restart orphans positions / can double-enter); the live path
does not enforce weekend forced-exit; kill-switch changes are load-time
only; `store.set_strategy_enabled` has zero callers. **Direct/Corroborated.**

## Reliability, testing, operations (Area 9)

~1,981 tests; the 2026-08-12 baseline read **1,906 passed / 25 FAILED**
(22 of 25 on the risk/gate surfaces), `hermetic_check --fast` RED, and the
**hermetic CI job has never run** (HEAD 60 commits ahead of origin; last
real CI 2026-08-03 failing 6 of 6). CI silently opted out on each new
long-lived branch prefix (three recorded incidents). A dedicated
portability test exists **because** hard-coded drive letters were a defect
class. **Direct** (CI file + baseline docs fetched). → **RETAIN_CONCEPT**
for the hermetic-reproducibility harness, the gate-quality vocabulary, and
`guard_live_paths`; **REDESIGN** so gates can actually refuse and CI is
authoritative; note the gate now covers `live/**`+`store.py` but **not**
`code/*.cs` (the program that submits orders).

## Reporting, governance, validation evidence (Area 10)

V1's governance corpus is unusually honest and is its most reusable
artefact: a 26-gate scoreboard, a decisions register with a linter, and a
vocabulary (`UNMEASURED`/`NEVER`/`UNWIRED`/`NONE`; "no number without a
source"; "a gate with no production caller, no forced-failure test and no
CI check is not a gate"). But: **11 gates registered, 8 "binding", and
ZERO can refuse a book on the generation or approval path**; six control
modules with 335+ tests have zero production callers; the activation gate
has never been exercised on a real book. **Corroborated.** → **RETAIN_CONCEPT**
(strongly) for the governance vocabulary and gate-quality clauses — they map
onto V2's acceptance-gate architecture; **REDESIGN** so every gate is wired,
forced-failure-tested, and CI-enforced.

---

## Backtest-to-live divergence — ranked largest first (critical focus)

Every item is an evidenced source of unrealistic backtest results. Ranked
by likely magnitude of live divergence. **Direct** unless noted.

1. **Trailed-stop look-ahead sizing defect.** `generator.py` mutates the
   `stop` variable inside the exit loop and sizes every position off the
   **final trailed** stop distance — only knowable at exit. Trailing moves
   the stop toward entry, so the denominator shrinks *precisely for
   winners*, manufacturing a right tail every selector looks at. Measured:
   97.36% of 5,388 trades sized off a tighter-than-entry stop; median 1.83×
   over-sized; **74.94% of all 43,977 stored candidates and 92–100% of the
   two reference books affected**; a 97-bar placebo is statistically
   indistinguishable from the real signal. **This alone means live can
   never reproduce the backtest, and backtest+live have never sized the
   same trade the same way** (live uses the initial stop).
2. **Data contamination** (Area 2): ADAUSD=Litecoin (40.3%), BCHUSD 2026-04
   =98.4% Solana, SOLUSD fabricated granularity — 23.2%+ of the reference
   book was backtested on the wrong instrument.
3. **Cost unrealism:** 96% of 2020+ bars (99% of FX-major bars) carry no
   measured spread; zero crypto cost ever measured; today's static costs
   applied to all history; the operative optimism belief is 1.83–2.79×.
4. **Static quote-currency conversion:** `QUOTE_USD` is one constant per
   currency applied 2008–2026, fixed at entry (CHF=1.12 while real CHF/USD
   ranged 0.81→1.41, moving +40.5% inside the 2015 gap). Also the original
   B1 defect: commission entered unconverted, understated ~150× on JPY.
5. **The −1R MTM clamp + gap branch:** open trades are clamped at
   `−risk_cash` and the gap branch needs a bar to *open* beyond the stop
   (rare on M1), so a −$39,271 outcome is recorded as −$450; gap-through-
   stop otherwise fills *at* the stop (optimistic loss tail).
6. **"No weekend hold" on D/W is fiction** (trades exit at Sunday reopen,
   gap included); signal/time/session exits fill at the signal bar's close
   and pay no exit slippage; live enforces no weekend flatten at all.
7. **Min-lot rounding breaks the risk clamp**; `max_concurrent_positions`
   accepted and never enforced; stat-arb pairs use a synthetic envelope,
   pay zero swap, and mix cross-quote units.
8. **Compounding:** the engine defaults `compounding=True` but **every
   persisted artifact was produced with `compounding=False`**; the additive
   greedy-assembly identity fails under compounding (up to 31.4% relative
   error; DD understated 25%).

**Consequence for V2 (Claude conclusion, INFERRED):** none of V1's backtest
results can be inherited as fidelity evidence. This corroborates the V2
BACKTEST_FIDELITY_SPEC direction (one deterministic lifecycle, bid/ask
fills, measured costs, no look-ahead, deterministic reproducibility) and
the D-034 simulation/certification requirement. → **REPLACE** the engine;
**RETAIN_CONCEPT** for the specific realism features V1 built correctly
(quote→USD conversion intent, per-bar historical spread, stop-exit
slippage, gap-through-stop handling, lot-rounding-with-risk-recompute) as a
*checklist of what a correct engine must do*, since V1 proved each is
load-bearing by getting it wrong.

## TradingView bridge findings (Area 8, critical focus)

**Direct — the v2 `.cs` source was read this session.**

- **Origin & rename:** `TradingViewBridge` is a cBot inherited from a
  TradingView-webhook era, now the order-submission program (HTTP JSON on
  `localhost:6000`, shared-token auth, actions buy/sell/closeall/partial/
  status/sizecheck/heartbeat). Per D-023 the V2 successor is renamed for
  its real responsibility (recommended: `CTraderExecutionBridge`).
- **Sizing lives in the bot**, not the app: `usableEquity = Equity −
  EquityDeduction(90000)`, `riskAmount = usableEquity × RiskPercentage/100`;
  the service can only audit the bot's *parameters*. This split is the
  root of the sizing-parity problem V2 must not inherit.
- **The "% weighting per symbol" mechanism (D-023 verification):** the exact
  phrase does not appear in V1. The feature Jacob means is the **per-strategy
  `riskMult`** — a per-member risk multiplier (DSR×inverse-vol, clipped
  [0.5,1.5]) that scales each strategy's size. Evidence: (a) V1 **disabled**
  it by default on 2026-07-27 (decision 4) because the layer was
  anti-correlated (−0.476) with the ranking statistic, rewarded near-
  inactive strategies (32 trades → 5.46× raw weight), and **breached its own
  1.5× cap to 1.978×**; (b) the shipped v2 bridge **ignores `riskMult`
  entirely** while the client sends it and the service logs weighted risk as
  authorised — "masked only by weighting being off, luck not design"; (c)
  the statgate v3 bridge re-adds it as a **fail-closed** field (absent/
  unparseable → refuse the trade; clamp only downward). **This corroborates
  D-023/EXEC-011: V2 must not carry per-symbol percentage weighting**; sizing
  derives solely from the approved book, the account risk-per-trade config,
  and the single authoritative engine. (A second, unrelated per-symbol
  mechanism exists in `PriceBridge` — a per-symbol wait/reject-list for bar
  serving — recorded here only to disambiguate.)
- **Live-safety defects open in the fetched v2 source (all Direct):**
  a rejected stop-loss leaves a full-size position naked while `TRADE OK` is
  logged (the `ModifyPosition` that installs the only loss limit is
  unchecked, `:502-513`); `tp="0"` passes the "every trade must have SL and
  TP" gate; a close can close nothing and report success (`:424-449`); HTTP
  200 "OK" is returned *before* the trade is attempted and regardless of
  outcome (`:234-245`) so every refusal books a phantom trade; the listener
  binds **all interfaces** (`http://*:{Port}/`, `:91`) — recorded as fixed
  and not fixed — and the Cloudflare tunnel routes a public hostname to that
  same order endpoint; the token is printed on every signal (`:225`); an
  order can execute after `OnStop`; `VolumeForFixedRisk` can round *up* past
  the risk budget; 40-char label truncation can let one strategy's exit
  flatten another's position.
- **Not compilable off-platform:** the `.cs` is built only by cTrader; every
  V1 "fix" was reviewed by reading + structural assertion — "a structural
  assertion is not a compilation and a compilation is not a run." The
  planned deploy was **HELD** on unanimous adversarial review; v1 remains
  installed and not running.

→ **V2 disposition: REPLACE** the bridge (a clean broker-neutral execution
adapter behind the V2 order contract, Round J), **RETAIN_CONCEPT** for the
fail-closed patterns V1 eventually reached (fail-closed auth, fail-closed
`riskMult`, loud zombie-listener handling, InvariantCulture parsing) and the
read-only `sizecheck` idea (a certification precursor — feeds D-034 Mode C).
**REMOVE** per-symbol weighting, the all-interfaces bind, token logging, and
the size-in-the-bot split.

---

## Prior V1 review claims vs verified repository evidence

Per Issue #21. Status ∈ {Confirmed, Partially confirmed, Contradicted,
Unable to verify}. The full 200+ claim inventory is retained in the audit
evidence set; the load-bearing ones:

| Claim (V1's own) | Verified status | Note |
|---|---|---|
| Backtest has no look-ahead; entries fill next-bar-open | **Contradicted** | Entry fill is clean, but position **sizing** has the trailed-stop look-ahead (Direct). |
| Locked calendar-aligned holdout, selection-untouched | **Contradicted** | Holdout cut is per-job wall-clock (7 cuts / 15 jobs), spent ~200×/run unledgered; "every OOS claim is selection-touched." |
| The 2008–2019 deep surface is pristine/untouched | **Contradicted** | A full seven-method generation ran from its start + ≥2 unledgered reads; "until the register lands, 'untouched' may not be written." |
| Robustness gate is honest and binding | **Partially confirmed** | The formulas were implemented; V1 later found each mis-applied and that **zero gates can refuse a book**. |
| ~31% durable CAGR / p=0.436 / Calmar 19.68 / +0.42 rank persistence | **Contradicted** | Each retired, corrected, or labelled untrusted by later measurement in the same corpus; re-scored reference book Calmar 0.81, DD 36.84%. |
| Canonical drawdown is peak-relative, one definition | **Partially confirmed** | Decided (D80) but not implemented; live code still carries base-relative + divergent computations. |
| $75 sizing parity verified end-to-end | **Contradicted** | No end-to-end lot comparison exists (zero `sizecheck` callers); under compounding "there is no $75." |
| cBot v2 blockers all fixed (deploy checklist) | **Contradicted** | ≥1 blocker not fixed in the file about to be installed; deploy HELD on unanimous HOLD. |
| Zero real fills / paper-only | **Confirmed** | `store.record_execution` has no callers; all 158 trade rows `dry_run`. |

**Profitability-evidence assessment (critical focus, Claude conclusion):**
V1's own most recent documents state plainly — *"It is not a platform that
has found an edge, and the measured evidence still says the most likely
honest outcome is that there is none in the space explored so far."* On
10,660 clean candidates (ex-contaminated crypto, honest sizing) the best
sits **below** a noise bar; gross expectancy before cost is **negative**
(mean R −0.0049). No out-of-sample, uncontaminated, cost-honest
profitability evidence exists; the one high-power validation arm
(2008–2019) was never run. **This is the direct answer to Q-010 and a
critical acceptance input — recorded, not decided.**

## Duplication, dead code, and hidden assumptions (Areas: additional checks)

- **Duplication/dead code:** `run_backtest.py` (demo path) vs the
  generator/pipeline; hand-mirrored live vs backtest strategy code (drift
  risk); ~16 overlapping data-pipeline modules; six control modules with
  zero production callers; `_d3c.py`/`_d3probe.py` scratch prototypes;
  statgate adds `statgate/bookgate/weighting/cost_identity` absent from
  `main`. → catalogued in V1_REUSE_REGISTER.
- **Hidden hard-coded assumptions:** fixed `account_size=100_000`,
  `starting_capital=10_000`, risk defaults (0.0075 / bot 0.75 /
  `equity_deduction=90000`); a 67-symbol universe + cost table; a 13-symbol
  exclusion register; approximate static `QUOTE_USD`; `weekend_close_hour=20`
  (open obligation, no gate); localhost endpoints; an absolute
  `C:\AutoFXData\...` path. → V2 must externalise all of these as versioned
  configuration/data, never code constants (corroborates DATA rules).

## Findings register (evidence + disposition)

The per-component REUSE/ADAPT/REJECT/UNKNOWN classifications, each with
evidence strength and V2-implication code, are in
[V1_REUSE_REGISTER.md](V1_REUSE_REGISTER.md). Disposition counts and the
Round B input list are in the execution report and the handoffs.

## What this audit did NOT do

No DB-side audit (deferred, D-022); no execution/rerun of any V1 code; no
optimisation or re-scoring (inspection only); no V2 design decisions closed;
no owner decisions made. All dispositions are `PROPOSED` recommendations for
their named later rounds.
