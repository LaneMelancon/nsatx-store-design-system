# NeuroSolution ATX Supplement Store — Design System

**Maintained By:** Lane Melancon — Onn Grid, LLC
**Client:** Dr. Brandon Crawford — NeuroSolution Center of Austin
**Last Updated:** 2026-06-29
**GitHub Repo:** `https://github.com/LaneMelancon/nsatx-store-design-system`
**Live Preview:** `https://lanemelancon.github.io/nsatx-store-design-system/`

---

## 1. Design Direction

The supplement store uses the NeuroSolution brand system as its foundation with a softer, more accessible treatment optimized for an eCommerce shopping context. The aesthetic is **Modern Professionalism** — prioritizing clarity, trust, and ease of navigation for patients.

### Philosophy

- **Light Mode First** — Clean, warm surfaces with white and platinum-range grays
- **Clean Minimalism** — Generous whitespace and a restricted palette keep products as the focal point
- **Warm Functionality** — Platinum grays and forest greens create a more inviting clinical space
- **Trust-Centric UI** — Stable grid structures and consistent typographic hierarchy reinforce professional-grade quality

### Relationship to Main NeuroSolution Brand

| Axis           | Supplement Store                                      | Main Clinic Site     |
| -------------- | ----------------------------------------------------- | -------------------- |
| Primary accent | Malachite green                                       | Lava red             |
| Backgrounds    | White and Platinum grays                              | Rich Black           |
| Typography     | Same Objective + Trade Gothic LT — softer application | Same family — bolder |
| Tone           | Clinical authority with retail warmth                 | Clinical evaluation  |

### Directory Structure

```
design-system/
├── CLAUDE.md               # This file — comprehensive documentation
├── index.html              # Main design system (editorial landing + component playground)
├── css/
│   ├── tokens.css          # Design tokens (colors, type, spacing, elevation)
│   ├── base.css            # Reset + typography fundamentals
│   ├── components.css      # All UI component styles (~1370 lines)
│   └── layout.css          # Grid, sections, playground shell
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

---

## 2. Color System

### 2.1 Base Brand Colors

| Name                  | Hex       | CSS Variable                              |
| --------------------- | --------- | ----------------------------------------- |
| Malachite             | `#0BDA51` | `--color-green-500` / `--color-primary-container` |
| Forest (UI workhorse) | `#0C8234` | `--color-green-700` / `--color-primary`   |
| White                 | `#FFFFFF` | `--color-white` / `--surface-lowest`      |
| Platinum              | `#F0EFEF` | `--color-gray-100`                        |
| Near Black            | `#131313` | `--color-gray-900`                        |

### 2.2 Malachite Green Scale

| Token       | Hex       | Usage                                                  |
| ----------- | --------- | ------------------------------------------------------ |
| `green-900` | `#101913` | Dark hero/footer surfaces, brand inverse backgrounds   |
| `green-800` | `#0D4A21` | Dark text/icon fills on light surfaces                 |
| `green-700` | `#0C8234` | AA-compliant green text on white (UI workhorse)        |
| `green-600` | `#0CB144` | Hover/active states                                    |
| `green-500` | `#0BDA51` | Base Malachite — brand buttons on dark bg only         |
| `green-400` | `#3CE174` | Focus rings, highlights                                |
| `green-300` | `#6DE997` | Subtle accents, focus rings                            |
| `green-200` | `#9DF0B9` | Light backgrounds, hover on dark                       |
| `green-100` | `#CEF8DC` | Success states, light fills                            |
| `green-50`  | `#E7FBEE` | Near-white tint, section backgrounds                   |

### 2.3 Gray Scale

| Token      | Hex       | Usage                                  |
| ---------- | --------- | -------------------------------------- |
| `gray-900` | `#131313` | Primary body text, near-black surfaces |
| `gray-800` | `#191919` | Dark backgrounds, footer               |
| `gray-700` | `#303030` | Dark text alternative, input labels    |
| `gray-600` | `#525252` | Secondary text, placeholders           |
| `gray-500` | `#747373` | Muted text, disabled states            |
| `gray-400` | `#969595` | Borders, dividers                      |
| `gray-300` | `#B8B7B7` | Light borders, input outlines          |
| `gray-200` | `#D9D8D8` | Light dividers                         |
| `gray-100` | `#F0EFEF` | Platinum — secondary backgrounds       |
| `gray-50`  | `#F9F9F9` | Lightest surface                       |

