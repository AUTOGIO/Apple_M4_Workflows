# Apple M4 Workflows

Personal hub for custom macOS / Apple M4 automation: Shortcuts-oriented workflows, scripts, and local tool config for a dual-monitor setup.

## Product / Status

**This repository is docs and design only.** Nothing here is a runnable automation product yet.

| Surface | Role |
|---------|------|
| HTML / Markdown under `docs/` | Browse in a browser |
| `scripts/` / `config/` | Empty placeholders — add helpers when you build them |
| `docs/USER_GUIDE.html` | BlackDragon / Hammerspoon companion guide (requires host Hammerspoon; not runnable from this repo alone) |
| `docs/apple_m4_ecosystem.html` | **Ideas / backlog** (50 cards) — not an inventory of shipped workflows |
| CLI design spec | **Deferred** — see `docs/superpowers/specs/2026-07-19-m4-workflows-cli-design.md` |

Canonical purpose: a personal automation **hub and backlog**. Live Hammerspoon behavior lives under `~/.hammerspoon` on the Mac, not in this tree. See `docs/HAMMERSPOON.md`.

Folder name: `Apple_M4_Workflows` (docs-only status; CLI deferred — not “not started” as incomplete product ambiguity).

## Where things live

- **`docs/`** — Guides and dashboards. Open `docs/apple_m4_ecosystem.html` for the idea catalog; see also `docs/USER_GUIDE.html` (Hammerspoon prerequisites).
- **`docs/external-links.md`** — Pointers to archived clippings and deferred design.
- **`scripts/`** — Shell, AppleScript, Hammerspoon, and similar helpers (add as you build them).
- **`config/`** — Non-secret settings (terminals, Spencer Pro / monitor layouts, prompts that are not secrets).
- **`archive/`** — Obsolete or third-party clippings kept for reference.

## How to run

There is no install step and no CLI yet. Browse the HTML docs above. Drop new automations into `scripts/` and settings into `config/` when you build them. See `AGENTS.md` for folder rules.
