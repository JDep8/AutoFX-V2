# Claude Code Command Runbook

- **Owner:** Jacob Depares
- **Status:** `PROPOSED` (catalogue evidence VERIFIED/DOCUMENTED as labelled
  per entry; every AutoFX policy in § 7–8 is `PROPOSED` and awaits Jacob's
  approval — nothing here is `OWNER_APPROVED`)
- **Version:** 0.1.0
- **Last reviewed:** 2026-08-18
- **Dependencies:** MODEL_ROUTING_POLICY.md (D-012/D-017),
  TOOLING_REGISTER.md (D-013/D-015/D-024),
  `.claude/rules/20-session-continuity.md`, CLAUDE.md (no-build gate)
- **Approval evidence:** None yet (owner-directed research task 2026-08-18;
  policies presented for approval, not approved)

## 1. Scope, environment, and method

- **Claude Code version tested:** 2.1.234 (`claude --version`, VERIFIED
  2026-08-18).
- **Environment:** Windows Server 2022 (NT 10.0.20348.0), terminal CLI
  (primary workspace per D-011); session model Fable 5 + Ultracode (D-012).
- **Research date:** 2026-08-18.
- **Official sources (product behaviour is taken ONLY from these):**
  - https://code.claude.com/docs/en/commands
  - https://code.claude.com/docs/en/sessions
  - https://code.claude.com/docs/en/scheduled-tasks
- **Local verification method (read-only; no command exercised):**
  1. `claude --version` output.
  2. Read-only string inspection of the installed binary
     (`C:\Users\Administrator\.local\bin\claude.exe`) for slash-command
     tokens — the same method used for the D-017 package validation.
  3. In-session observation: commands actually invoked by Jacob this
     session (`/remote-control`, `/tasks`), and the session's bundled-skill
     roster (skills are loose files, not binary strings, so the roster is
     the correct evidence for skill-backed commands).
- **Method caveats (evidence honesty):** a token FOUND in the binary is
  strong evidence of presence; a token ABSENT is **weak** evidence
  (minification can hide strings). Therefore: ABSENT + documented →
  `DOCUMENTED_NOT_LOCALLY_VERIFIED`, never `NOT_AVAILABLE` on string
  absence alone. `NOT_AVAILABLE` is used only when a command is absent
  from both the official catalogue and the binary. No potentially mutating
  command was executed during this research.

**Availability labels:** `VERIFIED_ON_V2_1_234` ·
`DOCUMENTED_NOT_LOCALLY_VERIFIED` · `NOT_AVAILABLE` · `REMOVED`.
**Type labels:** `BUILT_IN` · `BUNDLED_SKILL` · `WORKFLOW` ·
`PLUGIN_COMMAND` · `MCP_PROMPT` · `REMOVED_OR_UNAVAILABLE`.
**AutoFX classifications:** `SAFE_ROUTINE` · `BOUNDED_USE` ·
`OWNER_APPROVAL_REQUIRED` · `PROHIBITED_DURING_DISCOVERY` · `NOT_RELEVANT`.

## 2. Command kinds — how they differ

| Kind | What it is | Trust/behaviour notes |
|------|------------|----------------------|
| **BUILT_IN** | Core CLI functionality compiled into Claude Code (e.g. `/model`, `/permissions`, `/compact`) | Executes harness logic directly; Claude cannot invoke built-ins on its own — a scheduled/loop fire passes them through as plain text |
| **BUNDLED_SKILL** | A prompt/skill shipped with Claude Code (e.g. `/code-review`, `/loop`, `/doctor`) | Loads instructions into the turn; since v2.1.215 skills run only on explicit invocation unless model-invocable; may drive tools |
| **WORKFLOW** | Skill that launches a multi-subagent background workflow (`/deep-research`, `/batch`) | Fans out many agents; large token cost; governed by MODEL_ROUTING_POLICY ("no dynamic workflow may bypass routing") |
| **PLUGIN_COMMAND** | Commands/skills contributed by installed plugins (here: `product-management:*`, `claude-md-management:*`, `session-report`, and environment-visible `figma:*`) | Availability follows D-013 install gates; figma:* is D-015 OUT-OF-SCOPE |
| **MCP_PROMPT** | `/mcp__<server>__<prompt>` exposed by connected MCP servers | All claude.ai connectors here are D-015 OUT-OF-SCOPE / NOT AUTHORISED |
| **Custom skills** | Project-defined skills (`autofx-model-governor`) | Project-scoped; governed by their own definitions |

Recognition/queuing (official): commands are recognised only at message
start; while Claude is responding most commands queue until the turn ends;
`/status`, `/tasks`, `/usage` run immediately; dialog commands run
immediately in fullscreen rendering from v2.1.234.

## 3. Platform, plan, and version dependence (from official docs)

