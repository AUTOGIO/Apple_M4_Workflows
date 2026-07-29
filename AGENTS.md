# Agent notes — Apple M4 Workflows

Personal Mac automation hub (Shortcuts, scripts, layouts, local tool config). Prefer moves over copies; do not redesign features.

**Status:** Docs / design backlog only. Do not implement the deferred `m4` CLI unless the user explicitly starts that work.

## Folder layout

| Path | Purpose |
|------|---------|
| `scripts/` | Runnable helpers (`.sh`, `.zsh`, `.command`, AppleScript, Hammerspoon, Raycast) |
| `config/` | Non-secret settings (Ghostty, iTerm, Spencer Pro / monitor layouts, etc.) |
| `config/layouts/` | Spencer layout JSON stubs when added (prefer over a top-level `layouts/`) |
| `docs/` | Guides, HTML dashboards, design notes |
| `docs/prompts/` | AI prompt files (create when needed) |
| `data/` | CSV, Excel, exports, raw inputs (create when needed) |
| `assets/` | Images, icons, logos (create when needed) |
| `tests/` | Tests only (create when needed) |
| `archive/` | Obsolete files kept for reference — do not delete lightly |
| Root | Only `README.md`, `AGENTS.md`, `.gitignore`, workspace/toolchain files |

Do not invent new top-level folders. Use `src/` or `app/` only if application code appears (not both). If the deferred CLI is started, allow `src/`, `bin/`, `tests/`, and `.github/` as in the design spec; keep Spencer layouts under `config/layouts/` (not top-level `layouts/`).

## Rules

1. Prefer MOVE over copy; edit existing files over creating new ones.
2. No filename versioning (`Foo_v1.0.md` → `docs/foo.md`; unsure → `archive/`).
3. Merge duplicate folders (`config` vs `configs`, image folders → `assets/`).
4. Never commit secrets (`.env`, credentials). Do not put personal machine inventory here.
5. Folder names stay English as above; file content may stay Portuguese/English as already used.
6. After moves, fix broken paths if anything would break.
7. Delete only clear duplicates; otherwise move to `archive/`.
