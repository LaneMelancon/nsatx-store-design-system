# NeuroSolution ATX Supplement Store — Design System Reference

**Maintained By:** Lane Melancon — Onn Grid, LLC
**Client:** Dr. Brandon Crawford — NeuroSolution Center of Austin
**Last Updated:** 2026-07-15

---

## 1. Design Direction

The supplement store uses the NeuroSolution brand system as its foundation with a softer, more accessible treatment optimized for an eCommerce shopping context. The aesthetic is **Modern Professionalism** — prioritizing clarity, trust, and ease of navigation for patients.

### Philosophy

- **Light Mode First** — Clean, warm surfaces with white and neutral-range grays
- **Clean Minimalism** — Generous whitespace and a restricted palette keep products as the focal point
- **Warm Functionality** — Neutral grays and forest greens create a more inviting clinical space
- **Trust-Centric UI** — Stable grid structures and consistent typographic hierarchy reinforce professional-grade quality

### Relationship to Main NeuroSolution Brand

| Axis           | Supplement Store                                      | Main Clinic Site     |
| -------------- | ----------------------------------------------------- | -------------------- |
| Primary accent | Malachite green                                       | Lava red             |
| Backgrounds    | White and neutral grays                                | Rich Black            |
| Typography     | Same Objective + Trade Gothic LT — softer application | Same family — bolder |
| Tone           | Clinical authority with retail warmth                 | Clinical evaluation  |

---

## 2. Token Architecture (`tokens.css`)

`tokens.css` is a three-layer system: **primitives** → **aliases** → **dark-theme overrides**. Only alias tokens (or component-level tokens built on aliases) should be consumed by component/page CSS — primitives (`--color-*`) should not be referenced directly outside of `tokens.css`.

1. **Color primitives** — raw hex ramps (`--color-green-900`…`--color-green-025`, plus `blue`, `orange`, `red`, `neutral`, each 025–900) and `--color-white` / `--color-black`.
2. **Color aliases** — semantic tokens (`--system-*`, `--brand-*`, `--surface-*`, `--text-*`, `--icon-*`, `--border-*`) that reference primitives. These flip automatically under `[data-theme='dark']`.
3. **Typography, radius, elevation, transitions, z-index, spacing** — non-color scales, theme-independent.

### 2.1 Color Primitives

| Ramp      | Steps                                  | Notes                              |
| --------- | --------------------------------------- | ----------------------------------- |
| `green`   | 025, 050, 100–900                       | Brand ramp (malachite → near-black) |
| `blue`    | 025, 050, 100–900                       | Info system color                   |
| `orange`  | 025, 050, 100–900                       | Warning system color                 |
| `red`     | 025, 050, 100–900                       | Error system color                   |
| `neutral` | 025, 050, 100–950                       | Grays, includes a 950 dark step      |

Key green steps: `--color-green-700` (`#0C8234`, AA-compliant text/UI workhorse), `--color-green-500` (`#0BDA51`, base Malachite — dark-background buttons only), `--color-green-900` (`#0E2415`, deep brand background).

### 2.2 Color Aliases (Light Theme Default)

#### System
| Token | Value | Usage |
| ----- | ----- | ----- |
| `--system-default` | `color-black` | Default ink |
| `--system-default-hover` | `rgba(14,14,14,0.15)` | Hover overlay |
| `--system-alt` | `color-white` | Inverse ink |
| `--system-subtle` | `rgba(14,14,14,0.05)` | Subtle fill/surface-low |
| `--system-subtle-alt` | `rgba(14,14,14,0.85)` | Strong subtle overlay |
| `--system-disabled` | `rgba(14,14,14,0.65)` | Disabled state |

#### Brand
| Token | Value | Usage |
| ----- | ----- | ----- |
| `--brand-default` | `green-900` | Primary brand surface/ink |
| `--brand-alt` | `color-white` | Inverse brand surface |
| `--brand-accent` | `green-500` | Malachite accent (dark bg only) |
| `--brand-accent-alt` | `green-700` | AA-safe green accent (light bg) |
| `--brand-primary` | `green-700` | Primary CTA color |
| `--brand-primary-alt` | `green-200` | Light primary variant |
| `--brand-secondary` | `orange-025` | Secondary warm tint |
| `--brand-secondary-alt` | `green-025` | Secondary green tint |
| `--brand-subtle` | `green-050` | Subtle brand fill |
| `--brand-subtle-alt` | `green-100` | Subtle brand fill, stronger |