| Dependency | Commands |
|------------|----------|
| Version-gated | `/autocompact` (v2.1.221+), `/cd` (v2.1.169+), `/fork` as background copy (v2.1.212+), `/import` (v2.1.213+), `/list-agents` (v2.1.224+), `/fast` (v2.1.205+), `/deep-research` (v2.1.218+) — all ≤ 2.1.234, so version-eligible here |
| Plan/account-gated | `/privacy-settings` (Pro/Max), `/upgrade` (non-Enterprise), `/passes` (eligible accounts), resume-from-summary dialog (Pro/Max) |
| Platform-gated | `/design-sync`, `/import`, `/insights`, `/radio`, `/chrome` (not on Bedrock/GCP/Azure/AWS variants or with feature flags off); `/desktop` (macOS/x64 Windows + subscription); `/autofix-pr` (web access); `/loop` no-interval behaviour differs on Bedrock/GCP/Foundry |
| Environment-disable | `CLAUDE_CODE_DISABLE_CRON=1` removes `/loop` + cron tools entirely |

**Do not assume a documented command is available on this account/plan/
platform** — the catalogue below records local evidence per command.

## 4. Aliases and removed commands

- Aliases (official): `/cost`→`/usage` · `/review`→`/code-review` ·
  `/settings`→`/config` · `/reset`,`/new`→`/clear` · `/bg`→`/background` ·
  `/share`→`/bug` (v2.1.212+) · `/quit`→`/exit` · `/checkup`→`/doctor` ·
  `/allowed-tools`→`/permissions` · `/proactive`→`/loop` ·
  `/peers`→`/list-agents` · `/app`→`/desktop` · `/ios`,`/android`→`/mobile`.
  Locally FOUND in binary: `/cost`, `/review`, `/settings`, `/reset`,
  `/new`, `/bg`, `/share`. Not found (weak evidence only): `/checkup`,
  `/allowed-tools`, `/quit`, `/proactive`, `/peers`.
- **REMOVED:** `/pr-comments` — removed in v2.1.91 per official docs (its
  string persists in the 2.1.234 binary, consistent with a removal notice);
  use direct queries instead.
- **NOT_AVAILABLE:** `/reload-skills` — absent from the official commands
  catalogue AND from the binary; treat as non-existent on 2.1.234 (skills
  reload via `/reload-plugins` for plugin skills; revalidate after
  upgrades).

## 5. Command catalogue by group

Attributes columns: **Mut** = changes files/settings/permissions/external
systems/session state (N = none beyond display; S = session state; F =
files; P = permissions/settings; X = external/cloud). **Persist** = current
turn (T), session (S), resumable session (R), project (PJ), user account
(U), external/cloud (X). Blanket rule for any row marked `NOT_RELEVANT`:
no AutoFX use case; do not use during recorded work; cosmetic/UI only; no
gate; token impact negligible; no example needed.

### 5.1 Help and visibility

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/help` | BUILT_IN | VERIFIED_ON_V2_1_234 | Show help + available commands | N | T | SAFE_ROUTINE |
| `/status` | BUILT_IN | VERIFIED_ON_V2_1_234 | Session status incl. model (runs immediately) | N | T | SAFE_ROUTINE |
| `/context` | BUILT_IN | VERIFIED_ON_V2_1_234 | Visualise context usage | N | T | SAFE_ROUTINE |
| `/tasks` | BUILT_IN | VERIFIED_ON_V2_1_234 (invoked this session) | List background work/subagents | N | T | SAFE_ROUTINE |
| `/workflows` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary) | Watch workflow progress | N | T | SAFE_ROUTINE |
| `/list-agents` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary; v2.1.224+) | List messageable agents/sessions | N | T | SAFE_ROUTINE |
| `/skills` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary) | List/inspect skills | N | T | SAFE_ROUTINE |
| `/release-notes` | BUILT_IN | VERIFIED_ON_V2_1_234 | View changelog | N | T | SAFE_ROUTINE |
| `/insights` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary; not in cloud sessions) | HTML report of recent sessions | F (local report) | PJ | BOUNDED_USE (output may reveal session content — treat as internal) |
| `/recap` | BUILT_IN | DOCUMENTED_NOT_LOCALLY_VERIFIED | One-line session summary | N | T | SAFE_ROUTINE if present |

### 5.2 Models, reasoning, and usage

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/model` | BUILT_IN | VERIFIED_ON_V2_1_234 | Show/switch model; saves default | S/U | S–U | BOUNDED_USE (view); switching = OWNER_APPROVAL_REQUIRED in main session |
| `/effort` | BUILT_IN | VERIFIED_ON_V2_1_234 | Show/set effort (low…max, ultracode, auto) | S | S | BOUNDED_USE (verify); lowering for critical work prohibited |
| `/fast` | BUILT_IN | VERIFIED_ON_V2_1_234 (v2.1.205+) | Toggle fast mode (Opus-served) | S | S | BOUNDED_USE — never for critical work (owner rule) |
| `/advisor` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary) | Second-model advisor on/off | S | S | BOUNDED_USE (token cost; governor routing still applies) |
| `/usage` (`/cost`) | BUILT_IN | VERIFIED_ON_V2_1_234 | Usage/costs (runs immediately) | N | T | SAFE_ROUTINE |
| `/usage-credits` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary; not in official commands table — purpose INFERRED from name: credit balance view) | View usage credits | N | T | SAFE_ROUTINE |

