# Repository Audit Report

> **Remediation applied 2026-07-29:** Stages 0–4 complete for docs-only scope (identity, CLI deferred, ecosystem ideas, USER_GUIDE prerequisites, MCP archived, Notes SQLite fixed, fadeIn, `.gitignore` LF, Git baseline, Hammerspoon symlink, folder rename to `Apple_M4_Workflows`). See `docs/UPGRADE_REPORT.md`. Full CLI / Vitest / CI still deferred. Findings below remain the historical audit record.

## 1. Executive Summary

This repository is a **documentation and scaffold hub**, not a runnable application. It contains seven tracked content files (~124K), empty `scripts/` and `config/` directories, no package manifests, no tests, no CI, and **no Git repository**.

**Documented intent** spans three conflicting identities: (1) a personal macOS automation hub (`README.md` / `AGENTS.md`), (2) a BlackDragon / Hammerspoon interactive guide (`docs/USER_GUIDE.html`) whose live behavior depends on `~/.hammerspoon` outside this tree, and (3) an approved but **unimplemented** TypeScript CLI design (`docs/superpowers/specs/2026-07-19-m4-workflows-cli-design.md`) that would replace local-Ollama catalog copy with a cloud-API `m4` CLI.

**Operational verdict:** Stable as static HTML/Markdown to browse; **not** operationally stable as an automation product. Highest priority is to choose one product identity, initialize version control, and either implement the approved CLI scaffold or deliberately keep the repo as docs-only and stop promising runnable workflows.

No committed credentials were found. No Critical findings.

| Severity | Count |
|----------|------:|
| Critical | 0 |
| High | 4 |
| Medium | 5 |
| Low | 3 |
| Informational | 2 |
| **Total** | **14** |

## 2. Audit Scope and Limitations

**Completed**

- Full inventory of all files under the repository root (7 files + empty dirs).
- Read of README, AGENTS, `.gitignore`, design spec, HTML dashboards, and MCP clipping.
- Pattern scans for secrets, hard-coded `/Users/...` paths, unsafe shell patterns, and dependency manifests.
- Safe host tool version checks and HTML parse smoke checks.
- Read-only observation of related host paths referenced by docs (`~/.hammerspoon`, `~/Documents/01_Projects/BlackDragon_Project`).

**Not executed (by design / stop conditions)**

- No package installs, builds, tests, deployments, or service starts (none exist to run safely).
- No modification of application or config files other than creating this report.
- Git status/log/diff unavailable — repository is not a Git working tree.
- Live Hammerspoon / Spencer / Ghostty / n8n / Ollama behavior not exercised.
- External MCP server projects referenced only in clipped documentation were not cloned or audited.

**Primary source of truth:** repository contents. Documentation treated as claims and compared to implementation (which is largely absent).

## 3. Initial Repository State

| Item | Value |
|------|--------|
| Repository root | `/Users/eduardofgiovannini/Developer/automation/(NOT _START )Apple_M4_Workflows` |
| Size | `124K` |
| Git | **Not a Git repository** (`fatal: not a git repository`) |
| Branch / remote / submodules / worktrees | N/A |
| Uncommitted changes | N/A (no `.git`) |
| Nested repositories | None under this root |
| `REPOSITORY_AUDIT.md` prior to audit | Did not exist |
| Large / generated dirs | None (`node_modules`, `.venv`, `dist`, etc. absent) |
| Empty dirs | `scripts/`, `config/` (both zero files since 2026-06-30) |
| Folder name signal | `(NOT _START )` suggests intentionally incomplete / not started |

## 4. Repository Purpose

### Documented behavior

- **README:** Personal hub for macOS / Apple M4 automation (Shortcuts, scripts, dual-monitor config). Browse HTML docs; add scripts/config later. Explicitly: “There is no install step yet.”
- **AGENTS.md:** Folder conventions for a personal automation hub; prefer moves; no secrets; English folder names.
- **`docs/apple_m4_ecosystem.html`:** Interactive catalog of **50** workflow *ideas* (Local AI / Spencer / Ghostty / Apple).
- **`docs/USER_GUIDE.html`:** “BlackDragon Automation Guide” for Hammerspoon + Ghostty Ops Center with `hammerspoon://` live actions.
- **Design spec:** Approved direction to productize a cloud-API-first TypeScript CLI (`m4`) with tests and CI; reject local Ollama as first-class.

### Implemented behavior

- Static documentation and HTML UIs only.
- No CLI, no scripts, no config payloads, no tests, no CI, no `.env.example`.