### 2.4 System Colors

System colors are **separate from brand colors** with a clear functional purpose. Each state has light and dark surface variants.

#### Success (references brand green scale)

| Token                   | Value                      | Usage                   |
| ----------------------- | -------------------------- | ----------------------- |
| `--sys-success-bg`      | `green-50`                 | Light surface background|
| `--sys-success-border`  | `green-100`                | Light surface border    |
| `--sys-success-text`    | `green-900`                | Light surface text      |
| `--sys-success-icon`    | `green-700`                | Light surface icon      |
| `--sys-success-bg-dark` | `rgba(11,218,81,0.08)`     | Dark surface background |
| `--sys-success-text-dark`| `green-200`               | Dark surface text       |
| `--sys-success-icon-dark`| `green-400`               | Dark surface icon       |

#### Info (Blue)

| Token                | Value                      | Usage                   |
| -------------------- | -------------------------- | ----------------------- |
| `--sys-info-bg`      | `#EFF6FF`                  | Light surface background|
| `--sys-info-border`  | `#BFDBFE`                  | Light surface border    |
| `--sys-info-text`    | `#1E3A5F`                  | Light surface text      |
| `--sys-info-icon`    | `#2563EB`                  | Light surface icon      |
| `--sys-info-bg-dark` | `rgba(37,99,235,0.08)`     | Dark surface background |
| `--sys-info-text-dark`| `#93C5FD`                 | Dark surface text       |

#### Warning (Amber)

| Token                   | Value                      | Usage                   |
| ----------------------- | -------------------------- | ----------------------- |
| `--sys-warning-bg`      | `#FFFBEB`                  | Light surface background|
| `--sys-warning-border`  | `#FDE68A`                  | Light surface border    |
| `--sys-warning-text`    | `#78350F`                  | Light surface text      |
| `--sys-warning-icon`    | `#D97706`                  | Light surface icon      |
| `--sys-warning-bg-dark` | `rgba(217,119,6,0.08)`     | Dark surface background |
| `--sys-warning-text-dark`| `#FDE68A`                 | Dark surface text       |

#### Error (Red)

| Token                 | Value                      | Usage                   |
| --------------------- | -------------------------- | ----------------------- |
| `--sys-error-bg`      | `#FFDAD6`                  | Light surface background|
| `--sys-error-border`  | `#FCA5A5`                  | Light surface border    |
| `--sys-error-text`    | `#7F1D1D`                  | Light surface text      |
| `--sys-error-icon`    | `#BA1A1A`                  | Light surface icon      |
| `--sys-error-bg-dark` | `rgba(186,26,26,0.12)`     | Dark surface background |
| `--sys-error-text-dark`| `#FCA5A5`                 | Dark surface text       |

### 2.5 Surface Colors

| Token                    | Hex       | Usage                               |
| ------------------------ | --------- | ----------------------------------- |
| `--surface-bg`           | `#FCF9F8` | Page background                     |
| `--surface-lowest`       | `#FFFFFF` | Cards, modals, product tiles        |
| `--surface-low`          | `#F6F3F2` | Hover states, meta sections         |
| `--surface-container`    | `#F0EDEC` | Secondary sections                  |
| `--surface-high`         | `#EBE7E7` | Elevated containers, cancel buttons |
| `--surface-highest`      | `#E5E2E1` | Max emphasis surfaces               |
| `--surface-inverse`      | `#313030` | Footer, tooltips, dark sections     |

### 2.6 Accessibility Rules

- `green-500` (`#0BDA51`) on white **fails** WCAG AA for normal text — never use as a text color on light backgrounds
- `green-700` (`#0C8234`) on white **passes** AA — safe for green text and interactive labels
- White text on `green-700` **passes** AA — safe for primary CTA buttons
- **WCAG AA compliance is required** throughout
- All text contrast must meet minimum 4.5:1 ratio