#### Surface (brand + system state)
| Token | Value |
| ----- | ----- |
| `--surface-brand-default` | `brand-alt` |
| `--surface-brand-alt` | `brand-default` |
| `--surface-brand-secondary` | `brand-secondary` |
| `--surface-brand-subtle` | `system-subtle` |
| `--surface-success-default` | `green-700` |
| `--surface-success-default-hover` | `green-200` |
| `--surface-success-subtle` | `green-050` |
| `--surface-info-default` | `blue-600` |
| `--surface-info-default-hover` | `blue-200` |
| `--surface-info-subtle` | `blue-050` |
| `--surface-warning-default` | `orange-600` |
| `--surface-warning-default-hover` | `orange-200` |
| `--surface-warning-subtle` | `orange-050` |
| `--surface-error-default` | `red-600` |
| `--surface-error-default-hover` | `red-200` |
| `--surface-error-subtle` | `red-050` |

#### Text
| Token | Value |
| ----- | ----- |
| `--text-brand-default` / `--text-brand-heading` | `brand-default` |
| `--text-brand-body` | `neutral-800` |
| `--text-brand-caption` | `neutral-700` |
| `--text-brand-accent` | `brand-accent-alt` |
| `--text-brand-alt` | `brand-alt` |
| `--text-success-default` | `green-700` |
| `--text-success-subtle` | `neutral-800` |
| `--text-success-on-color` | `green-025` |
| `--text-info-default` | `blue-600` |
| `--text-warning-default` | `orange-600` |
| `--text-error-default` | `red-600` |
| (each state also has `-subtle`, `-on-color`, `-on-color-hover` variants) | |

#### Icon
| Token | Value |
| ----- | ----- |
| `--icon-brand-default` | `brand-default` |
| `--icon-brand-accent` | `brand-accent-alt` |
| `--icon-success-default` | `green-600` |
| `--icon-info-default` | `blue-500` |
| `--icon-warning-default` | `orange-500` |
| `--icon-error-default` | `red-500` |

#### Border
| Token | Value |
| ----- | ----- |
| `--border-brand-default` | `brand-default` |
| `--border-brand-subtle` | `system-subtle` |
| `--border-brand-accent` | `brand-accent-alt` |
| `--border-success-default` / `-subtle` | `green-700` / `green-100` |
| `--border-info-default` / `-subtle` | `blue-500` / `blue-100` |
| `--border-warning-default` / `-subtle` | `orange-500` / `orange-100` |
| `--border-error-default` / `-subtle` | `red-500` / `red-100` |

#### Surface Elevation
| Token | Value | Usage |
| ----- | ----- | ----- |
| `--surface-lowest` | `surface-brand-default` (white) | Cards, modals, product tiles |
| `--surface-low` | `system-subtle` | Hover states, meta sections |
| `--surface-high` | `neutral-100` | Elevated containers, cancel buttons |
| `--surface-highest` | `neutral-200` | Max emphasis surfaces |
| `--surface-inverse` | `neutral-900` | Footer, tooltips, dark sections |
| `--surface-on-variant` | `neutral-600` | Muted text on surfaces |
| `--surface-outline` | `neutral-300` | Default borders |
| `--surface-outline-variant` | `border-brand-subtle` | Subtle borders |

### 2.3 Dark Theme (`[data-theme='dark']`)

Overriding the alias layer flips the whole system — component CSS never needs `[data-theme]` selectors of its own. Notable flips: `--brand-default` → `orange-025`, `--brand-alt` → `green-900`, `--brand-accent-alt` → `green-400`, all `-subtle` surface/text/border tokens shift to their `800`/`900` ramp steps, and elevation surfaces (`--surface-high`, `--surface-highest`, `--surface-outline`) shift to `neutral-700`/`800`.

### 2.4 Accessibility Rules

- `green-500` (`#0BDA51`) on white **fails** WCAG AA for normal text — never use as a text color on light backgrounds
- `green-700` (`#0C8234`) on white **passes** AA — safe for green text and interactive labels
- White text on `green-700` **passes** AA — safe for primary CTA buttons
- **WCAG AA compliance is required** throughout; all text contrast must meet minimum 4.5:1 ratio

---

## 3. Typography

### 3.1 Font Stack

| Role | Font Family | CSS Variable |
| ---- | ----------- | ------------ |
| Primary (headings, body, UI) | Objective | `--font-primary` |
| Secondary (Eyebrow, nav links, footer headings) | Trade Gothic LT | `--font-secondary` |
| Monospace (code, tokens) | SF Mono / Fira Code | `--font-mono` |

**Font Source:** jsDelivr CDN from `github.com/LaneMelancon/ns-atx-font-files`
Loaded weights: Objective 400, 500, 700 | Trade Gothic LT 400, 700