### 5.3 Context, compaction, and session continuity

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/compact [instructions]` | BUILT_IN | VERIFIED_ON_V2_1_234 | Replace history with summary | S (lossy) | S | BOUNDED_USE — continuity protocol first |
| `/autocompact` | BUILT_IN | VERIFIED_ON_V2_1_234 (v2.1.221+) | Set auto-compact threshold | S | S | BOUNDED_USE |
| `/clear` (`/reset`,`/new`) | BUILT_IN | VERIFIED_ON_V2_1_234 | New empty conversation (old one saved, resumable) | S | S→R | BOUNDED_USE — pushed handoff first (hard precondition) |
| `/resume [name]` | BUILT_IN | VERIFIED_ON_V2_1_234 | Switch to saved conversation | S | R | BOUNDED_USE |
| `/rename` / `claude -n` | BUILT_IN | VERIFIED_ON_V2_1_234 | Name session for resumability | S | R | SAFE_ROUTINE |
| `/branch` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary) | Copy conversation, switch to copy | S | R | BOUNDED_USE (record branch IDs in handoff) |
| `/rewind` | BUILT_IN | VERIFIED_ON_V2_1_234 | Roll code + conversation back to checkpoint | **F+S** | S | OWNER_APPROVAL_REQUIRED — can discard work |
| `/export [file]` | BUILT_IN | VERIFIED_ON_V2_1_234 | Export transcript as text | F (local) | PJ | BOUNDED_USE (transcript may contain sensitive discussion; never commit) |
| `/cd` | BUILT_IN | VERIFIED_ON_V2_1_234 (docs; v2.1.169+) | Move session to new directory | S/PJ | R | BOUNDED_USE (stay in C:\AutoFXV2.0) |
| `/add-dir` | BUILT_IN | VERIFIED_ON_V2_1_234 | Add working directory | S/P | S | OWNER_APPROVAL_REQUIRED (widens file access — e.g. V1 paths) |
| `claude --continue/--resume/--fork-session` | CLI flags | VERIFIED (docs + prior sessions) | Resume/branch from shell | S | R | BOUNDED_USE per RESUME_PROMPT.md |

### 5.4 Planning and side questions

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/plan [desc]` | BUILT_IN | VERIFIED_ON_V2_1_234 | Enter plan mode (read-only analysis before acting) | S | S | BOUNDED_USE (plan content still lands in repo docs, not only chat) |
| `/btw [question]` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary) | Side question OUTSIDE conversation history | N | T (not in history) | BOUNDED_USE — never for decisions/requirements (they would be lost to the record) |

### 5.5 Code, diff, and security review

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/diff` | BUILT_IN | VERIFIED_ON_V2_1_234 | Interactive diff viewer | N | T | SAFE_ROUTINE |
| `/code-review` (`/review`) | BUNDLED_SKILL | VERIFIED_ON_V2_1_234 (session roster) | Review diff/PR for bugs; `--fix` applies; `ultra` = cloud | N (plain) / **F** (`--fix`) / X (`ultra`,`--comment`) | T | BOUNDED_USE plain; `--fix`/`--comment`/`ultra` = OWNER_APPROVAL_REQUIRED |
| `/security-review` | BUNDLED_SKILL (docs list built-in; session roster shows skill) | VERIFIED_ON_V2_1_234 (roster) | Security review of pending changes | N | T | BOUNDED_USE |
| `/simplify` | BUNDLED_SKILL (as above) | VERIFIED_ON_V2_1_234 (roster) | Simplification review **that applies fixes** | **F** | T | OWNER_APPROVAL_REQUIRED during discovery (edits files) |
| `/verify` | BUNDLED_SKILL | VERIFIED_ON_V2_1_234 (binary; not in this session's roster — may be config-hidden) | Verify an implementation | possible F (runs project commands) | T | PROHIBITED_DURING_DISCOVERY (nothing to verify; post-authorisation BOUNDED_USE) |
| `/run` | BUNDLED_SKILL | VERIFIED_ON_V2_1_234 (roster) | Launch/drive the project app | **F/X** (executes app) | S | PROHIBITED_DURING_DISCOVERY (no app exists; would be implementation-adjacent) |

### 5.6 Autonomous goals and monitoring

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/goal [condition\|clear]` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary) | Work across turns until condition met; survives resume | S | R | OWNER_APPROVAL_REQUIRED |
| `/loop [interval] [prompt]` (`/proactive`) | BUNDLED_SKILL | VERIFIED_ON_V2_1_234 (roster + binary) | Re-run prompt on schedule; dynamic pacing; 7-day expiry; session-scoped | S (cron state in project `.claude`) | R (unexpired) | OWNER_APPROVAL_REQUIRED |
| `/schedule` | BUNDLED_SKILL | VERIFIED_ON_V2_1_234 (roster + binary) | Cloud routines (Anthropic-managed, machine-off execution) | **X** | X | OWNER_APPROVAL_REQUIRED |
| One-time reminders (natural language → CronCreate) | Tool-backed | VERIFIED (tools present) | Single-fire in-session reminder | S | R (until fire) | BOUNDED_USE |
| Monitor tool | Tool | VERIFIED (tool present) | Stream a background script's output instead of polling | S | S (not restored on resume) | BOUNDED_USE |

