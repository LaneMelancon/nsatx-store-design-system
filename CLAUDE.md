# NeuroSolution ATX Supplement Store — Design System

**Maintained By:** Lane Melancon — Onn Grid, LLC **Client:** Dr. Brandon Crawford — NeuroSolution Center of Austin **Last Updated:** 2026-07-15 **GitHub Repo:** `https://github.com/LaneMelancon/nsatx-store-design-system`

---

## Read Next

- **`DESIGN.md`** — full design system reference: color tokens, typography, spacing. Read this before touching any CSS token or color.

---

## Directory Structure

The design system has been simplified down to portable tokens and base styles only — no documentation site, component library, or page demos.

```
design-system/
├── CLAUDE.md               # (this file) – High-level overview
├── DESIGN.md               # Full design system reference (tokens, type, spacing)
├── css/
│   ├── tokens.css          # PORTABLE — design tokens (color primitives/aliases, type, spacing, elevation, z-index)
│   ├── base.css             # PORTABLE — reset + typography fundamentals
│   └── fonts.css            # PORTABLE — @font-face declarations (Objective, Trade Gothic LT)
└── fonts/                   # Objective + Trade Gothic LT woff2 files referenced by fonts.css
```

All three CSS files are portable and meant to be dropped directly into the Shopify theme as-is.

---

## Rules

- All color, typography, and spacing specs live in `DESIGN.md` — keep that file in sync with `css/tokens.css` whenever it changes.
- `tokens.css` uses a primitive → alias architecture (`--color-*` primitives; `--system-*`/`--brand-*`/`--surface-*`/`--text-*`/`--icon-*`/`--border-*` aliases). There is currently no dark theme — no `[data-theme='dark']` overrides.
- Keep this file limited to structure and pointers — detailed specs belong in `DESIGN.md`.

---

## Changelog

| Date | Changes |
| --- | --- |
| 2026-07-15 | Simplified design system down to `tokens.css`, `base.css`, and `fonts.css` only — removed the documentation site (`index.html`, `foundations.html`, `components.html`, `patterns.html`), page demos (`pages/`), component/pattern/layout/playground CSS, and dark theme overrides. Updated and pruned tokens in `tokens.css`. |
| 2026-07-14 | Migrated `tokens.css` to the v2 alias architecture (semantic `--brand-*`/`--surface-*`/`--text-*`/`--icon-*`/`--border-*` tokens with `[data-theme='dark']` overrides); removed `tokens-v1.css`-era references from every CSS and HTML file. Split `components.css` into `css/components/*.css` (one file per component, linked individually — no bundler/`@import`). Split `layout.css` into true reusable primitives (containers/grid/flex) plus a new `playground.css` (documentation-only chrome) and `patterns.css` (reusable storefront section patterns: hero, product grid, features, testimonial, CTA band, newsletter, trust bar). Split `index.html` into `index.html` (landing), `foundations.html`, `components.html`, and `patterns.html`. Fixed the `.btn` base rule not consuming its own `--btn-*` modifier variables, collapsed the `.alert--*-dark` modifier classes in favor of `[data-theme='dark']`, and rebuilt the section-pattern demos to use real classes instead of inline styles. |
| 2026-06-29 | Migrated to standalone GitHub repo (`nsatx-store-design-system`). Added GitHub Actions deploy workflow. Design system live at `https://lanemelancon.github.io/nsatx-store-design-system/`. Repo connected as submodule of `nsatx-store`. |
| 2026-06-18 | Updated BASE_DESIGN.md to reflect v2 architecture. Added system colors (info=blue, warning=amber, error=red). Added 17 new component docs. Updated button rules (weight 500, primary vs brand context). Updated green-900 to #101913, green-800 to #0D4A21. Added directory structure, spacing, transitions, z-index documentation. |
| 2026-06-17 | Multi-file architecture (tokens, base, components, layout CSS). 8 page demos created. Fonts via jsDelivr CDN. System color palette added. Alerts with blue info + amber warning. Toasts redesigned as solid inline. Button weight changed to 500. |