Rule: Default body copy uses Objective Regular (400). Buttons use Objective Medium (500). Trade Gothic is reserved for eyebrows, desktop navbar links, and desktop footer column headings.

### 3.2 Size Scale

| Token | rem | Usage |
| ----- | --- | ----- |
| `--text-h1` | 3.625rem | H1 desktop |
| `--text-h1-mob` | 2.5rem | H1 mobile |
| `--text-h2` | 2.25rem | H2 desktop |
| `--text-h2-mob` | 2rem | H2 mobile |
| `--text-h3` | 1.5rem | H3 |
| `--text-h4` | 1.125rem | H4 |
| `--text-h5` | 1rem | H5 |
| `--text-eyebrow` | 0.75rem | Eyebrow/label |
| `--text-2xs` | 0.625rem | Micro captions |
| `--text-xs` | 0.75rem | Fine print |
| `--text-sm` | 0.875rem | Supporting/meta text |
| `--text-reg` | 1rem | Standard body |
| `--text-md` | 1.125rem | Emphasized body |
| `--text-lg` | 1.25rem | Intro paragraphs |

### 3.3 Line Height & Letter Spacing

| Token | Value |
| ----- | ----- |
| `--leading-h1` / `--leading-h1-mob` | 1.1 |
| `--leading-h2` / `--leading-h2-mob` | 1.15 |
| `--leading-h3` | 1.25 |
| `--leading-h4` | 1.3 |
| `--leading-h5` | 1.4 |
| `--leading-eyebrow` | 1 |
| `--leading-2xs` | 1 |
| `--leading-xs` | 1.1 |
| `--leading-sm` | 1.15 |
| `--leading-reg` | 1.5 |
| `--leading-md` | 1.55 |
| `--leading-lg` | 1.65 |
| `--tracking-h1` / `--tracking-h2` / `--tracking-h2-mob` | -0.0625rem |
| `--tracking-eyebrow` | 0.125rem |

### 3.4 Font Weights

| Token | Value | Where Used |
| ----- | ----- | ---------- |
| `--font-light` | 300 | Rare, decorative only |
| `--font-normal` | 400 | Body text |
| `--font-medium` | 500 | H4, H5, button labels, alert/toast headings, tags, chips, input labels |
| `--font-bold` | 700 | H1, H2, H3, eyebrow/label text, table headers |
| `--font-extrabold` | 800 | Rare emphasis |

---

## 4. Spacing

Spacing uses a `--space()` custom function on a 0.25rem (4px) base increment: `calc(var(--space-base) * multiplier)`.

| Token | Multiplier | Value |
| ----- | ---------- | ----- |
| `--space-none` | 0 | 0rem |
| `--space-4xs` | 0.25 | 0.0625rem (1px) |
| `--space-3xs` | 0.5 | 0.125rem (2px) |
| `--space-2xs` | 0.75 | 0.1875rem (3px) |
| `--space-xs` | 1 | 0.25rem (4px) |
| `--space-sm` | 2 | 0.5rem (8px) |
| `--space-reg` | 4 | 1rem (16px) |
| `--space-md` | 6 | 1.5rem (24px) |
| `--space-lg` | 8 | 2rem (32px) |
| `--space-xl` | 12 | 3rem (48px) |
| `--space-2xl` | 16 | 4rem (64px) |
| `--space-3xl` | 22 | 5.5rem (88px) |
| `--space-4xl` | 26 | 6.5rem (104px) |

---

## 5. Border Radius

| Token | Value | Usage |
| ----- | ----- | ----- |
| `--rounded-sm` | 0.25rem | Small elements |
| `--rounded` | 0.5rem | Buttons, inputs |
| `--rounded-md` | 0.75rem | Large buttons, alerts |
| `--rounded-lg` | 1rem | Cards, panels |
| `--rounded-xl` | 1.5rem | Large containers |
| `--rounded-full` | 50vw | Badges, chips, pills |

---

## 6. Elevation / Shadows

| Token | Usage |
| ----- | ----- |
| `--shadow-xs` | Subtle lift |
| `--shadow-sm` | Cards resting state |
| `--shadow-md` | Cards hover, elevated panels |
| `--shadow-lg` | Dropdowns, popovers |
| `--shadow-xl` | Modals |
| `--shadow-toast` | Toasts |

All shadow colors use a green-tinted black (`rgba(14, 36, 21, …)`) rather than pure black, to match the brand's cool-green neutral tone.

---

## 7. Transitions