### Inferred behavior

- Intended as a starting point for personal Mac automation that later grew a separate CLI product vision.
- `USER_GUIDE.html` appears copied or mirrored from the Hammerspoon ecosystem (`~/.hammerspoon` exists with `modules/guide.lua` and related modules; this repo’s guide is not installed at `~/.hammerspoon/USER_GUIDE.html`).

### Unresolved assumptions

- Whether the approved CLI will be built in this repo or elsewhere.
- Whether BlackDragon Hammerspoon content should remain here or only live under `~/.hammerspoon`.
- Whether the parent folder name `(NOT _START )` means “do not implement yet” supersedes the “Approved” CLI spec.

### Likely user / deployment model

| Aspect | Assessment |
|--------|------------|
| Likely user | Single owner (personal Mac automation) |
| Inputs | Browser viewing of HTML; future: prompts, files, API keys (spec only) |
| Outputs | None from this repo today; future CLI stdout / optional app actions (spec) |
| Persistent data | None in-repo; host Hammerspoon/n8n/Ollama state is out of tree |
| External services | Documented/aspirational: Ollama, LM Studio, OpenAI/Anthropic (spec), n8n, Spencer, Ghostty, Raycast, Shortcuts MCP |
| Deployment | Local docs; no deployables |

## 5. Repository Map

| Path | Purpose (actual) |
|------|------------------|
| `README.md` | Project intro; docs-only run instructions |
| `AGENTS.md` | Agent/folder layout rules |
| `.gitignore` | macOS / secrets / Python / Node ignore patterns |
| `scripts/` | **Empty** — intended for shell/AppleScript/Hammerspoon/Raycast helpers |
| `config/` | **Empty** — intended for non-secret settings |
| `docs/apple_m4_ecosystem.html` | 50-card workflow idea dashboard |
| `docs/USER_GUIDE.html` | BlackDragon Hammerspoon interactive guide |
| `docs/unlocking-macos-with-ai-apple-shortcuts-mcp.md` | Third-party web clipping on Shortcuts MCP |
| `docs/superpowers/specs/2026-07-19-m4-workflows-cli-design.md` | Approved CLI design (unimplemented) |
| `data/`, `assets/`, `tests/`, `archive/`, `docs/prompts/` | Referenced in AGENTS; **not present** |
| `src/`, `bin/`, `layouts/`, `package.json`, `Makefile`, `.github/` | Required by CLI spec; **not present** |

**Absent:** application source, libraries, services, build files, CI/CD, databases, migrations, infrastructure, shell scripts, tests.

## 6. Technology Stack

| Technology | Evidence | Status in repo |
|------------|----------|----------------|
| Markdown / HTML / CSS / client JS | `docs/*.html`, `docs/*.md` | Present |
| Hammerspoon URL scheme + Lua (external) | `docs/USER_GUIDE.html` (`hammerspoon://guide/run`) | Documented; code outside repo |
| Ghostty / Spencer / Raycast / Shortcuts | HTML docs + AGENTS | Documented only |
| Ollama / LM Studio | Ecosystem + USER_GUIDE | Documented; contradicted by CLI spec |
| TypeScript / Node 20+ / Vitest / Commander | CLI design spec | **Not present** |
| OpenAI / Anthropic APIs | CLI design spec | **Not present** |
| n8n webhooks | USER_GUIDE (`localhost:5678`) | Documented only |
| GitHub Actions | Spec `.github/workflows/ci.yml` | **Not present** |
| Package managers | None (no `package.json`, etc.) | N/A |
| Shell scripts | `scripts/` empty | N/A |

Host tools observed during audit (not repo dependencies): zsh 5.9, bash 3.2, Python 3.14.6, Node v26.5.0, npm 11.17.0, Swift 6.4, Homebrew, `osascript`, `shortcuts`. `mise` not found (relevant only to clipped MCP install guide).

## 7. Architecture Overview

### Actual architecture

```text
[ Browser ]
    │
    ├─► apple_m4_ecosystem.html  (filterable idea cards; no backend)
    ├─► USER_GUIDE.html          (UI + hammerspoon:// + localStorage)
    └─► Markdown docs / design spec (read-only)

scripts/  ── empty
config/   ── empty
```

Optional **out-of-repo** control plane (documented by USER_GUIDE, partially present on host):

```text
USER_GUIDE.html ──hammerspoon://──► ~/.hammerspoon (guide.lua, terminal_ops, n8n, …)
                                         │
                                         ├─► Ghostty / Spencer / apps
                                         └─► localhost:5678 (n8n, if running)
```

