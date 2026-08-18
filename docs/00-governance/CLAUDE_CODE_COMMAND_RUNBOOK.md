# Claude Code Command Runbook

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (v0.1.0's catalogue was **REJECTED by Jacob
  2026-08-18** for factual errors — D-035; this corrected version's
  policies remain `PROPOSED` and return to Jacob for separate,
  one-at-a-time approval per D-025. Nothing here is `OWNER_APPROVED`.)
- **Version:** 0.2.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** MODEL_ROUTING_POLICY.md (D-012/D-017),
  TOOLING_REGISTER.md (D-013/D-015/D-024/D-033),
  `.claude/rules/20-session-continuity.md`, CLAUDE.md (no-build gate),
  DECISION_LOG.md (D-025, D-035)
- **Approval evidence:** None (correction pass 2026-08-18 per owner
  instruction; B-7 approval explicitly NOT granted)

## 1. Scope, environment, and evidence method

- **Claude Code version tested:** 2.1.234 (`claude --version`, VERIFIED
  2026-08-18, twice this session).
- **Environment:** Windows Server 2022 (NT 10.0.20348.0), terminal CLI
  (primary workspace, D-011); session model Fable 5 + Ultracode (D-012).
- **Research dates:** initial 2026-08-18; correction pass later the same
  day.
- **Official sources (sole authority for product behaviour), accessed
  2026-08-18:**
  - https://code.claude.com/docs/en/commands (full raw page retrieved —
    154,231 bytes; 105 command rows enumerated exhaustively)
  - https://code.claude.com/docs/en/sessions
  - https://code.claude.com/docs/en/scheduled-tasks

**Two-axis evidence model (per owner instruction).** Every command carries
two independent statuses:

1. **Official status:** `DOCUMENTED` · `DOCUMENTED_AS_REMOVED` ·
   `NOT_IN_OFFICIAL_CATALOGUE`.
2. **Local status on this machine:** `LOCALLY_VERIFIED_VISIBLE` (safely
   observed: invoked by Jacob this session, listed in this session's
   skill roster, or exercised as a session-start check) ·
   `LOCALLY_VERIFIED_UNAVAILABLE` (safe positive evidence of absence —
   none currently established) · `LOCALLY_NOT_VERIFIED`.

**Hard evidence rules:** absence from a binary-string scan is **never**
proof a command is unavailable (official docs themselves note `/heapdump`
"doesn't appear in the command menu; type it in full" — menu and string
evidence both mislead). Binary-string hits are recorded only as weak
corroboration. No command that edits, reloads, authenticates, opens
external services, changes permissions/settings, creates cloud activity,
triggers billing, delegates work, or produces sensitive output was
executed to test availability. Where local verification was not safely
possible, the entry says `LOCALLY_NOT_VERIFIED` and § 9 gives the harmless
manual check.

**Behaviour codes:** `RO` read-only · `LM` local mutation (session state,
local files, settings on this machine) · `RM` repository mutation ·
`EX` external/cloud action · `AU` authentication · `BC` billing/cost ·
`DG` delegation/background execution · `SD` sensitive diagnostic output.

**AutoFX policy labels:** `ROUTINE` · `BOUNDED` · `OWNER_APPROVAL` ·
`PROHIBITED_DISCOVERY` · and the overlay `PROHIBITED_PROD_TRADING`
(never usable as a production or trading scheduler/executor, in any
phase).

## 2. Command kinds

| Kind | Meaning |
|------|---------|
| BUILT_IN | Core CLI functionality; Claude cannot invoke built-ins itself (a scheduled fire passes them through as plain text) |
| BUNDLED_SKILL | Skill shipped with Claude Code, marked **[Skill]** in the official table; loads instructions/tools into the turn |
| WORKFLOW | Bundled dynamic workflow fanning out subagents in the background (`/deep-research`; `/batch` behaves this way via background subagents) |
| PLUGIN_COMMAND | Contributed by installed plugins (D-013-governed; `figma:*` is D-015 out-of-scope) |
| MCP_PROMPT | `/mcp__<server>__<prompt>` from connected MCP servers (all current connectors D-015 out-of-scope) |
| ALIAS | Alternative name for another command (policy of the target applies) |
| ENVIRONMENT_SPECIFIC | Only visible under specific env vars/platforms (e.g. `/setup-bedrock`) |

Recognition/queuing (official): commands recognised only at message start;
most queue while Claude responds; `/status`, `/tasks`, `/usage` run
immediately; dialog commands run immediately in fullscreen from v2.1.234;
`/effort` takes effect immediately.

## 3. Platform, plan, version, and environment dependence (official)

- Version-gated (all ≤ 2.1.234, so version-eligible here): `/autocompact`
  2.1.221+ · `/cd` 2.1.169+ · `/fork` background-copy semantics 2.1.212+
  (2.1.161–2.1.211: forked subagent) · `/subtask` 2.1.212+ (earlier this
  was `/fork`; unavailable when agent view is off) · `/import` 2.1.213+ ·
  `/list-agents` 2.1.224+ · `/fast` 2.1.205+ · `/deep-research`
  self-invocation removed 2.1.218 · `/verify`,`/run`,`/run-skill-generator`
  2.1.145+ · `/reload-skills` 2.1.152+ · `/usage-credits` URL-print
  fallback 2.1.205+.