| Token | Value | Usage |
| ----- | ----- | ----- |
| `--duration-fast` | 150ms | Hover, focus, micro-interactions |
| `--duration-normal` | 250ms | State changes, reveals |
| `--duration-slow` | 400ms | Progress bars, page transitions |
| `--ease-out` | `cubic-bezier(0.16, 1, 0.3, 1)` | Natural deceleration |
| `--ease-in-out` | `cubic-bezier(0.65, 0, 0.35, 1)` | Symmetric motion |

`prefers-reduced-motion` is respected — animations and transitions reduce to near-zero.

---

## 8. Z-Index Scale

| Token | Value | Usage |
| ----- | ----- | ----- |
| `--z-base` | 0 | Default stacking |
| `--z-dropdown` | 10 | Menus |
| `--z-sticky` | 20 | Sticky header |
| `--z-fixed` | 30 | Fixed sidebar |
| `--z-overlay` | 40 | Overlays |
| `--z-modal` | 50 | Modals |
| `--z-toast` | 60 | Toasts |
| `--z-tooltip` | 70 | Tooltips |

---

## 9. Component System

### 9.1 Buttons

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

| Size | Font Size | Padding | Border Radius |
| ---- | --------- | ------- | -------------- |
| `.btn--sm` | 12px | 7px 14px | 8px |
| `.btn--md` | 14px | 10px 20px | 8px |
| `.btn--lg` | 16px | 14px 28px | 12px |

**States:** hover, active (scale 0.97), focus-visible (3px ring), disabled (opacity 0.38)

### 9.2 Badges

Pill-shaped status indicators using Trade Gothic LT Bold, uppercase, 10px.

| Variant | Background | Text Color |
| ------- | ---------- | ---------- |
| `.badge--success` | success-subtle surface | success text |
| `.badge--error` | error-subtle surface | error text |
| `.badge--warning` | warning-subtle surface | warning text |
| `.badge--info` | info-subtle surface | info text |
| `.badge--neutral` | `surface-high` | `surface-on-variant` |
| `.badge--brand` | `brand-default` | `brand-accent` |
| `.badge--new` | `brand-subtle` | `brand-accent-alt` |

### 9.3 Filter Chips

Interactive selectors using Objective Medium (500), 12px.

| State | Background | Text | Border |
| ----- | ---------- | ---- | ------ |
| Default | `surface-low` | `surface-on-variant` | `surface-outline-variant` |
| Hover | `brand-subtle` | `brand-accent-alt` | `brand-subtle-alt` |
| Active | `brand-accent` | `brand-default` | transparent |

### 9.4 Tags

Product category labels using Objective Medium (500), 9px, uppercase. Background: `brand-subtle`, text: `brand-accent-alt`, border: 1px solid `brand-subtle-alt`.

### 9.5 Form Inputs

- `.input-group` — container with `.input-label` + `.input`
- `.input` — full-width, 1px border, 10px 14px padding
- Focus: border-color `brand-primary`, 3px ring
- `.input--error` — error border, error focus ring
- `.select` — with custom chevron SVG arrow
- `.textarea` — min-height 100px, vertical resize
- `.checkbox-group` / `.radio-group` — flex row with accent-color primary

### 9.6 Product Cards

- `.card` — white bg, 1px border, 16px radius, hover shadow + translateY(-2px)
- `.card-image` — 160px height, brand-subtle bg placeholder
- `.card-body` — 16px padding
- `.card-brand` — Trade Gothic LT 9px uppercase (eyebrow)
- `.card-title` — Objective Medium 14px
- `.card-price` — Objective Bold 16px, primary color
- `.card-price-compare` — strikethrough, muted gray
- `.card-tags` — flex row of `.tag` items
- `.card-actions` — flex row with buttons
- `.card-wishlist` — absolute positioned heart button
- `.card--wholesale` — 1.5px `brand-default` border, dark image area

### 9.7 Alerts

5 states, theme-aware via `[data-theme='dark']` alias flips (no separate `-dark` modifier classes needed).

**Structure:** `.alert` > `.alert-icon` + div > `.alert-heading` + `.alert-text`

| Variant | Background | Text | Icon |
| ------- | ---------- | ---- | ---- |
| `.alert--success` | success-subtle surface | success text | success icon |
| `.alert--info` | info-subtle surface | info text | info icon |
| `.alert--warning` | warning-subtle surface | warning text | warning icon |
| `.alert--error` | error-subtle surface | error text | error icon |
| `.alert--brand` | `brand-default` | `brand-alt` | `brand-accent` |

### 9.8 Toasts

Solid, inline notifications — smaller than alerts.

**Structure:** `.toast` > `.toast-icon` + `.toast-content` > `.toast-title` + `.toast-desc` + `.toast-close`