### Aspirational architecture (design spec — not built)

CLI → workflows → LLM providers (OpenAI/Anthropic) + optional integrations (Spencer, Ghostty, Notes, Shortcuts).

### Architecture assessment

- **Cohesion:** Low across docs (three product stories).
- **Coupling:** USER_GUIDE tightly coupled to external Hammerspoon layout and BlackDragon project path.
- **Multiple sources of truth:** README vs USER_GUIDE vs ecosystem vs CLI spec.
- **Ambition–Capacity Mismatch:** Approved full product (CLI, providers, catalog, CI, tests) against a 7-file docs tree with empty script/config folders and no VCS.

## 8. Build, Test, and Run Procedure

### Canonical procedure (from README — matches reality)

1. **Prepare:** Clone/copy folder; no install.
2. **Configure:** None required for docs.
3. **Build:** None.
4. **Test:** None defined.
5. **Start:** Open `docs/apple_m4_ecosystem.html` and/or `docs/USER_GUIDE.html` in a browser (Safari preferred per USER_GUIDE for `file://` quirks).
6. **Stop:** Close browser.
7. **Recover:** N/A for docs; Hammerspoon issues require host permissions (documented in USER_GUIDE).

### Conflicting procedure (design spec — not implementable from this repo)

Claims `make setup`, `m4 doctor`, `npm test`, CI with `npm ci` → `npm test` → `npm run build`. **None of these files or commands exist.**

### USER_GUIDE “live” procedure (partially external)

Requires Hammerspoon running with `guide` URL handler, Accessibility/Automation grants, optional Ghostty/n8n/Ollama, and `~/Documents/01_Projects/BlackDragon_Project` — **path missing on the audited host**.

## 9. Commands Executed

| Command / check | Exit | Result |
|-----------------|-----:|--------|
| `pwd` | 0 | Repo root as above |
| `git status` / `branch` / `remote` / `log` / `submodule` / `worktree` | ≠0 | Not a Git repository |
| `du -sh .` | 0 | `124K` |
| `find` inventory (maxdepth / full) | 0 | 7 files; empty `scripts/`, `config/` |
| `file` on content files | 0 | HTML/Markdown/text; `.gitignore` mixed CRLF/LF |
| Secret-like regex scan | 0 | No real credentials; false positive in clipped SVG path data |
| Hard-coded `/Users/...` scan | 0 | None in repo |
| `zsh`/`bash`/`python3`/`node`/`npm`/`swift --version` | 0 | Tools present on host |
| `which mise brew osascript shortcuts` | 0 | `mise` missing; others present |
| HTML `HTMLParser` smoke parse | 0 | Both HTML files parse |
| `ls` BlackDragon project path | ≠0 | Path does not exist |
| `ls ~/.hammerspoon` | 0 | Hammerspoon config present with `modules/guide.lua` |
| `ls ~/.hammerspoon/USER_GUIDE.html` | ≠0 | Guide HTML not installed there |
| Package/test/build commands | — | **Skipped** — no manifests or scripts to run |

## 10. Findings Summary

| ID | Severity | Priority | Category | Finding | Confidence |
|---|---|---|---|---|---|
| AUDIT-001 | High | P1 | Reliability | No runnable automation surface | Confirmed |
| AUDIT-002 | High | P1 | Documentation | Conflicting product identities across docs | Confirmed |
| AUDIT-003 | High | P1 | Architecture | Approved CLI design unimplemented (ambition–capacity mismatch) | Confirmed |
| AUDIT-004 | High | P1 | Documentation | USER_GUIDE depends on external Hammerspoon / missing BlackDragon path | Confirmed |
| AUDIT-005 | Medium | P1 | Repository hygiene | No Git repository / version control | Confirmed |
| AUDIT-006 | Medium | P1 | Documentation | 50-workflow catalog has zero implementations | Confirmed |
| AUDIT-007 | Medium | P2 | Architecture | CLI spec layout conflicts with AGENTS.md rules | Confirmed |
| AUDIT-008 | Medium | P2 | Testing | No tests or CI despite design promises | Confirmed |
| AUDIT-009 | Medium | P2 | Security | Catalog advises Apple Notes SQLite access | High confidence |
| AUDIT-010 | Low | P3 | Documentation | Third-party MCP clip includes `curl \| sh` and broken markup | Confirmed |
| AUDIT-011 | Low | P3 | Correctness | Ecosystem filter animation references missing `@keyframes` | Confirmed |
| AUDIT-012 | Low | P3 | Documentation | `.gitignore` allows `.env.example` but file is missing | Confirmed |
| AUDIT-013 | Informational | P3 | macOS | Docs recommend `sudo ln -sf` for Spencer CLI | Confirmed |
| AUDIT-014 | Informational | P3 | Repository hygiene | Mixed CRLF/LF in `.gitignore`; `(NOT _START )` folder name | Confirmed |