---

## 3. Typography

### 3.1 Font Stack

| Role                         | Font Family     | CSS Variable     |
| ---------------------------- | --------------- | ---------------- |
| Primary (headings, body, UI) | Objective       | `--font-primary` |
| Label / Eyebrow              | Trade Gothic LT | `--font-label`   |
| Monospace (code, tokens)     | SF Mono / Fira Code | `--font-mono` |

**Font Source:** jsDelivr CDN from `github.com/LaneMelancon/ns-atx-font-files`

Loaded weights: Objective 400, 500, 700 | Trade Gothic LT 400, 700

### 3.2 Heading Scale

| Token                | Font      | Weight       | Size | Line Height | Letter Spacing |
| -------------------- | --------- | ------------ | ---- | ----------- | -------------- |
| `headline-h1`        | Objective | Bold (700)   | 60px | 68px        | -1px           |
| `headline-h1-mobile` | Objective | Bold (700)   | 40px | 48px        | -1px           |
| `headline-h2`        | Objective | Bold (700)   | 44px | 54px        | -1px           |
| `headline-h2-mobile` | Objective | Bold (700)   | 32px | 40px        | -0.5px         |
| `headline-h3`        | Objective | Bold (700)   | 24px | 32px        | 0              |
| `headline-h4`        | Objective | Medium (500) | 18px | 24px        | 0              |
| `headline-h5`        | Objective | Medium (500) | 16px | 24px        | 0              |

### 3.3 Eyebrow / Label

| Token           | Font            | Weight     | Size | Line Height | Letter Spacing |
| --------------- | --------------- | ---------- | ---- | ----------- | -------------- |
| `label-eyebrow` | Trade Gothic LT | Bold (700) | 14px | 14px        | +1px           |

Always uppercase. Used for section headers, nav links, brand labels on product cards, badges. Never substitute Objective in this role.

### 3.4 Body Scale

All body text uses **Objective Regular (400)**, color `gray-900` (`#131313`) on light backgrounds.

| Token       | Size | Line Height | Usage                                   |
| ----------- | ---- | ----------- | --------------------------------------- |
| `text-lg`   | 18px | 28px        | Intro paragraphs, featured descriptions |
| `text-reg`  | 16px | 24px        | Standard body, product descriptions     |
| `text-sm`   | 14px | 21px        | Supporting text, secondary info, meta   |
| `text-tiny` | 12px | 18px        | Captions, fine print, timestamps        |

### 3.5 Weight Hierarchy

| Weight  | Value | Where Used                                                    |
| ------- | ----- | ------------------------------------------------------------- |
| Bold    | 700   | H1, H2, H3, eyebrow/label text, table headers                |
| Medium  | 500   | H4, H5, **button labels**, alert headings, toast headings, tags, chips, input labels |
| Regular | 400   | All body text, alert body, toast body                         |

---

## 4. Component System

### 4.1 Buttons

Architecture uses CSS custom properties + cascade. One `.btn` base reads `--btn-*` vars. Modifier classes set only the vars that differ.

**Button text always uses Objective Medium (500) — never Bold (700).**

**Context rules:**
- **Light backgrounds:** Use `.btn--primary` (green-700 bg, white text)
- **Dark/green-900 backgrounds:** Use `.btn--brand` (malachite bg, green-900 text)
- **Never** use `.btn--brand` on light backgrounds

**Class API:**

```
.btn                              — base (required)
.btn--sm | .btn--md | .btn--lg    — size
.btn--primary                     — green-700 solid (LIGHT backgrounds)
.btn--primary-outline             — green-900 outline (LIGHT backgrounds)
.btn--primary-text                — green-700 text only (LIGHT backgrounds)
.btn--brand                       — malachite solid (DARK backgrounds)
.btn--brand-outline               — white outline (DARK backgrounds)
.btn--brand-text                  — green-400 text only (DARK backgrounds)
.btn--default                     — gray-800 solid
.btn--cancel                      — neutral low-emphasis
.btn--delete                      — error red solid
.btn--delete-outline              — error red outline
.btn--outline                     — generic gray outline
.btn--text                        — generic text-only
.btn--icon                        — icon-only square button
```

