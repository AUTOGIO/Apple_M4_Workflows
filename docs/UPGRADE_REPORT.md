# Final upgrade report — Apple M4 Workflows

**Date:** 2026-07-29  
**Source:** Remediation of `REPOSITORY_AUDIT.md` (14 findings; 0 Critical)  
**Scope:** Docs / design hub only — CLI intentionally not started  
**Outcome:** All in-scope audit remediations complete; repo stable on `main` (`origin`: `AUTOGIO/Apple_M4_Workflows`).

---

## Verdict

The repo is no longer an ambiguous “approved CLI / incomplete product / Hammerspoon app” mix. It is a **personal automation hub and backlog**: browse HTML/Markdown here; live Hammerspoon stays on the host; the `m4` CLI stays **Deferred** until you explicitly start it.

---

## Decisions locked

| Question | Decision |
|----------|----------|
| Product identity | Docs + design backlog (not a runnable automation product) |
| CLI (`m4`) | Deferred — Approach 1 remains the future direction |
| BlackDragon / USER_GUIDE | Kept as Hammerspoon companion; prerequisites + optional project path |
| 50-card catalog | Ideas / stubs only — not shipped inventory |
| Empty `scripts/` / `config/` | Placeholders (`.gitkeep`); `config/layouts/` reserved for Spencer |
| Parent folder name | `Apple_M4_Workflows` (dropped `(NOT _START )`) |
| CLI home | This repo when started; no separate remote chosen yet |

---

## What changed (upgrades)

### Identity & docs
- README **Product / Status** — one answer to “what runs from this repo?”
- CLI design spec → **Deferred**; layout uses `config/layouts/` (not top-level `layouts/`)
- `AGENTS.md` aligned with deferred CLI and folder rules
- `docs/HAMMERSPOON.md` — host vs repo boundary
- `docs/external-links.md` — archived clipping + design pointers
- Audit §28 open questions answered; final recommendation marked done for docs-only scope

### HTML / UX
- Ecosystem: ideas framing, stub status badges, cloud-vs-local banner, `@keyframes fadeIn`
- Card 45: no raw Notes SQLite advice; safer Shortcuts/AppleScript path
- USER_GUIDE: Hammerspoon requirement banner, optional BlackDragon path, Spencer without forced sudo, clearer live-action toasts, AI tab labeled optional

### Hygiene & host
- MCP Shortcuts clip → `archive/` with provenance header
- `.gitignore` normalized to LF
- Git baseline on `main` + remote
- Symlink: `~/.hammerspoon/USER_GUIDE.html` → in-repo guide
- `config/layouts/.gitkeep` + Cursor/VS Code workspace file

---

## Audit findings → final status

| ID | Severity | Status |
|----|----------|--------|
| AUDIT-001 | High | Mitigated — docs-only; no false runnable claims |
| AUDIT-002 | High | Fixed — one README identity |
| AUDIT-003 | High | Fixed — CLI Deferred |
| AUDIT-004 | High | Fixed — prerequisites + messaging + optional path |
| AUDIT-005 | Medium | Fixed — Git on `main` |
| AUDIT-006 | Medium | Fixed — ideas / stub badges |
| AUDIT-007 | Medium | Fixed — AGENTS ↔ spec layout (`config/layouts/`) |
| AUDIT-008 | Medium | Deferred by design — no CI until real code |
| AUDIT-009 | Medium | Fixed — Notes SQLite warning removed |
| AUDIT-010 | Low | Fixed — archived + provenance |
| AUDIT-011 | Low | Fixed — `fadeIn` keyframes |
| AUDIT-012 | Low | Deferred by design — `.env.example` with CLI |
| AUDIT-013 | Info | Fixed — Spencer PATH tip (no forced sudo) |
| AUDIT-014 | Info | Fixed — LF + folder rename |

**In-scope:** 12 fixed/mitigated. **Out of scope by design:** 2 (CI, `.env.example`).

---

## Still deferred (do not start unless asked)

- TypeScript CLI phase 1+, Vitest, GitHub Actions
- Rewriting all 50 cards into cloud CLI commands
- Rebuilding BlackDragon inside this repo
- Local Ollama as a first-class product provider

---

## How to use now

1. Browse `docs/apple_m4_ecosystem.html` (idea backlog).
2. Browse `docs/USER_GUIDE.html` with Hammerspoon for live actions (optional symlink already set).
3. Add real helpers under `scripts/` / `config/` (layouts → `config/layouts/`) when needed.
4. Start the CLI only with an explicit decision to leave “Deferred.”

---

## Closing checklist (remaining actions — done)

- [x] Stages 0–4 remediation for docs-only scope
- [x] `config/layouts/` placeholder
- [x] CLI spec problem text no longer claims top-level `layouts/`
- [x] Audit unresolved questions answered
- [x] Workspace file present at repo root
- [x] Hammerspoon symlink verified
- [x] HTML parse smoke + LF `.gitignore` verified