## 11. Critical Findings

None.

## 12. High Findings

### [AUDIT-001] No runnable automation surface

- Severity: High
- Priority: P1
- Confidence: Confirmed
- Category: Reliability
- File: `scripts/`, `config/`, `README.md`
- Location: empty directories; README “How to run”
- Evidence:
  - `scripts/` and `config/` contain no files (`ls -la` shows only `.` / `..`).
  - No `package.json`, `Makefile`, `bin/`, `src/`, or shell entry points exist.
  - README states: “There is no install step yet.”
- Impact:
  - Users cannot build, test, or run automations from this repository; operational value is documentation browsing only.
- Recommendation:
  - Either add a minimal real entry point (one script or CLI scaffold per the approved spec) or revise README/AGENTS to state explicitly that this repo is docs-only until a start decision is made.
- Validation:
  - `find scripts config -type f` returns intended files; or README contains a single unambiguous “docs-only” statement with no runnable claims.

### [AUDIT-002] Conflicting product identities across documentation

- Severity: High
- Priority: P1
- Confidence: Confirmed
- Category: Documentation
- File: `README.md`, `docs/USER_GUIDE.html`, `docs/apple_m4_ecosystem.html`, `docs/superpowers/specs/2026-07-19-m4-workflows-cli-design.md`
- Location: titles, architecture sections, AI provider strategy
- Evidence:
  - README: “Personal hub for custom macOS / Apple M4 automation.”
  - USER_GUIDE title: “BlackDragon — Interactive Automation Guide”; architecture table lists `ai.lua + Ollama`.
  - Ecosystem filter: “Local AI & LLMs” with 14+ Ollama/LM Studio mentions.
  - CLI spec: “Cloud API LLMs only”; “no orphaned local Ollama copy”; success criteria include `m4 doctor` / `make setup`.
- Impact:
  - Operators cannot tell which stack to install or which docs are authoritative; wasted setup on abandoned local-LLM paths.
- Recommendation:
  - Pick one canonical identity for this repo and mark other docs as `archive/` or “external / optional.” Align HTML copy with that choice.
- Validation:
  - Single README “Product” section; remaining docs either match it or are labeled obsolete with dates.

### [AUDIT-003] Approved CLI design unimplemented (ambition–capacity mismatch)

- Severity: High
- Priority: P1
- Confidence: Confirmed
- Category: Architecture
- File: `docs/superpowers/specs/2026-07-19-m4-workflows-cli-design.md`
- Location: Status line; §5 Repository layout; §12 Implementation phases
- Evidence:
  - Spec status: “Approved direction (Approach 1).”
  - Spec requires `package.json`, `src/`, `bin/m4`, `tests/`, `.github/workflows/ci.yml`, `.env.example` — none exist.
  - Spec itself describes today as “documentation plus empty `scripts/` … and `config/` folders” — still accurate ~10 days after the dated spec (audit date 2026-07-29).
- Impact:
  - Architecture complexity and success criteria exceed maintenance capacity; creates false expectation of a productized CLI.
- Recommendation:
  - Do not implement the full four-phase plan yet. Either demote the spec to “proposed / deferred,” or implement **phase 1 only** (scaffold + `doctor` + one provider + tests) after Git init.
- Validation:
  - Spec status matches reality (`Deferred` or phase-1 artifacts present and `m4 doctor --offline` works).

### [AUDIT-004] USER_GUIDE depends on external Hammerspoon / missing BlackDragon path

- Severity: High
- Priority: P1
- Confidence: Confirmed
- Category: Documentation
- File: `docs/USER_GUIDE.html`
- Location: hero “Live actions via hammerspoon://”; project path tips; footer path; `buildGuideURL` / `fireURL` (~747–774)
- Evidence:
  - Buttons fire `hammerspoon://guide/run?action=...` via hidden iframe; no fallback when Hammerspoon is absent.
  - Documents project path `~/Documents/01_Projects/BlackDragon_Project` — absent on audited host.
  - Footer claims `~/.hammerspoon/USER_GUIDE.html`; that path does not exist (guide lives only in this repo). Host does have `~/.hammerspoon/modules/guide.lua`.
