# Upgrade report — Apple M4 Workflows

**Date:** 2026-07-29  
**Source:** Remediation of `REPOSITORY_AUDIT.md` (14 findings; 0 Critical)  
**Outcome:** Repo stabilized as a **docs / design hub**; CLI remains **deferred**; Git baseline on `main`.

## Decisions locked

| Question | Decision |
|----------|----------|
| Product identity | Docs + design backlog (not a runnable automation product) |
| CLI (`m4`) | Deferred — Approach 1 remains the future direction, not started |
| BlackDragon / USER_GUIDE | Kept as Hammerspoon companion; prerequisites + optional project path |
| 50-card catalog | Ideas / stubs only — not shipped inventory |
| Empty `scripts/` / `config/` | Kept as placeholders (`.gitkeep`) |
| Parent folder name | Renamed to `Apple_M4_Workflows` (dropped `(NOT _START )`) |

## What changed

### Identity & docs
- README **Product / Status** table — single answer to “what runs from this repo?”
- CLI design spec status → **Deferred**; layouts path → `config/layouts/`
- `AGENTS.md` aligned (deferred CLI; no top-level `layouts/`)
- `docs/HAMMERSPOON.md` — host vs repo boundary
- `docs/external-links.md` — archived clipping + design pointers

### HTML / UX
- Ecosystem: ideas framing, status badges, cloud-vs-local narrative banner, `@keyframes fadeIn`
- Card 45: removed raw Notes SQLite advice; safer Shortcuts/AppleScript path
- USER_GUIDE: Hammerspoon requirement banner, optional BlackDragon path, Spencer without forced sudo, clearer live-action toasts, AI tab labeled optional

### Hygiene
- MCP Shortcuts clip moved to `archive/` with provenance header
- `.gitignore` normalized to LF
- `git init` + commits on `main`
- Optional symlink: `~/.hammerspoon/USER_GUIDE.html` → in-repo guide

## Audit findings → status

| ID | Severity | Status |
|----|----------|--------|
| AUDIT-001 | High | Mitigated — docs-only; no false runnable claims |
| AUDIT-002 | High | Fixed — one README identity |
| AUDIT-003 | High | Fixed — CLI Deferred |
| AUDIT-004 | High | Fixed — prerequisites + messaging + optional path |
| AUDIT-005 | Medium | Fixed — Git on `main` |
| AUDIT-006 | Medium | Fixed — ideas / stub badges |
| AUDIT-007 | Medium | Fixed — AGENTS ↔ spec layout |
| AUDIT-008 | Medium | Deferred — no CI until real code |
| AUDIT-009 | Medium | Fixed — Notes SQLite warning |
| AUDIT-010 | Low | Fixed — archived + provenance |
| AUDIT-011 | Low | Fixed — `fadeIn` keyframes |
| AUDIT-012 | Low | Deferred — `.env.example` with CLI |
| AUDIT-013 | Info | Fixed — Spencer PATH tip |
| AUDIT-014 | Info | Fixed — LF + folder rename |

## Still out of scope (by design)

- TypeScript CLI phase 1+, Vitest, GitHub Actions
- Rewriting all 50 cards into cloud CLI commands
- Rebuilding BlackDragon inside this repo
- Local Ollama as a first-class product provider

## How to use now

1. Browse `docs/apple_m4_ecosystem.html` (idea backlog).
2. Browse `docs/USER_GUIDE.html` with Hammerspoon installed for live actions.
3. Add real helpers under `scripts/` / `config/` when needed.
4. Start the CLI only with an explicit decision to leave “Deferred.”
