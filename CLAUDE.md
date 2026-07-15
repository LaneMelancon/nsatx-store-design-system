# NeuroSolution ATX Supplement Store — Design System

**Maintained By:** Lane Melancon — Onn Grid, LLC **Client:** Dr. Brandon Crawford — NeuroSolution Center of Austin **Last Updated:** 2026-07-15 **GitHub Repo:** `https://github.com/LaneMelancon/nsatx-store-design-system` **Live Preview:** `https://lanemelancon.github.io/nsatx-store-design-system/`

---

## Read Next

- **`DESIGN.md`** — full design system reference: color tokens, typography, spacing, component specs, iconography. Read this before touching any CSS token, color, or component style.

---

## Directory Structure

The project is split into a **portable core** (`tokens.css`, `base.css` — safe to port directly into the Shopify theme) and **documentation-only chrome** (`layout.css`, `components/`, `playground.css`, the sidebar shell, section scaffolding) that must never leak into the portable core. `patterns.css` sits in between: composed, page-section-level patterns (hero, product grid, CTA band, etc.) built from the core tokens/components — the closest preview of actual Shopify section templates.

```
design-system/
├── CLAUDE.md               # (this file) – High-level overview
├── DESIGN.md               # Full design system reference (tokens, type, components)
├── index.html              # Landing page: philosophy + nav-out to the 3 docs pages
├── foundations.html        # Colors, typography, spacing, accessibility docs
├── components.html         # All ~27 component demos
├── patterns.html           # Storefront section pattern demos
├── css/
│   ├── tokens.css          # PORTABLE — design tokens (colors, type, spacing, elevation)
│   ├── base.css            # PORTABLE — reset + typography fundamentals
│   ├── layout.css          # DOC-ONLY – container/grid/flex utility primitives only
│   ├── components/         # DOC-ONLY – one file per component (buttons.css, cards.css, alerts.css, …)
│   ├── patterns.css        # composed storefront section patterns
│   └── playground.css      # DOC-ONLY – sidebar shell, pg-section/pg-scene scaffolding,
│                            #   color swatches, type specimens — never port this file
└── pages/
    ├── homepage.html       # Landing page demo
    ├── product-listing.html# Category / PLP demo
    ├── product-detail.html # PDP demo
    ├── cart.html            # Shopping cart demo
    ├── checkout.html        # Multi-step checkout demo
    ├── login.html           # Login / create account demo
    ├── order-confirmation.html # Order confirmed demo
    └── account.html         # Account dashboard demo
```

Every HTML page (index/foundations/components/patterns/pages/_) links `css/components/_.css`individually — no bundler, no`@import`— matching how Shopify's`theme.liquid`loads many small assets.`pages/\*.html`do **not** load`playground.css`; they're meant to look like real storefront pages, not documentation chrome.

---

## Rules

- All color, typography, spacing, and component specs live in `DESIGN.md` — keep that file in sync with `css/tokens.css` and `css/components/*.css` whenever either changes.
- Never let `playground.css` (documentation chrome) leak into the portable core files.
- Keep this file limited to structure and pointers — detailed specs belong in `DESIGN.md`.

---

## Changelog

| Date | Changes |
| --- | --- |
| 2026-07-15 | Split design specs out of `CLAUDE.md` into a dedicated `DESIGN.md`, rewritten to match the current `tokens.css` primitive/alias/dark-theme-override architecture (`--color-*` primitives; `--system-*`/`--brand-*`/`--surface-*`/`--text-*`/`--icon-*`/`--border-*` aliases; `[data-theme='dark']` overrides). `CLAUDE.md` now holds only directory structure and high-level pointers. |
| 2026-07-14 | Migrated `tokens.css` to the v2 alias architecture (semantic `--brand-*`/`--surface-*`/`--text-*`/`--icon-*`/`--border-*` tokens with `[data-theme='dark']` overrides); removed `tokens-v1.css`-era references from every CSS and HTML file. Split `components.css` into `css/components/*.css` (one file per component, linked individually — no bundler/`@import`). Split `layout.css` into true reusable primitives (containers/grid/flex) plus a new `playground.css` (documentation-only chrome) and `patterns.css` (reusable storefront section patterns: hero, product grid, features, testimonial, CTA band, newsletter, trust bar). Split `index.html` into `index.html` (landing), `foundations.html`, `components.html`, and `patterns.html`. Fixed the `.btn` base rule not consuming its own `--btn-*` modifier variables, collapsed the `.alert--*-dark` modifier classes in favor of `[data-theme='dark']`, and rebuilt the section-pattern demos to use real classes instead of inline styles. |
| 2026-06-29 | Migrated to standalone GitHub repo (`nsatx-store-design-system`). Added GitHub Actions deploy workflow. Design system live at `https://lanemelancon.github.io/nsatx-store-design-system/`. Repo connected as submodule of `nsatx-store`. |
| 2026-06-18 | Updated BASE_DESIGN.md to reflect v2 architecture. Added system colors (info=blue, warning=amber, error=red). Added 17 new component docs. Updated button rules (weight 500, primary vs brand context). Updated green-900 to #101913, green-800 to #0D4A21. Added directory structure, spacing, transitions, z-index documentation. |
| 2026-06-17 | Multi-file architecture (tokens, base, components, layout CSS). 8 page demos created. Fonts via jsDelivr CDN. System color palette added. Alerts with blue info + amber warning. Toasts redesigned as solid inline. Button weight changed to 500. |