- Plan/account-gated: `/privacy-settings` (Pro/Max) · `/upgrade`
  (non-Enterprise) · `/passes` (eligible accounts) · `/voice` (Claude.ai
  account) · `/ultrareview` (3 free runs on Pro/Max, then usage credits =
  billing) · `/team-onboarding` share links (paid plans).
- Platform/feature-gated: `/design-sync`, `/import`, `/insights`,
  `/radio`, `/chrome` (unavailable on Bedrock/GCP/Azure/AWS variants or
  with feature flags off) · `/desktop` (macOS/x64 Windows + subscription) ·
  `/autofix-pr` (web access + `gh`) · `/sandbox` (supported platforms
  only) · `/scroll-speed`, `/focus`, `/tui fullscreen` (fullscreen
  renderer) · `/terminal-setup` (specific terminals).
- Environment-specific: `/setup-bedrock` (`CLAUDE_CODE_USE_BEDROCK=1`) ·
  `/setup-vertex` (`CLAUDE_CODE_USE_VERTEX=1`) ·
  `CLAUDE_CODE_DISABLE_CRON=1` removes `/loop` + cron tools.

## 4. Aliases, renames, and removed commands (official)

- Aliases: `/cost`, `/stats` → `/usage` · `/review` → `/code-review` ·
  `/ultrareview` → `/code-review ultra` (kept as alias) · `/settings` →
  `/config` · `/reset`, `/new` → `/clear` · `/bg` → `/background` ·
  `/share` → `/bug` (2.1.212+) · `/quit` → `/exit` · `/checkup` →
  `/doctor` · `/allowed-tools` → `/permissions` · `/proactive` → `/loop` ·
  `/peers` → `/list-agents` · `/app` → `/desktop` · `/ios`, `/android` →
  `/mobile` · `/checkpoint`, `/undo` → `/rewind` · `/routines` →
  `/schedule`. Renamed: `/usage-credits` was previously `/extra-usage`.
- **DOCUMENTED_AS_REMOVED:** `/pr-comments` (removed v2.1.91 — ask Claude
  directly) · `/vim` (removed v2.1.92 — use `/config` → Editor mode) ·
  `/ultraplan` (removed — use plan mode; previously sent a planning task
  to a web session).

## 5. Command catalogue

Columns: Type · Official (`DOC`/`REMOVED`/`NOT_CAT`) · Local (`VER` =
LOCALLY_VERIFIED_VISIBLE with evidence in brackets; `NV` =
LOCALLY_NOT_VERIFIED) · Behaviour codes · Policy. Blanket rule for rows
marked NOT_RELEVANT: cosmetic/owner-personal; no AutoFX use during
recorded work; negligible tokens; no gate; no example needed.

### 5.1 Help and visibility

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/help` | BUILT_IN | DOC | NV | RO | Help + command list | ROUTINE |
| `/status` | BUILT_IN | DOC | VER (D-012 session-start check) | RO | Session status incl. model; immediate | ROUTINE |
| `/context` | BUILT_IN | DOC | NV | RO | Context usage grid | ROUTINE |
| `/tasks` | BUILT_IN | DOC | VER (invoked by Jacob this session) | RO | Background work list; immediate | ROUTINE |
| `/workflows` | BUILT_IN | DOC | NV | RO/LM (can pause/resume/save workflows) | Workflow progress view | BOUNDED (viewing routine; pausing/resuming runs = bounded) |
| `/list-agents` (`/peers`) | BUILT_IN | DOC | NV | RO | List messageable agents/sessions | ROUTINE |
| `/skills` | BUILT_IN | DOC | NV | RO/LM (Space toggles skill visibility, Enter saves) | List skills; token sort; visibility override | ROUTINE to list; changing visibility = BOUNDED |
| `/agents` | BUILT_IN | DOC | NV | RO | Subagent config info (v2.1.198+: pointer) | ROUTINE |
| `/release-notes` | BUILT_IN | DOC | NV | RO | Changelog viewer | ROUTINE |
| `/recap` | BUILT_IN | DOC | NV | RO | One-line session summary | ROUTINE |
| `/insights` | BUILT_IN | DOC | NV | LM (writes local HTML report) | Session-usage report (not in cloud sessions) | BOUNDED (report reveals session content — keep local, never commit) |
| `/stats` | ALIAS→`/usage` | DOC | NV | RO | Usage, Stats tab | ROUTINE |

### 5.2 Models, reasoning, and usage

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/model` | BUILT_IN | DOC | NV | LM (saves default) | Switch model | View = BOUNDED; switching main session off `best` = OWNER_APPROVAL (D-012) |
| `/effort` | BUILT_IN | DOC | VER (session-start check) | LM | Set effort (`max`/`ultracode` session-only; immediate) | Verify = ROUTINE; lowering below Ultracode for critical work = OWNER_APPROVAL |
| `/fast` | BUILT_IN | DOC | NV | LM | Toggle fast mode | BOUNDED — **never for critical AutoFX work** (owner rule; D-012 requires Fable for critical judgment) |
| `/advisor` | BUILT_IN | DOC | NV | LM/BC (second-model consultation costs tokens) | Advisor model on/off (`fable`/`opus`/`sonnet`/ID) | BOUNDED — token cost stated; never substitutes for governor-routed independent review |
| `/usage` (`/cost`) | BUILT_IN | DOC | NV | RO | Usage/costs; immediate | ROUTINE |
| `/usage-credits` | BUILT_IN | DOC | NV | **EX/BC** — opens billing settings in browser, or sends a usage-credit request to an admin (after a confirm dialog); prints URL over SSH (2.1.205+). Previously `/extra-usage` | Configure/request usage credits | **OWNER_APPROVAL** — a billing/spend action under D-019, NOT a read-only counterpart of `/usage` |