**Size scale:**

| Size       | Font Size | Padding   | Border Radius |
| ---------- | --------- | --------- | ------------- |
| `.btn--sm` | 12px      | 7px 14px  | 8px           |
| `.btn--md` | 14px      | 10px 20px | 8px           |
| `.btn--lg` | 16px      | 14px 28px | 12px          |

**States:** hover, active (scale 0.97), focus-visible (3px green-300 ring), disabled (opacity 0.38)

### 4.2 Badges

Pill-shaped status indicators using Trade Gothic LT Bold, uppercase, 10px.

| Variant          | Background          | Text Color       |
| ---------------- | ------------------- | ---------------- |
| `.badge--success` | `sys-success-100`  | `green-800`      |
| `.badge--error`   | `sys-error-bg`     | `sys-error-text` |
| `.badge--warning` | `sys-warning-200`  | `sys-warning-800`|
| `.badge--info`    | `sys-info-200`     | `sys-info-800`   |
| `.badge--neutral` | `surface-high`     | `gray-600`       |
| `.badge--brand`   | `green-900`        | `green-400`      |
| `.badge--new`     | `green-50`         | `green-700`      |

### 4.3 Filter Chips

Interactive selectors using Objective Medium (500), 12px.

| State    | Background     | Text         | Border            |
| -------- | -------------- | ------------ | ----------------- |
| Default  | `surface-low`  | `gray-600`   | `outline-variant` |
| Hover    | `green-50`     | `green-800`  | `green-100`       |
| Active   | `green-500`    | `green-900`  | transparent       |

### 4.4 Tags

Product category labels using Objective Medium (500), 9px, uppercase.
Background: `green-50`, text: `green-700`, border: 1px solid `green-100`.

### 4.5 Form Inputs

- `.input-group` — container with `.input-label` + `.input`
- `.input` — full-width, 1px border, 10px 14px padding
- Focus: border-color primary, 3px green-300 ring
- `.input--error` — red border, red focus ring
- `.select` — with custom chevron SVG arrow
- `.textarea` — min-height 100px, vertical resize
- `.checkbox-group` / `.radio-group` — flex row with accent-color primary

### 4.6 Product Cards

- `.card` — white bg, 1px border, 16px radius, hover shadow + translateY(-2px)
- `.card-image` — 160px height, green-50 bg placeholder
- `.card-body` — 16px padding
- `.card-brand` — Trade Gothic LT 9px uppercase (eyebrow)
- `.card-title` — Objective Medium 14px
- `.card-price` — Objective Bold 16px, primary color
- `.card-price-compare` — strikethrough, gray-400
- `.card-tags` — flex row of `.tag` items
- `.card-actions` — flex row with buttons
- `.card-wishlist` — absolute positioned heart button
- `.card--wholesale` — 1.5px green-900 border, dark image area

### 4.7 Alerts

5 states with light and dark surface variants. Blue for info, amber for warning.

**Structure:** `.alert` > `.alert-icon` + div > `.alert-heading` + `.alert-text`

| Light Variant       | Background          | Text              | Icon              |
| ------------------- | ------------------- | ----------------- | ----------------- |
| `.alert--success`   | `sys-success-bg`    | `sys-success-text`| `sys-success-icon`|
| `.alert--info`      | `sys-info-bg`       | `sys-info-text`   | `sys-info-icon`   |
| `.alert--warning`   | `sys-warning-bg`    | `sys-warning-text`| `sys-warning-icon`|
| `.alert--error`     | `sys-error-bg`      | `sys-error-text`  | `sys-error-icon`  |
| `.alert--brand`     | `green-900`         | white             | `green-500`       |

Dark variants: append `-dark` (e.g., `.alert--success-dark`).

### 4.8 Toasts

Solid, inline notifications — smaller than alerts.

**Structure:** `.toast` > `.toast-icon` + `.toast-content` > `.toast-title` + `.toast-desc` + `.toast-close`