- Impact:
  - “Live” UI silently no-ops or targets a different machine layout; onboarding instructions fail on missing project path.
- Recommendation:
  - Label the guide as requiring Hammerspoon + list prerequisites; add a visible non-live mode; remove or parameterize BlackDragon-specific paths for this hub; optionally symlink/copy guide into `~/.hammerspoon` if that remains the home.
- Validation:
  - Opening the guide without Hammerspoon shows an explicit unavailable state; with Hammerspoon, one documented action succeeds; paths resolve or are removed.

## 13. Medium Findings

### [AUDIT-005] No Git repository / version control

- Severity: Medium
- Priority: P1
- Confidence: Confirmed
- Category: Repository hygiene
- File: repository root
- Location: absence of `.git`
- Evidence:
  - All `git` commands failed with “not a git repository.”
  - AGENTS.md and `.gitignore` assume commit workflows and secret exclusion.
- Impact:
  - No history, branching, review, or safe rollback; audit/remediation cannot use standard VCS controls.
- Recommendation:
  - `git init`, add remote if desired, commit baseline after clarifying product identity. Do not invent history.
- Validation:
  - `git status` succeeds; initial commit contains only intended non-secret files.

### [AUDIT-006] 50-workflow catalog has zero implementations

- Severity: Medium
- Priority: P1
- Confidence: Confirmed
- Category: Documentation
- File: `docs/apple_m4_ecosystem.html`
- Location: cards 1–50; e.g. card 22 references `launch-terminal-operations-center.applescript`
- Evidence:
  - Exactly 50 `.card` elements; descriptions are aspirational prose.
  - Referenced scripts/configs (AppleScript, Spencer layouts, Raycast extensions) are not in `scripts/` or `config/`.
- Impact:
  - Catalog overstates capability; users may believe workflows are inventory rather than ideas.
- Recommendation:
  - Relabel UI as “Ideas / backlog”; or map each card to `implemented | external | stub` once a CLI/catalog exists (per spec §8).
- Validation:
  - Every card has an explicit status badge matching reality.

### [AUDIT-007] CLI spec layout conflicts with AGENTS.md rules

- Severity: Medium
- Priority: P2
- Confidence: Confirmed
- Category: Architecture
- File: `AGENTS.md`, `docs/superpowers/specs/2026-07-19-m4-workflows-cli-design.md`
- Location: AGENTS “Do not invent new top-level folders”; spec §5 (`src/`, `bin/`, `layouts/`, `tests/`, `.github/`)
- Evidence:
  - AGENTS allows `src/` or `app/` only if application code appears; forbids inventing new top-level folders.
  - Spec introduces `layouts/` (not listed in AGENTS table) and assumes empty `layouts/` today though the directory does not exist.
- Impact:
  - Agents following AGENTS will refuse the scaffold the approved spec requires.
- Recommendation:
  - Update AGENTS once when implementation starts (allowlisted layout for the CLI), or move Spencer layouts under `config/layouts/` to avoid a new top-level name.
- Validation:
  - AGENTS and spec agree on the same directory tree.

### [AUDIT-008] No tests or CI despite design promises

- Severity: Medium
- Priority: P2
- Confidence: Confirmed
- Category: Testing
- File: `docs/superpowers/specs/2026-07-19-m4-workflows-cli-design.md` (§10); missing `tests/`
- Location: Vitest / `.github/workflows/ci.yml` claims
- Evidence:
  - No `tests/` directory; AGENTS says create when needed — never created.
  - Spec success criterion #5 requires unit tests with mocked HTTP in CI.
- Impact:
  - No regression safety if/when code is added; design overpromises quality gates.
- Recommendation:
  - When phase 1 lands, add Vitest + CI as part of the same PR as the first provider — not afterward.
- Validation:
  - CI green on `doctor --offline` without API keys.

### [AUDIT-009] Catalog advises Apple Notes SQLite access

- Severity: Medium
- Priority: P2
- Confidence: High confidence
- Category: Security
- File: `docs/apple_m4_ecosystem.html`
- Location: card 45 “Local Model RAG via Notes”
- Evidence:
  - Card text: “A python script that reads your Apple Notes SQLite DB and uses it as context for local LM Studio queries.”
- Impact:
  - If followed, risks privacy exposure, DB locking/corruption, and bypass of Notes’ normal access controls; guidance without safety warnings.
- Recommendation:
  - Remove or rewrite with a warning and safer APIs (Shortcuts / AppleScript export), and never recommend raw Notes DB writes.
