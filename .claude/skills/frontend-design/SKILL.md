---
name: frontend-design
description: Redesign a Vue 3 (or similar SPA) UI into a modern, professional SaaS-style interface — left vertical sidebar navigation, clean card layouts, consistent spacing, and a polished aesthetic. Use when asked to modernize, restyle, or "make it look like a SaaS product," or to convert a top-nav layout to a sidebar layout.
---

# Frontend Design — Modern SaaS Redesign

A reusable recipe for transforming a plain SPA into a polished, professional SaaS-style
interface. Framework-agnostic in principle; examples target Vue 3 + Composition API.

## When to use
- "Redesign this app into a modern SaaS look"
- "Move the top nav into a left sidebar"
- "Make the UI more professional / polished"
- Any request to restyle an existing app without changing its functionality

## Core layout — left sidebar shell
Replace top navigation with a persistent **left vertical sidebar**:

```
┌────────────┬─────────────────────────────┐
│  LOGO      │  (optional) filter/toolbar   │
│            ├─────────────────────────────┤
│  ▣ Nav 1   │                             │
│  📦 Nav 2  │      main content            │
│  🛒 Nav 3  │      (router-view)           │
│  📊 Nav 4  │                             │
│            │                             │
│  ─────────  │                             │
│  user/lang │                             │
└────────────┴─────────────────────────────┘
```

- Sidebar width: **240px** expanded, **64px** collapsed (icons-only).
- Each nav item = **icon + label**, clear active state (accent background + left accent bar).
- Dock secondary controls (profile, language, settings) at the **bottom** of the sidebar.
- Main content area flexes to fill remaining width; keep an inner max-width for readability.

## Design tokens (adapt to the project's existing palette first)
Before inventing colors, read the app's current stylesheet and reuse its palette.
Sensible professional defaults (slate) if none exists:

| Token | Value |
|-------|-------|
| Background | `#f8fafc` |
| Surface / card | `#ffffff` |
| Ink (text) | `#0f172a` |
| Muted text | `#64748b` |
| Border | `#e2e8f0` |
| Accent | `#2563eb` |
| Accent soft (active bg) | `#eff6ff` |
| Status | green `#059669` · amber `#d97706` · red `#dc2626` |

**Spacing scale:** 4 / 8 / 12 / 16 / 24 / 32 px. Use consistently — no arbitrary values.
**Radius:** 10–14px on cards, 6–8px on chips/buttons.
**Shadow:** soft, layered — e.g. `0 1px 2px rgba(15,23,42,.06), 0 8px 24px rgba(15,23,42,.06)`.

## Component styling rules
- **Cards:** surface bg, 1px border, soft shadow, ~20px padding, subtle hover (lift/border).
- **Stat tiles:** uppercase muted label + large bold value; color the value by status.
- **Tables:** muted uppercase header row on a tinted background; row hover; generous cell padding.
- **Buttons:** solid accent for primary, outline/ghost for secondary; consistent height & radius.
- **Typography:** one sans stack; clear size hierarchy (page title → card title → body → caption).

## Hard rules
1. **Never change functionality.** Preserve every route, prop, event, composable, and modal.
   Only the presentation layer changes.
2. **No new dependencies** unless explicitly approved. Use inline SVG for icons, not an icon lib.
3. **Respect the project's design system** (check `CLAUDE.md`) — e.g. "no emojis in UI",
   specific colors, unique v-for keys.
4. **Delegate `.vue` edits** to the `vue-expert` subagent when the project's CLAUDE.md requires it.
5. **Keep it responsive** — sidebar collapses to icons-only (or a drawer) on narrow screens.

## Recommended process
1. Read the app shell (e.g. `App.vue`) and global styles to learn the current palette & structure.
2. Restructure the shell into the sidebar layout, keeping all existing child components wired.
3. Refresh global component styles (cards, tables, stat tiles) against the tokens above.
4. Add a collapse toggle + icons-only compact mode.
5. Verify in the browser at the dev URL; check each route still works.

## Definition of done
- Left sidebar with icon+label nav and a clear active state.
- Polished cards, tables, and stat tiles with consistent spacing.
- All routes and interactive features work exactly as before.
- Responsive: usable at narrow widths (collapsed sidebar).