States: `.toast--success`, `.toast--info`, `.toast--warning`, `.toast--error`, `.toast--neutral`

Action variant: add `.toast-action` button inside toast.

### 4.9 Navigation

Two variants: `.nav--light` (white bg) and `.nav--dark` (green-900 bg).

- Logo: `.nav-logo-mark` (20px square malachite) + `.nav-logo-text` (Objective Bold 13px)
- Links: `.nav-link` — Trade Gothic LT Bold, 10px, uppercase
- Active: `.nav-link.is-active` — primary color
- Icons: `.nav-icon` — 32px touch target, 18px icon
- Cart badge: `.nav-cart-count` — 16px circle, malachite bg

### 4.10 Progress Bars

`.progress` > `.progress-label` + `.progress-track` > `.progress-fill`

Fill variants: default (primary), `.progress-fill--brand` (malachite), `.progress-fill--muted`

### 4.11 Tabs

`.tabs` > `.tab` items. Active: `.tab.is-active` — primary color with 2px bottom border.

### 4.12 Breadcrumbs

`.breadcrumbs` > `.breadcrumb-link` + `.breadcrumb-sep` + `.breadcrumb-current`

### 4.13 Pagination

`.pagination` > `.pagination-btn` items. Active: `.pagination-btn.is-active` — green-900 bg, white text.

### 4.14 Modal

`.modal-overlay` > `.modal` > `.modal-header` + `.modal-body` + `.modal-footer`

Modal header: title + close button. Footer: button row.

### 4.15 Dropdown

`.dropdown` > `.dropdown-menu` > `.dropdown-item` items + `.dropdown-divider`

### 4.16 Table

`.table` with `th` (uppercase, 2px bottom border) and `td`. Striped variant: `.table--striped`.

### 4.17 Accordion

`.accordion` > `.accordion-item` > `.accordion-trigger` + `.accordion-content`

Trigger has `aria-expanded` attribute; chevron rotates 180deg when expanded.

### 4.18 Tooltip

`.tooltip-wrapper` > trigger + `.tooltip` (absolutely positioned above).

### 4.19 Avatar

`.avatar` — 36px circle, green-50 bg, green-700 text. Sizes: `.avatar--sm` (28px), `.avatar--lg` (48px).

### 4.20 Skeleton Loader

`.skeleton` base with shimmer animation. Variants: `--text`, `--heading`, `--image`, `--circle`.

### 4.21 Empty State

`.empty-state` > `.empty-state-icon` + `.empty-state-title` + `.empty-state-desc`

### 4.22 Divider

`.divider` (1px) and `.divider--thick` (2px).

### 4.23 Step Indicator

`.steps` > `.step` + `.step-connector` items. States: `.step.is-active` (malachite), `.step.is-complete` (green-50 bg).

### 4.24 Quantity Selector

`.qty-selector` > `.qty-btn` (minus) + `.qty-value` + `.qty-btn` (plus)

### 4.25 Toggle / Switch

`.toggle` > `.toggle-track` > `.toggle-thumb` + `.toggle-label`. Active: `.toggle-track.is-active`.

### 4.26 Search Bar

`.search-bar` > search icon + input. Full border-radius, focus ring on `:focus-within`.

### 4.27 Order Summary / Line Items

`.line-item` > `.line-item-image` + `.line-item-info` > `.line-item-name` + `.line-item-meta` + `.line-item-price`

`.order-total` > `.order-total-label` + `.order-total-value`

---

## 5. Iconography

**Library:** Lucide Icons (inline SVG)
**Default size:** 16px for UI icons, 14px for small contexts
**Stroke width:** 2 (standard)

Common icons: search, shopping-cart, heart, package, circle-check, info, triangle-alert, x-circle, x, shield-check, lock, user, mail, credit-card, map-pin, truck, settings, log-out, eye, plus, minus, chevron-right, chevron-down, arrow-left, clipboard-list

**No emojis.** All icons are SVG-based.

---

## 6. Layout & Spacing

### Spacing Scale