### 5.7 Agents, parallelism, and workflows

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/subtask` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary) | Hand side task to a subagent | S | S | BOUNDED_USE — governor routing mandatory (D-017) |
| `/fork` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary; v2.1.212+ semantics) | Copy conversation to new background session | S | R | BOUNDED_USE (continuity risk — record in handoff) |
| `/background [prompt]` (`/bg`) | BUILT_IN | VERIFIED_ON_V2_1_234 (binary) | Detach session as background agent | S | R | OWNER_APPROVAL_REQUIRED (unattended autonomous continuation) |
| `/batch <instruction>` | WORKFLOW (skill) | VERIFIED_ON_V2_1_234 (binary) | Parallel large-scale codebase changes via worktrees | **F** (mass edits) | S/PJ | PROHIBITED_DURING_DISCOVERY (mass change = implementation-shaped; post-authorisation OWNER_APPROVAL_REQUIRED per use) |
| `/deep-research <question>` | WORKFLOW | DOCUMENTED_NOT_LOCALLY_VERIFIED (v2.1.218+; absent from binary + roster) | Multi-agent web research with citations | X (web reads) | S | BOUNDED_USE if available — governor routing + approved research brief + token budget stated first |
| `/agents` | BUILT_IN | VERIFIED_ON_V2_1_234 | Subagent config info (v2.1.198+: pointer) | N | T | SAFE_ROUTINE (config changes themselves = owner-gated) |

### 5.8 Permissions and sandboxing

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/permissions` (`/allowed-tools`) | BUILT_IN | VERIFIED_ON_V2_1_234 | View/manage allow/ask/deny rules | **P** | PJ/U | View = SAFE_ROUTINE; any change = OWNER_APPROVAL_REQUIRED (committed settings are Jacob's, per the D-024 permissions note) |
| `/fewer-permission-prompts` | BUNDLED_SKILL | VERIFIED_ON_V2_1_234 (roster) | Scan transcripts, add allowlist to project settings | **P/F** | PJ | OWNER_APPROVAL_REQUIRED (writes `.claude/settings.json` — NEXT_ACTIONS § B item) |
| `/import` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary; platform-gated) | Import config from other coding agents | **P/F** | PJ/U | PROHIBITED_DURING_DISCOVERY (foreign config into a governed workspace) |

### 5.9 Plugins, skills, hooks, and MCP

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/plugin` | BUILT_IN | VERIFIED_ON_V2_1_234 | Manage plugins (list/install/enable/disable) | **P/F/X** | PJ/U | List = SAFE_ROUTINE; install/enable/disable = OWNER_APPROVAL_REQUIRED (D-013 gates) |
| `/reload-plugins` | BUILT_IN | VERIFIED_ON_V2_1_234 | Reload active plugins | S | S | BOUNDED_USE (only after an owner-approved plugin change) |
| `/reload-skills` | — | NOT_AVAILABLE (absent from official catalogue and binary) | — | — | — | REMOVED_OR_UNAVAILABLE — revalidate after upgrades |
| `/mcp` | BUILT_IN | VERIFIED_ON_V2_1_234 | Manage/authenticate MCP servers | **P/X** (connect/auth) | S/U | Status view = SAFE_ROUTINE; enable/connect/auth = PROHIBITED_DURING_DISCOVERY for D-015 out-of-scope connectors; otherwise OWNER_APPROVAL_REQUIRED |
| `/hooks` | BUILT_IN | VERIFIED_ON_V2_1_234 | View hook configurations | N (view) | T | SAFE_ROUTINE (view); hook changes = OWNER_APPROVAL_REQUIRED |
| `/memory` | BUILT_IN | VERIFIED_ON_V2_1_234 | Edit CLAUDE.md files; manage auto-memory | **F** (edits constitution) | PJ/U | View = SAFE_ROUTINE; editing CLAUDE.md = OWNER_APPROVAL_REQUIRED (authority-hierarchy document) |
| MCP prompts `/mcp__server__prompt` | MCP_PROMPT | Environment-dependent | Server-exposed prompts | Varies | Varies | PROHIBITED_DURING_DISCOVERY (all present connectors are D-015 out-of-scope) |
| Plugin commands (`product-management:*`, `claude-md-management:*`, `session-report`) | PLUGIN_COMMAND | VERIFIED_ON_V2_1_234 (roster; D-013-installed) | Per plugin | Varies (claude-md-management edits CLAUDE.md → owner-gated) | Varies | BOUNDED_USE within each plugin's D-013 purpose |
| `figma:*` skills/tools | PLUGIN_COMMAND | Present in environment | Design tooling | X | X | PROHIBITED_DURING_DISCOVERY (D-015; deferred to wireframe phase) |

### 5.10 GitHub, remote, and cloud integration

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/install-github-app` | BUILT_IN | VERIFIED_ON_V2_1_234 | Install Claude GitHub App + optional Actions workflows | **X/P** | X | OWNER_APPROVAL_REQUIRED (external install; Actions = deploy-adjacent) |
| `/install-slack-app` | BUILT_IN | VERIFIED_ON_V2_1_234 | Install Slack app (OAuth) | **X** | X | NOT_RELEVANT / OWNER_APPROVAL_REQUIRED if ever wanted |
| `/web-setup` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary; not in official commands table — purpose INFERRED: set up Claude Code on the web/cloud execution) | Cloud/web session setup | **X** | X/U | OWNER_APPROVAL_REQUIRED (creates cloud activity; code would leave this machine) |
| `/remote-control` | BUILT_IN | VERIFIED_ON_V2_1_234 (invoked by Jacob this session) | Continue this local session from another device | S/X (pairing) | S | BOUNDED_USE — owner-operated; Claude never initiates |
| `/teleport` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary) | Pull a web session into terminal | S/X | S | OWNER_APPROVAL_REQUIRED (imports external session state) |
| `/autofix-pr` | BUILT_IN | DOCUMENTED_NOT_LOCALLY_VERIFIED (web access) | Cloud session watches PR, pushes fixes | **X/F** | X | PROHIBITED_DURING_DISCOVERY (autonomous cloud pushes) |
| `/desktop` (`/app`) | BUILT_IN | VERIFIED_ON_V2_1_234 (binary; platform/plan-gated) | Continue in Desktop app | S | R | BOUNDED_USE (Desktop = visual review per D-011) |
| Routines / Desktop scheduled tasks | Cloud/Desktop features | DOCUMENTED (via `/schedule`; Desktop app) | Machine-independent scheduling | **X** | X | OWNER_APPROVAL_REQUIRED; never trading schedulers |