### 5.3 Context, compaction, and session continuity

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/compact [instructions]` | BUILT_IN | DOC | NV | LM (lossy history replacement) | Summarise conversation | BOUNDED — AutoFX continuity protocol first (§ 7) |
| `/autocompact` | BUILT_IN | DOC | NV | LM | Auto-compact threshold | BOUNDED |
| `/clear` (`/reset`,`/new`) | BUILT_IN | DOC | NV | LM (old conversation saved + resumable; new context empty) | Fresh conversation | BOUNDED — **pushed repository handoff first** (hard precondition) |
| `/resume [name]` | BUILT_IN | DOC | NV | LM | Switch to saved conversation | BOUNDED — re-verify repo truth after resume |
| `/rename` / `claude -n` | BUILT_IN | DOC | NV | LM | Name session (resume handle) | ROUTINE |
| `/branch [name]` | BUILT_IN | DOC | NV | LM | Copy conversation, switch into copy | BOUNDED — record branch IDs in SESSION_LOG |
| `/rewind` (`/checkpoint`,`/undo`) | BUILT_IN | DOC | NV | **LM/RM** (rolls conversation and/or code back) | Checkpoint rewind / summarize-from | **OWNER_APPROVAL — must never silently discard approved or uncommitted work**: commit/stash first, Jacob picks the checkpoint, event recorded in SESSION_LOG |
| `/export [file]` | BUILT_IN | DOC | NV | LM (writes transcript file) | Export conversation text | BOUNDED — local only, never committed, never to synced/public paths |
| `/cd` | BUILT_IN | DOC | NV | LM (relocates session storage) | Move session directory | BOUNDED — stay in `C:\AutoFXV2.0` |
| `/add-dir` | BUILT_IN | DOC | NV | LM (widens file access; not restored on resume) | Add working directory | OWNER_APPROVAL (access-scope change, e.g. any V1 path) |
| `claude --continue/--resume/--fork-session/--from-pr` | CLI | DOC | VER (used across sessions) | LM | Resume/branch from shell | BOUNDED per RESUME_PROMPT.md |

### 5.4 Planning and side questions

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/plan [desc]` | BUILT_IN | DOC | NV | LM (mode change; never restored on resume) | Enter plan mode | BOUNDED — material plan content must land in repo docs |
| `/btw [question]` | BUILT_IN | DOC | NV | RO (answer OUTSIDE conversation history; no-arg browses previous side Q&A, 2.1.212+) | Side question | BOUNDED — **never for decisions, requirements, or approvals** (bypasses the record) |

