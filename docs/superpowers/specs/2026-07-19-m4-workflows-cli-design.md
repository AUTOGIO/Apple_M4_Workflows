# Apple M4 Workflows CLI — Design Spec

**Date:** 2026-07-19  
**Status:** Deferred (Approach 1 approved as direction; not started — this repo remains docs-only until explicitly begun)  
**Goal:** Turn the catalog/docs repo into a productized, cloud-API-first CLI that is installable, testable, and runnable with graceful optional macOS integrations.

---

## 1. Problem

The repo today is documentation plus empty `scripts/` and `config/` placeholders (`config/layouts/` reserved for Spencer stubs). Workflow ideas assume local LLMs (Ollama/LM Studio). The user wants:

- Cloud API LLMs only (no local model runtime required)
- Practices aligned with strong eng teams: one CLI, config as code, tests, CI, clear docs
- A suite that is “100% runnable” in the sense that core commands always work, and optional integrations degrade cleanly

## 2. Non-goals

- Rebuilding BlackDragon / Hammerspoon as a full second product
- Supporting local Ollama/LM Studio as first-class providers
- Guaranteeing Spencer Pro / Raycast / Ghostty are installed
- Shipping 50 unique production-grade automations on day one (catalog maps to a smaller set of real commands + stubs)

## 3. Success criteria

1. `make setup` installs deps and creates local config from `.env.example`.
2. `m4 doctor` reports env, API key presence, and optional app availability.
3. With a valid API key, these always succeed: `chat`, `summarize`, `review`, `shell-help`, `notes-draft`.
4. Optional commands (`layout`, `ops-center`, etc.) exit 0 with a skip message when the app is missing, or run when present.
5. Unit tests with mocked HTTP pass in CI without real API keys.
6. HTML dashboard and README document real CLI commands (no orphaned “local Ollama” copy).

## 4. Architecture

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│  CLI (bin)  │────▶│  Workflows   │────▶│  LLM Provider   │
│  m4 <cmd>   │     │  (pure logic)│     │  OpenAI/Anthropic│
└─────────────┘     └──────┬───────┘     └─────────────────┘
                           │
                    ┌──────▼───────┐
                    │  Integrations │
                    │  (optional)   │
                    │  Spencer,     │
                    │  Ghostty,     │
                    │  Shortcuts,   │
                    │  Notes        │
                    └──────────────┘
```

- **CLI layer:** argument parsing, exit codes, human/JSON output.
- **Workflows:** orchestration only; no direct `curl` in workflow files.
- **Providers:** single interface (`complete(messages, options)`); swap via config.
- **Integrations:** detect binary/app; run or skip with structured reason.

**Language:** TypeScript (Node 20+), ESM, compiled with `tsx` for dev and `tsc` for publishable `dist/`. Chosen for strong typing, easy packaging (`bin`), and CI familiarity.

## 5. Repository layout

```
/
  package.json
  tsconfig.json
  Makefile
  .env.example
  .gitignore
  README.md
  bin/m4                     # thin wrapper → dist/cli.js
  src/
    cli.ts                   # entry: commander/citty
    config.ts                # load .env + defaults
    doctor.ts
    providers/
      types.ts
      openai.ts
      anthropic.ts
      index.ts               # factory from config
    workflows/
      chat.ts
      summarize.ts
      review.ts
      shell-help.ts
      notes-draft.ts
      catalog.ts             # maps workflow IDs 1–50 → command or skip
    integrations/
      detect.ts
      spencer.ts
      ghostty.ts
      notes.ts
      shortcuts.ts
  scripts/macos/             # thin shell helpers called by integrations
  config/
    layouts/                 # Spencer layout JSON stubs + README (not top-level layouts/)
    defaults.json
    workflows.json           # catalog metadata for dashboard + CLI list
  docs/
    apple_m4_ecosystem.html  # updated: cloud + real commands
    USER_GUIDE.html          # updated: m4 CLI setup
    superpowers/specs/       # this document
  tests/
    providers.test.ts
    workflows.test.ts
    doctor.test.ts
  .github/workflows/ci.yml
```

## 6. Configuration

| Source | Purpose |
|--------|---------|
| `.env` / process env | `M4_PROVIDER`, `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, `M4_MODEL`, `M4_BASE_URL` (optional) |
| `config/defaults.json` | Default model names, timeouts, output prefs |
| `config/workflows.json` | Catalog entries: id, title, category, `command` or `status: optional\|stub` |

Secrets never committed. Prefer env vars; document macOS Keychain as optional future enhancement (out of v1 scope).

## 7. CLI surface (v1)

| Command | Behavior |
|---------|----------|
| `m4 doctor` | Checks Node, env keys, provider reachability (optional `--ping`), optional apps |
| `m4 list` | Lists catalog from `workflows.json` with runnable/skip status |
| `m4 chat [prompt]` | Interactive or one-shot chat via configured provider |
| `m4 summarize [-f file\|stdin]` | Summarize text |
| `m4 review [-f file\|stdin]` | Code review |
| `m4 shell-help <goal>` | Suggest shell command (print only; never auto-execute) |
| `m4 notes-draft` | Summarize stdin → write draft via Notes integration or print markdown |
| `m4 run <id\|slug>` | Run catalog entry by id |
| `m4 layout <name>` | Spencer restore or skip |
| `m4 ops-center` | Launch Ghostty ops helper or skip |
| `m4 version` | Package version |

Exit codes: `0` success or intentional skip; `1` user/config error; `2` provider/API failure.

## 8. Catalog strategy (50 → runnable)

Each of the 50 dashboard cards maps to one of:

1. **Core command** — implemented workflow  
2. **Optional integration** — runs if app present  
3. **Documented stub** — `m4 run N` prints what it would do and how to enable it (exit 0)

No card remains as “local Ollama only.” AI cards point at cloud provider commands.

## 9. Error handling

- Missing API key → exit 1 with setup hint (`cp .env.example .env`)
- Provider HTTP errors → exit 2 with status + truncated body
- Optional app missing → stderr message `SKIP: Spencer not found` + exit 0
- Network timeout → configurable; default 60s

## 10. Testing & CI

- Vitest for unit tests; mock `fetch` for providers  
- CI: `npm ci` → `npm test` → `npm run build` → `node dist/cli.js doctor --offline`  
- No live API calls in CI

## 11. Docs updates

- README: install, `make setup`, first commands, provider setup  
- Ecosystem HTML: filter “Cloud AI APIs”; each card shows `m4 …` command  
- USER_GUIDE: replace Ollama-centric architecture with `m4` CLI + cloud providers; keep hotkey/Hammerspoon sections labeled optional/external  

## 12. Implementation phases

1. Scaffold package, config, doctor, OpenAI provider, core workflows, tests, CI  
2. Anthropic provider + catalog `workflows.json` + `m4 list` / `m4 run`  
3. Optional integrations + layout stubs  
4. Rewrite HTML/README for cloud + real commands  

## 13. Open decisions (locked for v1)

| Decision | Choice |
|----------|--------|
| Language | TypeScript / Node 20+ |
| Primary provider | OpenAI-compatible API (works with OpenAI and compatible gateways) |
| Second provider | Anthropic Messages API |
| Local LLMs | Not supported in v1 |
| Package name / bin | `@local/m4-workflows` / `m4` |

---

## Spec self-review notes

- No TBD placeholders left for v1 scope.  
- Architecture matches CLI + providers + optional integrations.  
- Scope is one implementation plan (phases above), not multiple products.  
- “100% runnable” explicitly means core always works + optional/stub never crashes the suite.  