States: `.toast--success`, `.toast--info`, `.toast--warning`, `.toast--error`, `.toast--neutral`

Action variant: add `.toast-action` button inside toast.

### 9.9 Navigation

Two variants: `.nav--light` (white bg) and `.nav--dark` (brand-default bg).

- Logo: `.nav-logo-mark` (20px square malachite) + `.nav-logo-text` (Objective Bold 13px)
- Links: `.nav-link` — Trade Gothic LT Bold, 10px, uppercase
- Active: `.nav-link.is-active` — primary color
- Icons: `.nav-icon` — 32px touch target, 18px icon
- Cart badge: `.nav-cart-count` — 16px circle, malachite bg

### 9.10 Progress Bars

`.progress` > `.progress-label` + `.progress-track` > `.progress-fill`

Fill variants: default (primary), `.progress-fill--brand` (malachite), `.progress-fill--muted`

### 9.11 Tabs

`.tabs` > `.tab` items. Active: `.tab.is-active` — primary color with 2px bottom border.

### 9.12 Breadcrumbs

`.breadcrumbs` > `.breadcrumb-link` + `.breadcrumb-sep` + `.breadcrumb-current`

### 9.13 Pagination

`.pagination` > `.pagination-btn` items. Active: `.pagination-btn.is-active` — `brand-default` bg, white text.

### 9.14 Modal

`.modal-overlay` > `.modal` > `.modal-header` + `.modal-body` + `.modal-footer`

Modal header: title + close button. Footer: button row.

### 9.15 Dropdown

`.dropdown` > `.dropdown-menu` > `.dropdown-item` items + `.dropdown-divider`

### 9.16 Table

`.table` with `th` (uppercase, 2px bottom border) and `td`. Striped variant: `.table--striped`.

### 9.17 Accordion

`.accordion` > `.accordion-item` > `.accordion-trigger` + `.accordion-content`

Trigger has `aria-expanded` attribute; chevron rotates 180deg when expanded.

### 9.18 Tooltip

`.tooltip-wrapper` > trigger + `.tooltip` (absolutely positioned above).

### 9.19 Avatar

`.avatar` — 36px circle, brand-subtle bg, brand-accent-alt text. Sizes: `.avatar--sm` (28px), `.avatar--lg` (48px).

### 9.20 Skeleton Loader

`.skeleton` base with shimmer animation. Variants: `--text`, `--heading`, `--image`, `--circle`.

### 9.21 Empty State

`.empty-state` > `.empty-state-icon` + `.empty-state-title` + `.empty-state-desc`

### 9.22 Divider

`.divider` (1px) and `.divider--thick` (2px).

### 9.23 Step Indicator

`.steps` > `.step` + `.step-connector` items. States: `.step.is-active` (malachite), `.step.is-complete` (brand-subtle bg).

### 9.24 Quantity Selector

`.qty-selector` > `.qty-btn` (minus) + `.qty-value` + `.qty-btn` (plus)

### 9.25 Toggle / Switch

`.toggle` > `.toggle-track` > `.toggle-thumb` + `.toggle-label`. Active: `.toggle-track.is-active`.

### 9.26 Search Bar

`.search-bar` > search icon + input. Full border-radius, focus ring on `:focus-within`.

### 9.27 Order Summary / Line Items

`.line-item` > `.line-item-image` + `.line-item-info` > `.line-item-name` + `.line-item-meta` + `.line-item-price`

`.order-total` > `.order-total-label` + `.order-total-value`

---

## 10. Iconography

**Library:** Lucide Icons (inline SVG)
**Default size:** 16px for UI icons, 14px for small contexts
**Stroke width:** 2 (standard)

Common icons: search, shopping-cart, heart, package, circle-check, info, triangle-alert, x-circle, x, shield-check, lock, user, mail, credit-card, map-pin, truck, settings, log-out, eye, plus, minus, chevron-right, chevron-down, arrow-left, clipboard-list

**No emojis.** All icons are SVG-based.

---

## 11. Layout — Grid & Containers

### Grid System

| Class | Columns | Responsive |
| ----- | ------- | ---------- |
| `.grid-2` | 2 | 1 col at 640px |
| `.grid-3` | 3 | 2 col at 900px, 1 at 640px |
| `.grid-4` | 4 | 2 col at 900px, 1 at 640px |

### Containers

| Class | Max Width |
| ----- | --------- |
| `.container` | 1200px |
| `.container--sm` | 720px |
| `.container--md` | 960px |
| `.container--lg` | 1400px |
| `.container--full` | none |