### 5.11 Debugging and diagnostics

| Command | Type | Availability | Purpose | Mut | Persist | AutoFX class |
|---|---|---|---|---|---|---|
| `/doctor` (`/checkup`) | BUNDLED_SKILL | VERIFIED_ON_V2_1_234 (binary; not in session roster — may load on demand) | Setup checkup; can TRIM CLAUDE.md / migrate guidance | N (diagnose) / **F** (trim) | T/PJ | Diagnose = BOUNDED_USE; any CLAUDE.md modification = OWNER_APPROVAL_REQUIRED |
| `/debug` | BUNDLED_SKILL | VERIFIED_ON_V2_1_234 (binary) | Debug logging + troubleshooting | S (logging) | S | BOUNDED_USE (logs may capture paths/content — never commit logs) |
| `/heapdump` | BUILT_IN | DOCUMENTED_NOT_LOCALLY_VERIFIED (absent from binary strings) | Write heap snapshot for memory diagnosis | **F** (memory dump) | PJ | OWNER_APPROVAL_REQUIRED — **highly sensitive**: a heap dump can contain raw conversation/credential residue; never commit, store outside repo, delete after use |
| `/bug` (`/share`) | BUILT_IN | VERIFIED_ON_V2_1_234 | Report bug; may share conversation with consent | **X** (shares content) | X | OWNER_APPROVAL_REQUIRED (conversation content leaves the machine) |
| `claude doctor` / `claude --version` | CLI | VERIFIED_ON_V2_1_234 | Version/diagnostics from shell | N | T | SAFE_ROUTINE |

### 5.12 UI and convenience (blanket: NOT_RELEVANT unless noted)

| Command | Type | Availability | Purpose | Class |
|---|---|---|---|---|
| `/theme`, `/color`, `/focus`, `/keybindings`, `/copy`, `/mobile` (`/ios`,`/android`), `/radio`, `/powerup`, `/passes`, `/upgrade`, `/feedback`, `/chrome`, `/ide`, `/exit` (`/quit`), `/login`, `/logout` | BUILT_IN | VERIFIED_ON_V2_1_234 (binary) except plan/platform gates in § 3 | Cosmetic/UI/account conveniences | NOT_RELEVANT (`/exit` BOUNDED_USE — checkpoint first; `/login`/`/logout` BOUNDED_USE — owner-operated identity) |
| `/init` | BUNDLED_SKILL | VERIFIED_ON_V2_1_234 (roster) | Initialise CLAUDE.md | PROHIBITED_DURING_DISCOVERY (CLAUDE.md exists and is owner-governed — would overwrite the constitution) |
| `/config` (`/settings`) | BUILT_IN | VERIFIED_ON_V2_1_234 | Open/set settings | View = SAFE_ROUTINE; changes = OWNER_APPROVAL_REQUIRED |
| `/privacy-settings` | BUILT_IN | DOCUMENTED_NOT_LOCALLY_VERIFIED (Pro/Max) | Privacy settings | Owner-operated |
| `/statusline` etc. (project skills: `update-config`, `keybindings-help`, `session-report`, `claude-api`, `dataviz`, artifact skills) | BUNDLED_SKILL/PLUGIN | VERIFIED (roster) | Various conveniences | BOUNDED_USE; `update-config` writes settings → OWNER_APPROVAL_REQUIRED |

### 5.13 Removed or deprecated

| Command | Status |
|---|---|
| `/pr-comments` | REMOVED (v2.1.91, per official docs) — use direct queries |
| `/reload-skills` | NOT_AVAILABLE on 2.1.234 (not in official catalogue; not in binary) |
| `/agents` interactive builder | Superseded from v2.1.198 (now points to asking Claude) |

## 6. Session-continuity facts that AutoFX policies rely on (official)

- `/clear` saves the old conversation (resumable via `/resume` and the
  rewind menu) but the **new context is empty** — repository handoffs are
  the only reliable state carrier (matches the standing AutoFX rule:
  documents, never chat memory).