- Validation:
  - Card text no longer recommends direct SQLite access, or includes explicit risk + safer alternative.

## 14. Low and Informational Findings

### [AUDIT-010] Third-party MCP clip includes `curl | sh` and broken markup

- Severity: Low
- Priority: P3
- Confidence: Confirmed
- Category: Documentation
- File: `docs/unlocking-macos-with-ai-apple-shortcuts-mcp.md`
- Location: Homebrew install instructions; long SVG/HTML residue; mode `600`
- Evidence:
  - Documents `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`.
  - File is a Skywork/Skypage clip with truncated charts and embedded SVG noise; permissions `-rw-------`.
- Impact:
  - Readers may run remote install pipelines without understanding this is third-party marketing content, not project runbooks.
- Recommendation:
  - Move to `archive/` or add a header: “External clipping — not maintained; do not treat as setup for this repo.” Prefer linking out over vendoring the clip.
- Validation:
  - File header states provenance; or file relocated under `archive/`.

### [AUDIT-011] Ecosystem filter animation references missing `@keyframes`

- Severity: Low
- Priority: P3
- Confidence: Confirmed
- Category: Correctness
- File: `docs/apple_m4_ecosystem.html`
- Location: filter script ~line 439; CSS block lines 7–143
- Evidence:
  - JS sets `card.style.animation = 'fadeIn 0.5s ease forwards'` but no `@keyframes fadeIn` exists in the stylesheet (`rg` found no matches).
- Impact:
  - Cosmetic only; filter show/hide still works via `.hidden`.
- Recommendation:
  - Add `@keyframes fadeIn` or remove the animation assignment.
- Validation:
  - Filter toggle shows animation or no console/style reference to undefined keyframes.

### [AUDIT-012] `.gitignore` allows `.env.example` but file is missing

- Severity: Low
- Priority: P3
- Confidence: Confirmed
- Category: Documentation
- File: `.gitignore`
- Location: `!.env.example`
- Evidence:
  - Negation pattern present; `.env.example` does not exist (required by CLI spec).
- Impact:
  - Harmless today; signals unfinished secret/config scaffolding.
- Recommendation:
  - Add `.env.example` only when CLI config lands; until then the negation is fine to keep.
- Validation:
  - When CLI exists, `.env.example` lists `M4_PROVIDER`, `OPENAI_API_KEY`, `ANTHROPIC_API_KEY` without real secrets.

### [AUDIT-013] Docs recommend `sudo ln -sf` for Spencer CLI

- Severity: Informational
- Priority: P3
- Confidence: Confirmed
- Category: macOS
- File: `docs/USER_GUIDE.html`
- Location: tip card “Spencer layouts”
- Evidence:
  - `sudo ln -sf /Applications/Spencer.app/Contents/MacOS/SpencerCLI /usr/local/bin/spencer`
- Impact:
  - Privileged symlink into `/usr/local/bin`; acceptable for some personal setups but elevates install risk if path is wrong.
- Recommendation:
  - Prefer documenting `PATH` export or `~/.local/bin` without sudo when implementing real Spencer helpers.
- Validation:
  - Install instructions succeed without unnecessary sudo, or sudo necessity is explained.

### [AUDIT-014] Mixed CRLF/LF in `.gitignore`; `(NOT _START )` folder name

- Severity: Informational
- Priority: P3
- Confidence: Confirmed
- Category: Repository hygiene
- File: `.gitignore`; repository directory name
- Location: `od -c` shows `\r\n` around blank lines; parent folder `(NOT _START )Apple_M4_Workflows`
- Evidence:
  - `file .gitignore` reports “CRLF, LF line terminators.”
  - Folder name encodes a “not started” signal conflicting with “Approved” CLI status.
- Impact:
  - Minor tooling noise; naming ambiguity about project readiness.
- Recommendation:
  - Normalize `.gitignore` to LF; rename folder when product identity is decided.
- Validation:
  - `file .gitignore` shows LF only; folder name matches project status.

## 15. Security Assessment

| Area | Result |
|------|--------|
| Committed secrets / keys / private keys | **None found** |
| `.env` files | Absent (correctly gitignored if VCS added) |
| Shell injection / `eval` / `rm -rf` in repo scripts | N/A — no scripts |
| `curl \| sh` | Present only in third-party clipping (AUDIT-010) |
| Network bindings | USER_GUIDE references localhost n8n/MQTT/WebSocket as examples; simulated in-page, not a server |
| `hammerspoon://` URL firing | Local privilege to drive Hammerspoon if running — expected for guide; no auth beyond OS permissions |
| Sensitive guidance | Notes SQLite RAG idea (AUDIT-009) |
| Supply chain | No lockfiles / dependencies to audit |