| Token       | Value | Usage                    |
| ----------- | ----- | ------------------------ |
| `--space-1` | 4px   | Tight gaps               |
| `--space-2` | 8px   | Related element gaps     |
| `--space-3` | 12px  | Small padding            |
| `--space-4` | 16px  | Standard padding/gap     |
| `--space-6` | 24px  | Section padding, grids   |
| `--space-8` | 32px  | Large gaps               |
| `--space-12`| 48px  | Section padding          |
| `--space-16`| 64px  | Large section padding    |
| `--space-20`| 80px  | Hero vertical padding    |
| `--space-24`| 96px  | Hero vertical padding    |

### Border Radius Scale

| Token          | Value  | Usage                 |
| -------------- | ------ | --------------------- |
| `--rounded-sm` | 4px    | Small elements        |
| `--rounded`    | 8px    | Buttons, inputs       |
| `--rounded-md` | 12px   | Large buttons, alerts |
| `--rounded-lg` | 16px   | Cards, panels         |
| `--rounded-xl` | 24px   | Large containers      |
| `--rounded-full`| 9999px| Badges, chips, pills  |

### Elevation / Shadows

| Token         | Usage                          |
| ------------- | ------------------------------ |
| `--shadow-xs` | Subtle lift                    |
| `--shadow-sm` | Cards resting state            |
| `--shadow-md` | Cards hover, elevated panels   |
| `--shadow-lg` | Dropdowns, popovers            |
| `--shadow-xl` | Modals                         |

### Grid System

| Class     | Columns | Responsive                    |
| --------- | ------- | ----------------------------- |
| `.grid-2` | 2       | 1 col at 640px                |
| `.grid-3` | 3       | 2 col at 900px, 1 at 640px   |
| `.grid-4` | 4       | 2 col at 900px, 1 at 640px   |

### Containers

| Class             | Max Width |
| ----------------- | --------- |
| `.container`      | 1200px    |
| `.container--sm`  | 720px     |
| `.container--md`  | 960px     |
| `.container--lg`  | 1400px    |
| `.container--full`| none      |

### Z-Index Scale

| Token          | Value | Usage        |
| -------------- | ----- | ------------ |
| `--z-dropdown` | 10    | Menus        |
| `--z-sticky`   | 20    | Sticky header|
| `--z-fixed`    | 30    | Fixed sidebar|
| `--z-overlay`  | 40    | Overlays     |
| `--z-modal`    | 50    | Modals       |
| `--z-toast`    | 60    | Toasts       |
| `--z-tooltip`  | 70    | Tooltips     |

---

## 7. Transitions

| Token              | Value | Usage                        |
| ------------------ | ----- | ---------------------------- |
| `--duration-fast`  | 150ms | Hover, focus, micro-interactions |
| `--duration-normal`| 250ms | State changes, reveals       |
| `--duration-slow`  | 400ms | Progress bars, page transitions |
| `--ease-out`       | cubic-bezier(0.16, 1, 0.3, 1) | Natural deceleration |
| `--ease-in-out`    | cubic-bezier(0.65, 0, 0.35, 1) | Symmetric motion    |

`prefers-reduced-motion` is respected — animations and transitions reduce to near-zero.

---

## 8. Changelog
- Keep this markdown file up to date with changes or additions related to the Design System.

| Date       | Changes |
| ---------- | ------- |
| 2026-06-29 | Migrated to standalone GitHub repo (`nsatx-store-design-system`). Added GitHub Actions deploy workflow. Design system live at `https://lanemelancon.github.io/nsatx-store-design-system/`. Repo connected as submodule of `nsatx-store`. |
| 2026-06-18 | Updated BASE_DESIGN.md to reflect v2 architecture. Added system colors (info=blue, warning=amber, error=red). Added 17 new component docs. Updated button rules (weight 500, primary vs brand context). Updated green-900 to #101913, green-800 to #0D4A21. Added directory structure, spacing, transitions, z-index documentation. |
| 2026-06-17 | Multi-file architecture (tokens, base, components, layout CSS). 8 page demos created. Fonts via jsDelivr CDN. System color palette added. Alerts with blue info + amber warning. Toasts redesigned as solid inline. Button weight changed to 500. |