- Resume restores: history, model (with exceptions), agent, permission mode
  (plan/bypass never restored), active `/goal` (counters reset), unexpired
  scheduled tasks. NOT restored: background Bash/monitor tasks,
  `/add-dir` additions, `--mcp-config`/`--settings`-style launch flags.
- Resume-from-summary (Pro/Max, >100k tokens, >1h idle) runs `/compact`
  over the history — detail loss applies; "resume full session as-is"
  preserves everything at higher per-request cost.
- `/loop`-first sessions are hidden from the session picker; recurring
  tasks expire after 7 days; jitter shifts fire times; tasks fire only
  while the session runs; `Esc` stops a waiting loop.
- Transcripts live at `~/.claude/projects/<project>/<session-id>.jsonl`,
  default 30-day retention (`cleanupPeriodDays`) — **not** a durable
  archive; the repository remains the source of truth.

## 7. AutoFX policy proposals (`PROPOSED` — Jacob approves/amends)

Standing rules first (apply to every command):

- **P-0.1** No command may bypass the no-build gate, D-015 tooling
  boundary, D-017/MODEL_ROUTING_POLICY routing, or the D-024 git rules.
  A command capable of fixing, editing, pushing, connecting, installing,
  changing permissions, or creating cloud activity is never classified or
  treated as routine read-only.
- **P-0.2** Mutating variants are gated separately from read variants
  (e.g. `/code-review` vs `/code-review --fix`).
- **P-0.3** Any command that sends conversation or repository content off
  this machine (`/bug` sharing, `/web-setup`, `/schedule` cloud routines,
  `ultra` cloud review, `/teleport`) requires Jacob's explicit approval
  per use while Q-014 (public repo) and the discovery gate stand.
- **P-0.4** Delegation-creating commands (`/subtask`, `/fork`,
  `/background`, `/batch`, `/deep-research`, parallel agents) route
  through the `autofx-model-governor` skill first, with token/cost
  consideration stated before launch.
- **P-0.5** After every Claude Code upgrade, run the § 9 revalidation
  before relying on any classification here.

Per-command policies (each: use when / never / gate):

- **/status — SAFE_ROUTINE.** Use at session start and before every
  critical task (D-012 mandatory check: `best` → Fable). Never skip before
  critical acceptance. No gate. Example: session-start checklist step 1.
- **/effort — BOUNDED_USE.** Use to verify Ultracode before critical work
  (D-012). Never lower effort for critical/judgment work or to stretch
  usage caps (policy: never trade quality for caps). Gate: changing effort
  below Ultracode for any critical task requires Jacob.
- **/model — BOUNDED_USE (view) / OWNER_APPROVAL_REQUIRED (switch).** Use
  to confirm the main session resolves to Fable. Never switch the main
  discovery session off `best`; subagent model choice belongs to the
  governor, not `/model`. Example: `/model` after launch, expect Fable.
- **/advisor — BOUNDED_USE.** Use only when an independent second opinion
  inside a turn is cheaper than a governor-routed review, and note the
  extra token cost. Never treat advisor output as the independent Fable
  review required for critical acceptance. Gate: none for occasional use;
  sustained use = owner cost decision.
- **/usage, /usage-credits — SAFE_ROUTINE.** Use when monitoring
  capacity (continuity thresholds) and before starting long work. Record
  displayed reset times exactly; never guess.
- **/context — SAFE_ROUTINE.** Use at ~60% context and before/after
  compaction. Feeds the 60–70%/75–80% continuity thresholds.
- **/autocompact — BOUNDED_USE.** Acceptable to set a conservative
  threshold so auto-compaction never lands mid-atomic-task. Never rely on
  it instead of handoff refresh — compaction is lossy.
- **/compact — BOUNDED_USE.** Only after the AutoFX continuity protocol:
  finish the atomic task, refresh handoffs/registers, commit; then compact
  with instructions naming what must survive (active phase, gate status,
  open questions). Never compact mid-decision or with unrecorded owner
  input in history.
- **/clear — BOUNDED_USE (hard precondition).** Only after a completed
  repository handoff (handoffs + registers updated, committed, and
  **pushed** to the approved branch). Never to "tidy up" mid-task. The
  saved-but-out-of-context old conversation is not an AutoFX state
  carrier.
- **/resume — BOUNDED_USE.** Use with named sessions per RESUME_PROMPT.md;
  verify repo state before acting (resume restores chat, not repo truth).
  Never treat restored conversation memory as authoritative over
  registers. Prefer "resume full session as-is" for critical sessions; if
  resuming from summary, re-read handoffs first (summary loss is real).
- **/btw — BOUNDED_USE (safeguard).** Side questions only (syntax help,
  quick lookups). **Never for decisions, requirements, approvals, or
  anything that must be on the record — /btw does not join conversation
  history and would silently vanish from the audit trail.** Anything
  material goes in a normal message and then into the registers.
- **/plan — BOUNDED_USE.** Use for structuring complex discovery analysis.
  Plan-mode output that matters must still be persisted to repo documents;
  plan mode is never restored on resume. Never let plan acceptance imply
  build authorisation (the gate phrase alone authorises).