### 5.5 Code, diff, and security review

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/diff` | BUILT_IN | DOC | NV | RO | Interactive diff viewer | ROUTINE |
| `/code-review` (`/review`) | BUNDLED_SKILL (official **[Skill]**) | DOC | VER (roster) | RO plain; `--fix` RM; `--comment`/`--post` EX; `ultra` EX/BC (cloud sandbox; credits after free runs) | Diff/PR review | Plain = BOUNDED; `--fix`/`--comment` = OWNER_APPROVAL; `ultra` = OWNER_APPROVAL (cloud + billing, P-0.3) |
| `/ultrareview` | ALIAS→`/code-review ultra` | DOC | NV | EX/BC | Deep cloud review | OWNER_APPROVAL (explicitly out of scope this task class) |
| `/security-review` | BUILT_IN per official table (session roster surfaces it as a skill — discrepancy recorded, official classification adopted) | DOC | VER (roster) | RO (needs `origin` remote; reviews branch vs origin default) | Security review of branch changes | BOUNDED |
| `/simplify [target]` | BUNDLED_SKILL (official **[Skill]**) | DOC | VER (roster) | **RM** — runs four parallel review subagents (reuse, simplification, efficiency, abstraction) and **applies the fixes**; no bug-hunting from v2.1.154 | Cleanup review + auto-apply | OWNER_APPROVAL during discovery (edits files; also DG — parallel subagents route via governor) |
| `/verify` | BUNDLED_SKILL (official **[Skill]**, 2.1.145+; self-invocation removed 2.1.215) | DOC | NV (not in this session's roster) | LM/EX (builds + runs the app) | Verify change by running app | PROHIBITED_DISCOVERY (nothing to run); post-authorisation BOUNDED |
| `/run` | BUNDLED_SKILL (official **[Skill]**, 2.1.145+) | DOC | VER (roster) | LM/EX (launches app) | Launch/drive project app | PROHIBITED_DISCOVERY; post-authorisation BOUNDED in approved phase |
| `/run-skill-generator` | BUNDLED_SKILL (official **[Skill]**, 2.1.145+) | DOC | NV | **RM** (writes a per-project skill file) | Teach `/run`+`/verify` the project | PROHIBITED_DISCOVERY (writes project config for an app that must not exist yet) |

### 5.6 Autonomous goals and monitoring

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/goal [condition\|clear]` | BUILT_IN | DOC | NV | LM/DG (multi-turn autonomy; survives resume with counters reset; no-arg shows current; `clear`/`stop`/`off`/`reset`/`none`/`cancel` ends) | Work-until-condition | OWNER_APPROVAL — goal text must carry scope, completion condition, stopping conditions (incl. the twelve D-019 stops), approval boundaries |
| `/loop [interval] [prompt]` (`/proactive`) | BUNDLED_SKILL (official **[Skill]**) | DOC | VER (roster) | LM/DG. **Persistence (corrected):** scheduled tasks are session/conversation-scoped; unexpired recurring tasks (≤7 days) and unfired one-shots are restored when THAT session is resumed; a fresh conversation clears them; fires only while the session runs; missed fires don't catch up; jitter applies. `.claude/loop.md` is ONLY the optional project-level default loop prompt — it is never storage for scheduled-task state | Repeat a prompt on schedule | OWNER_APPROVAL during discovery; **PROHIBITED_PROD_TRADING — never a production or trading scheduler** |
| `/schedule [description]` (`/routines`) | BUILT_IN command driving cloud Routines (a same-named local skill also appears in this session's roster) | DOC | VER (roster) | **EX/DG** (cloud execution, Anthropic-managed, no local files, no permission prompts; prompts `/web-setup` if GitHub unconnected → AU) | Cloud routines | OWNER_APPROVAL; **PROHIBITED_PROD_TRADING** |
| Natural-language one-shot reminders (CronCreate/CronList/CronDelete) | Tools | DOC | VER (tools present) | LM | In-session reminders; ≤50 tasks; local timezone | BOUNDED |
| Monitor tool | Tool | DOC | VER (tool present) | LM/DG (not restored on resume) | Stream background script output | BOUNDED |

### 5.7 Agents, parallelism, and workflows

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/subtask <task>` | BUILT_IN (2.1.212+; was `/fork` on 2.1.161–211; unavailable with agent view off) | DOC | NV | DG (forked subagent inherits full conversation; result returns here) | Side task to subagent | BOUNDED — governor routing first (D-017); read-only agents during discovery |
| `/fork [prompt]` | BUILT_IN (2.1.212+; earlier/agent-view-off = forked subagent) | DOC | NV | DG/LM (copy runs as background session; makes its own worktree for code edits, 2.1.221+) | Copy conversation to background session | BOUNDED — record fork in SESSION_LOG; never two forks writing the same registers |
| `/background [prompt]` (`/bg`) | BUILT_IN | DOC | NV | DG (detaches session as background agent) | Unattended continuation | OWNER_APPROVAL (same conditions as `/goal`) |
| `/stop` | BUILT_IN | DOC | NV | LM (stops a background session; transcript kept) | Stop background session | BOUNDED |
| `/batch <instruction>` | BUNDLED_SKILL (official **[Skill]**) | DOC | NV | **RM/DG/EX** — decomposes into 5–30 units, one background subagent per unit in isolated worktrees, each runs tests and **opens a pull request** | Mass parallel change | PROHIBITED_DISCOVERY; post-authorisation OWNER_APPROVAL per use with token/cost statement + governor routing |
| `/deep-research <question>` | WORKFLOW (official) | DOC | NV | EX/DG (web fan-out, cited report; invoke-only since 2.1.218) | Multi-agent research | BOUNDED — governor routing + approved research brief + token budget stated; output = dated repo brief |

### 5.8 Permissions and sandboxing

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/permissions` (`/allowed-tools`) | BUILT_IN | DOC | NV | RO view; **LM/RM** on change (settings files) | Allow/ask/deny rules | View = ROUTINE; any durable change = OWNER_APPROVAL |
| `/fewer-permission-prompts` | BUNDLED_SKILL (official **[Skill]**) | DOC | VER (roster) | **RM** (writes project settings allowlist) | Reduce prompts | OWNER_APPROVAL (NEXT_ACTIONS § B settings item) |
| `/sandbox` | BUILT_IN | DOC | NV (supported platforms only; Windows support unknown — § 9 check) | LM (execution-isolation posture) | Toggle sandbox mode | BOUNDED — changing isolation posture is a session-discipline event; record in SESSION_LOG |
| `/import` | BUILT_IN (2.1.213+; platform-gated) | DOC | NV | LM/RM (foreign agent config in) | Import Codex/Gemini config | PROHIBITED_DISCOVERY |

### 5.9 Plugins, skills, hooks, and MCP

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/plugin` | BUILT_IN | DOC | NV | RO list; LM/RM/EX on install/enable/disable | Manage plugins | List = ROUTINE; install/enable/disable = OWNER_APPROVAL (D-013) |
| `/reload-plugins` | BUILT_IN | DOC | NV | LM | Reload active plugins | BOUNDED (after an approved plugin change) |
| `/reload-skills` | BUILT_IN — **DOCUMENTED (added v2.1.152)**: re-scans skill/command directories so skills added/changed on disk become available without restart; reports counts | DOC | NV (binary string absent — weak; § 9 check) | LM (session skill roster) | Refresh skills mid-session | BOUNDED — after approved skill-file changes only (e.g. governor-skill updates); v0.1.0's "NOT_AVAILABLE" claim was WRONG (errata E-1) |
| `/mcp` | BUILT_IN | DOC | NV | RO status; **AU/EX** on enable/reconnect/auth | MCP servers | Status = ROUTINE; enable/connect/auth = PROHIBITED_DISCOVERY for D-015 connectors, otherwise OWNER_APPROVAL |
| `/hooks` | BUILT_IN | DOC | NV | RO view | Hook configs | ROUTINE (view); hook changes = OWNER_APPROVAL |
| `/memory` | BUILT_IN | DOC | NV | **RM** (edits CLAUDE.md; auto-memory toggles) | Memory management | View = ROUTINE; CLAUDE.md edit = OWNER_APPROVAL (authority-hierarchy doc) |
| MCP prompts `/mcp__*__*` | MCP_PROMPT | DOC (mechanism) | NV | varies | Server prompts | PROHIBITED_DISCOVERY (D-015) |
| Plugin commands (`product-management:*`, `claude-md-management:*`, `session-report`) | PLUGIN_COMMAND | n/a (plugin-defined) | VER (roster; D-013-installed) | varies (`claude-md-management` edits CLAUDE.md → OWNER_APPROVAL) | Per plugin | BOUNDED within D-013 purpose |
| `figma:*` | PLUGIN_COMMAND | n/a | VER (visible) | EX | Design tooling | PROHIBITED_DISCOVERY (D-015; wireframe phase only) |

### 5.10 GitHub, remote, and cloud integration

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/install-github-app` | BUILT_IN | DOC | NV | EX/AU/P (repo app + optional Actions workflows) | GitHub App install | OWNER_APPROVAL (Actions = deploy-adjacent; gate lists deploying workflows) |
| `/install-slack-app` | BUILT_IN | DOC | NV | EX/AU | Slack app OAuth | NOT_RELEVANT / OWNER_APPROVAL |
| `/web-setup` | BUILT_IN — **DOCUMENTED**: connects your GitHub account to Claude Code on the web **using local `gh` CLI credentials**; `/schedule` triggers it automatically when GitHub isn't connected | DOC | NV | **AU/EX** | Web/cloud GitHub connection | OWNER_APPROVAL — authentication + cloud exposure of repo access (P-0.3); note the `/schedule` auto-prompt path when weighing any `/schedule` approval |
| `/remote-control` | BUILT_IN | DOC | VER (invoked by Jacob this session) | LM/EX (device pairing) | Continue local session from another device | BOUNDED — owner-operated; Claude never initiates |
| `/remote-env` | BUILT_IN | DOC | NV | LM/EX (default cloud-agent environment) | Cloud-agent env selection | OWNER_APPROVAL (only meaningful with cloud execution, itself owner-gated) |
| `/teleport` | BUILT_IN | DOC | NV | LM/EX (imports web session) | Pull web session into terminal | OWNER_APPROVAL |
| `/autofix-pr [prompt]` | BUILT_IN | DOC | NV | **EX/RM/DG** (cloud session watches PR, pushes fixes) | Autonomous cloud PR fixing | PROHIBITED_DISCOVERY (autonomous external pushes) |
| `/desktop` (`/app`) | BUILT_IN | DOC | NV (platform/plan-gated) | LM | Continue in Desktop app | BOUNDED (Desktop = visual review, D-011) |
| `/setup-bedrock`, `/setup-vertex` | ENVIRONMENT_SPECIFIC | DOC | NV (env vars unset) | AU/LM | Provider auth wizards | NOT_RELEVANT (not this deployment); any use = OWNER_APPROVAL |
| `/team-onboarding` | BUILT_IN | DOC | NV | LM/EX (analyses 30-day usage; paid plans get a share link) | Onboarding guide from usage history | OWNER_APPROVAL (distils session history; share link publishes it) |

### 5.11 Debugging and diagnostics

| Command | Type | Official | Local | Behaviour | Purpose | Policy |
|---|---|---|---|---|---|---|
| `/doctor` (`/checkup`) | BUNDLED_SKILL (official **[Skill]**) | DOC | NV | RO diagnose; **RM/P on accepted fixes** (dedupes/trims CLAUDE.md, migrates guidance to skills, offers auto-mode default + pre-approvals — asks confirmation first) | Setup checkup | Diagnose = BOUNDED; accepting ANY offered change (CLAUDE.md trim, auto-mode, pre-approvals) = OWNER_APPROVAL |
| `/debug [description]` | BUNDLED_SKILL (official **[Skill]**) | DOC | NV | LM/SD (session debug logging from that point) | Runtime troubleshooting | BOUNDED — logs never committed |
| `/heapdump` | BUILT_IN — official: writes heap snapshot + memory breakdown to `~/Desktop` (or home); **“the `.heapsnapshot` contains your full conversation and credentials, so don't share it”**; only the `-diagnostics.json` may be attached to reports; doesn't appear in the command menu (type in full) | DOC | NV (menu absence is by design — string evidence meaningless here) | **LM/SD — highly sensitive** | Memory diagnosis | OWNER_APPROVAL; if ever used: file stays outside the repository, never committed/shared, deleted after diagnosis, event recorded in SESSION_LOG |
| `/bug` (`/share`) | BUILT_IN | DOC | NV | EX/SD (shares conversation with consent) | Bug report | OWNER_APPROVAL (content leaves machine) |
| `/feedback` | BUILT_IN | DOC | NV | EX/SD (session context attached) | Product feedback | OWNER_APPROVAL |
| `claude doctor`, `claude --version` | CLI | DOC | VER (`--version` run twice today) | RO | Shell diagnostics | ROUTINE |

### 5.12 UI and convenience

| Command | Type | Official | Local | Policy |
|---|---|---|---|---|
| `/theme`, `/color`, `/focus`, `/keybindings`, `/copy`, `/mobile` (`/ios`,`/android`), `/radio`, `/powerup`, `/passes`, `/upgrade`, `/chrome`, `/ide`, `/scroll-speed`, `/stickers`, `/tui`, `/terminal-setup`, `/statusline`, `/voice` | BUILT_IN | DOC | NV | NOT_RELEVANT (cosmetic/owner-personal; `/statusline` writes settings → OWNER_APPROVAL if durable; `/voice` needs Claude.ai account) |
| `/exit` (`/quit`) | BUILT_IN | DOC | NV | BOUNDED — checkpoint before exiting; background sessions keep running |
| `/login`, `/logout` | BUILT_IN | DOC | NV | AU — owner-operated identity only |
| `/config` (`/settings`) | BUILT_IN | DOC | NV | View = ROUTINE; changes = OWNER_APPROVAL |
| `/privacy-settings` | BUILT_IN | DOC (Pro/Max) | NV | Owner-operated |
| `/init` | BUILT_IN per official table (locally surfaced via skill roster — discrepancy recorded, official classification adopted) | DOC | VER (roster) | PROHIBITED_DISCOVERY — CLAUDE.md exists and is owner-governed; regeneration would overwrite the constitution |
| Project/bundled convenience skills (`update-config`, `keybindings-help`, `session-report`, `claude-api`, `dataviz`, artifact skills, `design`) | BUNDLED_SKILL/PLUGIN | n/a (skill docs) | VER (roster) | BOUNDED; `update-config` writes settings → OWNER_APPROVAL |

### 5.13 Removed or deprecated

| Command | Status | Replacement |
|---|---|---|
| `/pr-comments` | DOCUMENTED_AS_REMOVED (v2.1.91) | Ask Claude directly |
| `/vim` | DOCUMENTED_AS_REMOVED (v2.1.92) | `/config` → Editor mode |
| `/ultraplan` | DOCUMENTED_AS_REMOVED | Plan mode (`/plan`) |
| `/extra-usage` | Renamed | `/usage-credits` |
| `/agents` interactive builder | Superseded v2.1.198 | Ask Claude |

## 6. Session-continuity facts AutoFX policies rely on (official)

- `/clear` saves the old conversation (resumable) but empties context —
  repository handoffs are the only reliable state carrier.
- Resume restores: history, model (with exceptions), agent, permission
  mode (plan/bypass never restored), active `/goal` (counters reset),
  **unexpired scheduled tasks of that session**. Not restored: background
  Bash/Monitor tasks, `/add-dir` additions, `--mcp-config`-style flags.
- Resume-from-summary (Pro/Max, >100k tokens, >1h idle) compacts — detail
  loss; "as-is" preserves everything at higher per-request cost.
- `/loop` corrections (errata E-9): tasks are session/conversation-scoped
  and return on resume of that session if unexpired (7-day recurring
  expiry; unfired one-shots); a fresh conversation clears them; fires only
  while the session runs and is idle; no catch-up for missed fires; jitter
  shifts fire times; `Esc` stops a waiting loop; `/loop`-first sessions
  are hidden from the session picker; `.claude/loop.md` is only the
  optional default prompt (project or user level), never task-state
  storage.
- Transcripts: `~/.claude/projects/<project>/<session-id>.jsonl`, default
  30-day retention — not a durable archive; the repository is the record.

## 7. AutoFX policy proposals (`PROPOSED` — return to Jacob one at a time per D-025)

Standing rules P-0.1 … P-0.5 (unchanged from v0.1.0, restated):

- **P-0.1** No command may bypass the no-build gate, D-015 boundary,
  D-017/MODEL_ROUTING_POLICY routing, or D-024/D-033 git controls. Any
  command whose behaviour codes include RM, EX, AU, BC, or P is never
  treated as routine read-only.
- **P-0.2** Mutating variants are gated separately from read variants.
- **P-0.3** Anything sending conversation/repository content or
  credentials-backed access off this machine (`/bug`, `/feedback`,
  `/web-setup`, `/schedule`, `ultra`/`/ultrareview`, `/teleport`,
  `/autofix-pr`, `/team-onboarding` share links) needs Jacob's per-use
  approval.
- **P-0.4** Delegation-creating commands (`/subtask`, `/fork`,
  `/background`, `/batch`, `/deep-research`, `/simplify`'s parallel
  reviewers) route through the `autofx-model-governor` with token/cost
  consideration stated first.
- **P-0.5** Re-run § 9 revalidation after every Claude Code upgrade.

Per-command policies: as classified in § 5, with these owner-mandated
safeguards restated verbatim in intent:

- `/btw` never carries decisions or requirements (it does not join
  conversation history).
- `/clear` requires a completed **and pushed** repository handoff first.
- `/compact` follows the AutoFX continuity protocol (atomic task finished,
  handoffs/registers refreshed, committed; compaction instructions name
  what must survive).
- `/fast` is never used for critical AutoFX work.
- `/loop`, `/schedule`, Claude routines, and Claude sessions are **never
  production or trading schedulers** — production scheduling is V2
  application architecture (Rounds J/N).
- `/goal` requires explicit scope, completion condition, stopping
  conditions, and approval boundaries in the goal text.
- `/batch`, `/deep-research`, and parallel-agent commands require
  token/cost consideration and model-governor routing.
- `/rewind` never silently discards approved or uncommitted work.
- `/heapdump` output is highly sensitive (officially contains the full
  conversation and credentials) — never committed, never shared, deleted
  after use.
- `/usage-credits` is a billing action, never conflated with read-only
  `/usage`.

## 8. Recommended command sequences (`PROPOSED`, unchanged from v0.1.0 §8 in substance)

1. **Session start:** `claude --model best --effort ultracode` → `/status`
   → `/effort` → handoffs per RESUME_PROMPT.md → git verify → restate
   phase/gate → `/usage` if capacity matters → clear stale `/goal`.
2. **Critical task start:** `/status` + `/effort` → governor
   classification + route → `/context` headroom → Fable.
3. **Monitoring:** `/context` at breakpoints; `/usage` before long work;
   act at 60–70% / 75–80% thresholds.
4. **Pre-compaction:** finish atomic task → registers + handoffs → commit
   (+push) → `/compact <survival instructions>` → `/context` → re-read
   CURRENT_STATE.md.
5. **Usage exhaustion:** stop new work → full checkpoint → `/usage`,
   record displayed reset time exactly → `/rename` → stop.
6. **Resume:** `claude --resume <name>` → prefer as-is for critical
   sessions → `/status` + `/effort` → git verify → handoffs → continue
   from NEXT_ACTIONS.
7. **Documentation review:** `/diff` → secret scan → consistency checks →
   optional `/security-review` → commit → push per D-024.
8. **Implementation review (post-authorisation):** `/diff` →
   `/code-review` plain → governed Fable review for critical code → tests
   → `/security-review` → commit → push to approved phase branch.
9. **Bounded autonomous work:** owner scope approval → governor + token
   statement → prefer `/subtask` → `/tasks` monitoring → outcomes to
   registers.
10. **Diagnostics:** `claude --version` → `/status` → `/debug` →
    `/doctor` (decline write offers) → `/release-notes` → `/heapdump`
    only with Jacob per its safeguard → SESSION_LOG.

## 9. Safe local verification and post-upgrade revalidation

**Harmless manual checks for LOCALLY_NOT_VERIFIED commands** (Jacob or a
supervised session can run these; none mutate anything): type the command
name into the CLI prompt WITHOUT pressing Enter and observe whether the
command menu offers it (works for menu-listed commands; NOT for
`/heapdump`, which by design never appears); or run `/help` and read the
list; or for dialog-openers (`/theme`, `/config`) open and immediately
`Esc`. Commands with behaviour codes RM/EX/AU/BC/DG are never availability-
tested by execution.

**Revalidation after every Claude Code upgrade:**

1. `claude --version` → update header + TOOLING_REGISTER.
2. Re-retrieve the raw official commands page (the `.md` endpoint used
   2026-08-18 returned the full 105-row table; extraction summaries are
   NOT sufficient — v0.1.0's errors came from truncated extractions) and
   diff the command inventory.
3. Re-check the session skill roster against § 5 BUNDLED_SKILL rows.
4. Re-check `/resume`, `/compact`, `/rewind`, `/loop` semantics on the
   sessions and scheduled-tasks pages.
5. Update entries; mark disappearances DOCUMENTED_AS_REMOVED or
   NOT_IN_OFFICIAL_CATALOGUE; never delete history.
6. Re-verify D-012 launch checks and D-017 agent validation.
7. Record the revalidation in SESSION_LOG + TOOLING_REGISTER.
8. Any behaviour change touching a policy here goes to Jacob before the
   changed command is used.

## 10. Errata — v0.1.0 → v0.2.0 (correction pass 2026-08-18, D-035)

| # | Previous statement (v0.1.0) | Corrected statement (v0.2.0) | Evidence | Policy impact | Files updated |
|---|---|---|---|---|---|
| E-1 | `/reload-skills` "NOT_AVAILABLE — absent from the official catalogue and binary" | DOCUMENTED built-in, added v2.1.152: re-scans skill/command directories mid-session; LOCALLY_NOT_VERIFIED | Official commands page row (raw page, line 119) | New BOUNDED policy (was: do-not-attempt) | This runbook; TOOLING_REGISTER; SESSION_LOG |
| E-2 | `/web-setup` "not in official commands table — purpose INFERRED" | DOCUMENTED: connects GitHub to Claude Code on the web using local `gh` credentials; `/schedule` auto-prompts it | Official row (line 156) | OWNER_APPROVAL confirmed; AU behaviour added; `/schedule` interaction flagged | Same |
| E-3 | `/usage-credits` "SAFE_ROUTINE … view usage credits" (read-only) | DOCUMENTED billing action: opens billing settings or sends an admin usage-credit request; previously `/extra-usage`; NOT equivalent to `/usage` | Official row (line 152) | **Reclassified SAFE_ROUTINE → OWNER_APPROVAL (EX/BC)** | Same |
| E-4 | `/sandbox`, `/run-skill-generator`, `/remote-env`, `/stats`, `/stop`, `/team-onboarding`, `/ultrareview`, `/voice`, `/scroll-speed`, `/setup-bedrock`, `/setup-vertex`, `/tui`, `/stickers`, `/terminal-setup`, `/statusline` omitted | All catalogued with official rows; `/run-skill-generator` = skill that WRITES a project skill file (PROHIBITED_DISCOVERY); `/team-onboarding` distils usage history (OWNER_APPROVAL) | Official rows (full 105-row enumeration) | New entries + policies | Same |
| E-5 | `/workflows` "not in official commands table" | DOCUMENTED: workflow progress view (watch/pause/resume/save) | Official row (line 157) | Pause/resume noted as state-affecting → BOUNDED | Same |
| E-6 | Removed list = `/pr-comments` only | Also `/vim` (removed v2.1.92 → `/config` Editor mode) and `/ultraplan` (removed → plan mode); `/extra-usage` renamed | Official rows (lines 154, 148) | Removed-history completed | Same |
| E-7 | `/security-review` typed as bundled skill; `/init` typed as bundled skill | Official table types both as BUILT_IN (no [Skill] marker); local roster surfaces both via skills — discrepancy recorded, official classification adopted | Official rows (lines 131, 95) vs session roster | None (policies unchanged) | Same |
| E-8 | `/simplify` "(docs list built-in)" | Official **[Skill]**: four parallel review subagents (reuse/simplification/efficiency/abstraction), applies fixes, no bug-hunting from v2.1.154 | Official row (line 134) | DG behaviour added → P-0.4 routing also applies | Same |
| E-9 | `/loop` persistence: "cron state in project `.claude`" implied project-level persistence | Corrected: tasks are session/conversation-scoped; unexpired tasks restored on resume of that session; fresh conversation clears them; `.claude/loop.md` is only the optional default-prompt file, never task-state storage | Official scheduled-tasks page + commands row (line 103) | Wording only; prohibition on production/trading scheduling unchanged | Same |
| E-10 | Single four-value availability label conflating official and local evidence; binary ABSENT treated as availability signal (led to E-1) | Two independent axes: official status and local status; binary-string absence never proves unavailability (`/heapdump` proves menus/strings mislead by design) | Owner instruction + official `/heapdump` row (line 90) | Evidence-honesty structural fix across every entry | Same |
| E-11 | `/goal` syntax "`[condition\|clear]`" only | Official: no-arg shows current/most recent goal; `clear`/`stop`/`off`/`reset`/`none`/`cancel` all end it | Official row (line 89) | None | Same |
| E-12 | `/subtask`/`/fork` version interplay unstated | `/subtask` requires 2.1.212+ (earlier: `/fork`); unavailable when agent view off; `/fork` copy isolates edits in own worktree from 2.1.221 | Official rows (lines 141, 88) | None | Same |
| E-13 | `/heapdump` sensitivity stated as inference ("may embed…") | Official wording: the `.heapsnapshot` "contains your full conversation and credentials, so don't share it"; only `-diagnostics.json` attachable; hidden from menu by design | Official row (line 90) | Sensitivity now evidence-backed; safeguard unchanged | Same |

Every other § 5 entry was re-verified against the raw official page's
105-row enumeration during this pass, not only the examples above.
