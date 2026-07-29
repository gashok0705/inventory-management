# Claude Code Workshop — Progress Tracker

> Read this first when resuming. It records exactly where we are in the 12-step
> Claude Code Workshop (Anthropic FDE Basecamp, July 2026). User: Raj (DXC).

## Project
Factory Inventory Management System — Vue 3 + Vite frontend (port 3000),
Python FastAPI backend (port 8001), in-memory JSON mock data.
Root: `/Users/rajagopalganesan/Desktop/bootcamp/Anthropic/inventory-management`

**IMPORTANT: Always operate from the project root above (not `server/data`).**
Earlier sessions launched from `server/data`, which broke `@` file mentions.

## Steps completed ✅
- **Step 1 — Fork & Clone**: Forked to `gashok0705/inventory-management`, cloned via HTTPS.
- **Step 2/3 — Install & Run**: Installed `uv` (brew), `uv venv && uv sync` for backend;
  `npm install` for frontend. Both servers verified (frontend :3000 = 200, backend :8001/docs).
- **Step 4 — CLAUDE.md**: Added coding convention under `## Coding Conventions`:
  "Always document non-obvious logic changes with comments".
- **Step 5 — Architecture page**: Created `docs/architecture.html` — theme-aware page with
  tech-stack cards, 4-layer diagram, 6-step data flow, endpoints table.
- **Step 6 — Build a Feature (Option B: SaaS UI Redesign)**:
  - Redesigned `client/src/App.vue`: top-nav → **left vertical sidebar**.
  - Added `<aside class="sidebar">` with brand glyph, 6 nav links each w/ inline SVG icon
    (grid, box, cart, dollar, trending-up, bar-chart) + label, `.sidebar-footer` docking
    LanguageSwitcher + ProfileMenu, and a `.app-body` right content column.
  - ~470 lines of new CSS: design tokens (slate palette, accent #2563eb), spacing scale,
    soft shadows, refreshed cards/tables/stat-tiles. Responsive: sidebar → 72px icon rail
    at max-width 900px.
  - **Zero logic changed** — `<script>` block byte-for-byte identical; all 6 routes,
    i18n `t()` labels, active-state logic, and modals preserved.
  - Also created a reusable skill: `.claude/skills/frontend-design/SKILL.md`.
  - KNOWN OPEN ITEM: Profile/Language dropdowns open downward (top:100%); docked at sidebar
    bottom they may spill past the viewport. Fix needs editing those child components
    (out of App.vue-only scope). Not yet done.
- **Step 7 — Context Management**: Demonstrated `/context`, `/compact`, and
  `/compact <instruction>`. Done.
- **Step 8 — Add Playwright MCP**: Ran `claude mcp add playwright npx @playwright/mcp@latest`.
  Added to local config. REQUIRES RESTART to activate the `mcp__playwright__*` tools.
- **Step 9 — Use Playwright MCP to Test**: Started both servers, navigated to :3000,
  screenshotted the dashboard, and clicked through all 6 nav tabs — every route loads and
  renders (no regressions from the Step 6 sidebar redesign). Caught and fixed 2 bugs found
  while testing:
  1. Demand Forecast showed `++50.0%` (doubled sign) — `Demand.vue` template hardcoded a
     `+` on top of `getChangePercent()`'s own sign. Removed the stray `+`.
  2. `GET /api/tasks` 404 on every page load — the Vue Tasks feature had no backend. Added
     `Task`/`CreateTaskRequest` models + GET/POST/PATCH/DELETE endpoints in `server/main.py`
     (in-memory store, API ids start at 1000 to avoid colliding with mock task ids 1-4).
  Re-verified: dashboard now loads with 0 console errors; full Tasks create round-trip
  persists to the backend. (The Profile/Language dropdown viewport-spill hit during testing
  is the Step 6 KNOWN OPEN ITEM, not a new regression.)

## Next up ▶
- **Step 10 — Connect Claude Code to GitHub** (GitHub MCP / `gh` auth).
- **Step 11 — Commit, Push & Open a PR** (use GitHub MCP per CLAUDE.md).
- **Step 12 — Advanced Workflows**.
- **Expert Challenge — Bug Bounty**: Fix the Reports Page.

## Deferred (not part of workshop)
Hayley's 3 AI agent demos (Documentation agent, Ad Ops automation, Personalization).
Explicitly postponed until after the workshop.