- **/goal — OWNER_APPROVAL_REQUIRED.** Any `/goal` needs, in the goal text
  itself: explicit scope, completion condition, stopping conditions
  (including the twelve D-019 mandatory stops), and approval boundaries.
  Never for open-ended work; never spanning an authorisation gate. Note:
  goals survive resume — clear stale goals at session start.
- **/loop — OWNER_APPROVAL_REQUIRED.** Only for bounded session-local
  polling of documentation/CI-like state, with Jacob's per-use approval.
  **Never a production or trading scheduler** — it dies with the session,
  jitters fire times, rounds intervals, expires at 7 days, and skips
  missed fires. Any V2 production scheduling is designed in Rounds J/N as
  application architecture, never as a Claude Code loop.
- **/schedule — OWNER_APPROVAL_REQUIRED.** Cloud routines run on
  Anthropic-managed infrastructure without local files or permission
  prompts — external activity under D-019 (expenses/cloud) and P-0.3.
  **Never a production or trading scheduler** (same rule as /loop).
- **/tasks — SAFE_ROUTINE.** Use to monitor delegated/background work.
- **/subtask — BOUNDED_USE.** Governor routing first (classification,
  lowest permitted model, sufficiency); read-only agents only during
  discovery. Never for critical acceptance (Fable review rule).
- **/fork — BOUNDED_USE.** Only to isolate an experiment with the full
  context; record the fork in SESSION_LOG. Never run two forks writing to
  the same registers concurrently (register race = continuity hazard).
- **/background — OWNER_APPROVAL_REQUIRED.** Detached autonomous
  continuation is unattended work; Jacob authorises scope per use, same
  conditions as /goal.
- **/batch — PROHIBITED_DURING_DISCOVERY.** Mass parallel edits are
  implementation-shaped. Post-authorisation: OWNER_APPROVAL_REQUIRED per
  use with token/cost statement and governor routing (P-0.4).
- **/deep-research — BOUNDED_USE (if available; currently
  DOCUMENTED_NOT_LOCALLY_VERIFIED).** Requires: governor routing, an
  approved research brief per `.claude/rules/quantitative-evidence.md`
  § Research standard, and a stated token budget. Output lands as a dated
  research brief in the repo. Never as a substitute for the sceptical
  verification pass.
- **/diff — SAFE_ROUTINE.** Use before every commit (documentation diff
  review). Example: step 7 sequence below.
- **/code-review — BOUNDED_USE.** Plain review of documentation diffs is
  allowed. `--fix` (edits files), `--comment` (posts to GitHub), and
  `ultra` (cloud) are OWNER_APPROVAL_REQUIRED. During discovery the
  governed reviewers (autofx-opus-reviewer etc.) remain the primary
  review path for critical artefacts.
- **/security-review — BOUNDED_USE.** Read-only sweep of pending changes;
  useful before pushes. Never a substitute for the Round N threat model
  or the metadata-only secret scans.
- **/simplify — OWNER_APPROVAL_REQUIRED during discovery** (it applies
  edits). Post-authorisation: BOUNDED_USE within an approved phase.
- **/run — PROHIBITED_DURING_DISCOVERY.** There is no application and
  nothing may be launched. Post-authorisation: BOUNDED_USE inside the
  approved phase only.
- **/verify — PROHIBITED_DURING_DISCOVERY** (nothing implemented to
  verify). Post-authorisation: BOUNDED_USE; its results feed evidence
  records, never replace gate criteria.
- **/rewind — OWNER_APPROVAL_REQUIRED.** **Never silently discards
  approved or uncommitted work:** before any rewind — commit or stash the
  working tree, confirm with Jacob which checkpoint, record the rewind in
  SESSION_LOG. File rollback can erase register updates; conversation
  rollback can erase recorded owner input that was not yet persisted.
- **/permissions — SAFE_ROUTINE (view) / OWNER_APPROVAL_REQUIRED (any
  change).** The committed allowlist is Jacob's (see TOOLING_REGISTER
  permissions note); per-session grants are fine, durable rules are not.
- **/fewer-permission-prompts — OWNER_APPROVAL_REQUIRED.** Writes a
  durable allowlist to project settings — exactly the NEXT_ACTIONS § B
  settings decision; run only if Jacob approves that item.
- **/memory — SAFE_ROUTINE (view) / OWNER_APPROVAL_REQUIRED (edit).**
  CLAUDE.md is rank 2 in the authority hierarchy — edits are owner
  changes. Auto-memory entries must never carry decisions that belong in
  registers.
- **/plugin — SAFE_ROUTINE (list) / OWNER_APPROVAL_REQUIRED
  (install/enable/disable)** per the D-013 gate table.
- **/reload-plugins — BOUNDED_USE** immediately after an owner-approved
  plugin change; otherwise unnecessary.
- **/skills — SAFE_ROUTINE.** Listing only. (`/reload-skills`:
  NOT_AVAILABLE — do not attempt; revalidate after upgrades.)
- **/mcp — SAFE_ROUTINE (status view) only.** Enabling, reconnecting, or
  authenticating any server is PROHIBITED for D-015 out-of-scope
  connectors and OWNER_APPROVAL_REQUIRED for anything else.
- **/doctor — BOUNDED_USE (diagnosis) / OWNER_APPROVAL_REQUIRED (any
  offered CLAUDE.md trim or migration).** Decline write offers unless
  Jacob has approved them.