**Overall:** Low security exposure because there is almost no executable surface. Main risks are **misleading guidance** and **future** API-key handling when the CLI is built (spec correctly says secrets never committed).

## 16. Correctness Assessment

- HTML documents parse successfully.
- Filter logic in ecosystem dashboard is coherent; animation name is undefined (AUDIT-011).
- USER_GUIDE webhook simulator does not perform network I/O (labels “simulated”) — correct for a static guide.
- Material correctness failure is **documentary**: claims of live workflows, local AI architecture, and CLI commands do not match repository contents (AUDIT-002, AUDIT-004, AUDIT-006).

## 17. Reliability and Operational Stability

| Concern | Assessment |
|---------|------------|
| Startup / shutdown | Docs: N/A. Live guide: depends on Hammerspoon process. |
| Monitoring / health checks | None in-repo. Spec proposes `m4 doctor` — missing. |
| Retries / timeouts | N/A |
| Machine-specific paths | BlackDragon path + `~/.hammerspoon` assumptions (AUDIT-004) |
| Silent failure | Guide buttons fire custom URLs with toast only — no confirmation of success |
| Fresh clone operability | Can open HTML; cannot run automations; no Git clone history |

**Verdict:** Reliable as static documentation. Unreliable as an automation suite.

## 18. Architecture and Complexity Assessment

**Ambition–Capacity Mismatch:** Confirmed.

Defer or delete complexity that is not backed by code:

- Full 50-card “product” framing → backlog/ideas.
- Dual local-LLM + cloud-CLI narratives → one narrative.
- BlackDragon ops-center guide inside this hub → keep in Hammerspoon repo/config or clearly “external.”
- Four-phase CLI + Anthropic + catalog + integrations → start with phase 1 only after VCS.

Prefer incremental simplification: docs-only honesty now, then thin CLI scaffold, then optional integrations.

## 19. Dependency Assessment

- **No application dependencies** (no manifests or lockfiles).
- Host optional tools are documented but not declared as versioned requirements.
- Spec would introduce Node 20+, Vitest, OpenAI/Anthropic SDKs or raw `fetch` — not yet applicable.
- `.gitignore` anticipates Python/Node clutter appropriately.

## 20. Testing Assessment

- No test suites, fixtures, or test commands.
- Design requires Vitest with mocked HTTP — unmet.
- Manual validation possible: open HTML files; optional host Hammerspoon checks.

Critical untested paths (when built): provider auth errors, skip-on-missing-app, `shell-help` never executing commands.

## 21. Documentation Assessment

| Doc | Accuracy vs implementation |
|-----|----------------------------|
| README | Accurate for docs-only; understates identity conflict |
| AGENTS.md | Internally consistent; conflicts with future CLI layout |
| Ecosystem HTML | Idea catalog misreadable as inventory; Ollama-centric vs approved cloud direction |
| USER_GUIDE | Documents external BlackDragon/Hammerspoon system; paths stale on this host |
| CLI design spec | Clear and detailed; **not implemented**; status “Approved” overstates delivery |
| MCP clipping | External; not project setup; noisy markup |

Missing: recovery/backup procedures (N/A today), contribution guide, env examples, single source of truth for “how to run.”

## 22. macOS and Apple-Specific Assessment

- Targets Apple Silicon M4 / dual monitor / Shortcuts / Spencer / Ghostty — all documentary.
- No Xcode project, entitlements, LaunchAgents, or binaries in-repo.
- USER_GUIDE correctly mentions Accessibility and Automation permission needs for Hammerspoon.
- Hard-coded `/Users/<name>/` paths: none; uses `~/...` for BlackDragon (still machine-layout specific).
- Spencer `sudo ln` guidance: see AUDIT-013.
- Host has working `~/.hammerspoon` with modules matching guide narrative — **outside** this repository’s ownership boundary.

## 23. Shell Script Assessment

- **No shell scripts** in `scripts/` or elsewhere in the repository.
- Shell content appears only as documentation snippets (Ollama, Spencer, Ghostty config).
- No `set -euo pipefail`, quoting, or destructive operations to review in-repo.

## 24. Repository Hygiene