- **/debug — BOUNDED_USE.** For CLI faults; logs stay out of the repo.
- **/export — BOUNDED_USE.** Local, uncommitted exports only; transcripts
  can contain sensitive discussion. Never commit an export; never export
  to a synced/public location while Q-014 stands.
- **/heapdump — OWNER_APPROVAL_REQUIRED; highly sensitive.** (Currently
  DOCUMENTED_NOT_LOCALLY_VERIFIED.) A heap dump may embed raw session
  memory including any credential material the process ever held. If ever
  used: write outside the repository, never commit, never share, delete
  immediately after diagnosis, record the event in SESSION_LOG.
- **/install-github-app — OWNER_APPROVAL_REQUIRED.** External install +
  potential Actions workflows (deploy-adjacent; the no-build gate lists
  deploying workflows). Not needed for the current D-024 model.
- **/web-setup — OWNER_APPROVAL_REQUIRED.** Would move execution to cloud
  where repository content is cloned externally — a D-019 infrastructure
  and Q-014-adjacent decision.
- **/remote-control — BOUNDED_USE (owner-operated).** Jacob may attach
  his own devices; Claude never initiates pairing. Continuity rules
  unchanged — repo documents remain the source of truth.
- **/fast — BOUNDED_USE with a hard rule: never for critical AutoFX
  work.** Fast mode serves via Opus; D-012 requires Fable for critical
  judgment/acceptance. Acceptable only for trivial mechanical
  non-critical chores, and even then the governor's classification comes
  first. If in doubt, off.

## 8. Recommended command sequences (`PROPOSED`)

1. **Start every AutoFX session:** `claude --model best --effort
   ultracode` → `/status` (expect Fable) → `/effort` (expect Ultracode) →
   read handoffs per RESUME_PROMPT.md → `git status` / `git log` /
   `git remote -v` → restate phase/gate → `/usage` if capacity is a
   concern → clear any stale `/goal`.
2. **Begin a critical discovery task:** `/status` + `/effort` re-check →
   load `autofx-model-governor` → classify + show route → `/context`
   (headroom check) → proceed on Fable.
3. **Monitor context and usage:** `/context` at natural breakpoints;
   `/usage` before long work; act at 60–70% (finish atomic task + refresh
   handoffs) and 75–80% (checkpoint, then `/compact` or fresh session).
4. **Prepare for compaction:** finish atomic task → update registers +
   handoffs → commit (+ push if authorised) → `/compact <instructions
   naming phase, gate status, open questions>` → verify with `/context` →
   re-read CURRENT_STATE.md before continuing.
5. **Prepare for weekly usage exhaustion:** on any limit warning — stop
   opening new work → full checkpoint (handoffs + registers + commit +
   push) → `/usage` and record the displayed reset time exactly →
   `/rename` the session for later resumability → stop.
6. **Resume after a reset:** `claude --resume <name>` (or `--continue`) →
   if offered, prefer "resume full session as-is" for critical sessions →
   `/status` + `/effort` → re-verify git state → re-read handoffs (repo
   truth beats restored memory) → continue from NEXT_ACTIONS.
7. **Review documentation changes (current practice):** `/diff` → secret
   scan → consistency checks → optional `/security-review` → commit →
   push per D-024.
8. **Review future implementation changes (post-authorisation only):**
   `/diff` → `/code-review` (plain) → governed Fable review for critical
   code → tests → `/security-review` → commit → push to approved phase
   branch; `--fix`/`ultra` only with approval.
9. **Run bounded autonomous work:** obtain Jacob's scope approval →
   governor routing + token statement → prefer `/subtask` (read-only
   agents) → monitor with `/tasks` → record outcomes in registers; `/goal`
   or `/loop` only with the P-policies above satisfied.
10. **Diagnose Claude Code problems:** `claude --version` → `/status` →
    `/debug` → `/doctor` (decline write offers) → `/release-notes` (known
    changes) → if memory-related, discuss `/heapdump` with Jacob before
    use → record findings in SESSION_LOG.

## 9. Revalidation procedure (after every Claude Code upgrade)

1. `claude --version` — record the new version in this runbook's header
   and TOOLING_REGISTER.md.
2. Re-run the read-only binary token scan (method § 1) over the mandatory
   command list; diff FOUND/ABSENT against § 5.
3. Compare the session skill roster against § 5's BUNDLED_SKILL entries.
4. Re-fetch the three official pages (§ 1) and diff the catalogue:
   new/removed/renamed commands, changed availability gates, changed
   semantics for `/resume`, `/compact`, `/rewind`, `/loop`.
5. Update this runbook's entries and availability labels; mark vanished
   commands `REMOVED_OR_UNAVAILABLE`; never delete history — supersede.
6. Re-verify the D-012 launch checks still pass (`/status` → Fable,
   `/effort` → Ultracode) and the D-017 agent frontmatter still validates.
7. Record the revalidation in SESSION_LOG.md and refresh
   TOOLING_REGISTER.md § Claude Code command governance.
8. Any behaviour change affecting a `PROPOSED`/approved policy in § 7 goes
   to Jacob before the changed command is used.