| Item | Status |
|------|--------|
| `.gitignore` | Present; mixed line endings |
| Secrets / logs / caches | None committed |
| Empty placeholders | `scripts/`, `config/` |
| Archives | None; MCP clip and USER_GUIDE candidates for archive or externalization |
| Duplicate product docs | Identity conflict (AUDIT-002) |
| Fresh clone | Not Git-backed; copy works for HTML viewing |
| Folder naming | `(NOT _START )` awkward and status-signaling |

## 25. Prioritized Remediation Plan

### Stage 0 — Preserve and Validate

1. Decide product identity in writing (docs-only hub vs Hammerspoon mirror vs `m4` CLI).
2. Initialize Git and create a baseline commit of current files (no secrets).
3. Snapshot or note relationship to `~/.hammerspoon` so moves do not orphan live automation.
4. **Validation:** `git status` clean after baseline; decision recorded in README.
5. **Rollback:** Keep a zip copy of the folder before renames.
6. **Do not yet:** Implement full CLI, rewrite all 50 cards, or delete Hammerspoon host config.

### Stage 1 — Critical Stabilization

1. Resolve AUDIT-002 / AUDIT-004: one README identity; demote or relocate USER_GUIDE / Ollama catalog claims.
2. Update CLI spec status to match reality (`Deferred` or start phase 1 only) — AUDIT-003.
3. Relabel ecosystem as ideas or stub statuses — AUDIT-006.
4. **Validation:** Fresh reader can answer “what runs from this repo?” from README alone.
5. **Dependencies:** Stage 0 Git init first.

### Stage 2 — Reliability Improvements

1. If keeping USER_GUIDE: document prerequisites; fix/remove BlackDragon path; detect Hammerspoon availability messaging.
2. If building CLI: implement phase 1 (`doctor`, one provider, `.env.example`, tests) — not optional integrations.
3. Align AGENTS.md with chosen tree — AUDIT-007.
4. **Validation:** `m4 doctor --offline` or explicit docs-only badge; no broken path references.

### Stage 3 — Simplification

1. Archive MCP clipping or replace with a short link list — AUDIT-010.
2. Remove Notes SQLite advice — AUDIT-009.
3. Drop dual Ollama vs cloud narratives from HTML.
4. **Do not attempt yet:** 50 production automations, local LLM provider support, rebuilding BlackDragon inside this repo.

### Stage 4 — Maintainability

1. Add CI only with real code.
2. Normalize line endings; rename folder when status clear — AUDIT-014.
3. Fix fadeIn keyframes — AUDIT-011.
4. **Validation:** CI green; `file` shows LF; folder name matches README.

## 26. Quick Wins

1. Add a one-paragraph README “Status” (docs-only / CLI deferred).
2. Change ecosystem subtitle/filter from implying shipped workflows to “Ideas.”
3. Header banner on USER_GUIDE: “Requires Hammerspoon; not runnable from this repo alone.”
4. Set CLI spec Status to `Deferred` or `Approved — not started`.
5. `git init` + baseline commit.
6. Move MCP clipping under `archive/` or add provenance header.
7. Remove or warn on Notes SQLite card text.
8. Add missing `@keyframes fadeIn` or delete animation line.
9. Normalize `.gitignore` to LF.
10. Soften Spencer install tip to avoid unnecessary `sudo` when documenting future scripts.

## 27. Deferred Improvements

- Full TypeScript CLI with Anthropic + catalog mapping of all 50 cards.
- Optional Spencer/Ghostty/Notes integrations.
- Vitest + GitHub Actions.
- Rewriting USER_GUIDE into a generic M4 hub guide without BlackDragon.
- Keychain-backed secrets (spec: out of v1).
- Local Ollama providers (explicitly non-goal in approved CLI direction).

## 28. Unresolved Questions

1. Does `(NOT _START )` override the “Approved” CLI spec until the user explicitly starts implementation?
2. Should BlackDragon / Hammerspoon documentation leave this repository entirely?
3. Will the eventual CLI live here (`@local/m4-workflows`) or in a new GitHub remote?
4. Is the 50-card catalog still desired after rejecting local LLMs as first-class?
5. Should empty `scripts/` / `config/` remain as placeholders or be omitted until needed?

## 29. Final Recommendation

Treat this repository as a **docs and design backlog**, not a product binary. Stabilize identity and version control first. Do **not** begin a large CLI rewrite until Stage 0–1 decisions are explicit. The highest-value next action is: **declare one canonical purpose in README, initialize Git, and either defer the CLI spec or implement only phase-1 scaffold with tests** — leaving Hammerspoon/BlackDragon and the 50-idea catalog clearly marked as external or aspirational.
