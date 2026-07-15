# NeuroSolution ATX Supplement Store — Design System Reference

**Maintained By:** Lane Melancon — Onn Grid, LLC **Client:** Dr. Brandon Crawford — NeuroSolution Center of Austin **Last Updated:** 2026-07-15

---

## 1. Design Direction

The supplement store uses the NeuroSolution brand system as its foundation with a softer, more accessible treatment optimized for an eCommerce shopping context. The aesthetic is **Modern Professionalism** — prioritizing clarity, trust, and ease of navigation for patients.

### Philosophy

- **Light Mode First** — Clean, warm surfaces with white and neutral-range grays
- **Clean Minimalism** — Generous whitespace and a restricted palette keep products as the focal point
- **Warm Functionality** — Neutral grays and forest greens create a more inviting clinical space
- **Trust-Centric UI** — Stable grid structures and consistent typographic hierarchy reinforce professional-grade quality

### Relationship to Main NeuroSolution Brand

| Axis | Supplement Store | Main Clinic Site |
| --- | --- | --- |
| Primary accent | Malachite green | Lava red |
| Backgrounds | White and neutral grays | Rich Black |
| Typography | Same Objective + Trade Gothic LT — softer application | Same family — bolder |
| Tone | Clinical authority with retail warmth | Clinical evaluation |

---

## 2. Token Architecture (`tokens.css`)

`tokens.css` is a three-layer system: **primitives** → **aliases** → **dark-theme overrides**. Only alias tokens should be consumed by any downstream CSS — primitives (`--color-*`) should not be referenced directly outside of `tokens.css`.

1. **Color primitives** — raw hex ramps (`--color-green-900`…`--color-green-025`, plus `blue`, `orange`, `red`, `neutral`, each 025–900) and `--color-white` / `--color-black`.
2. **Color aliases** — semantic tokens (`--system-*`, `--brand-*`, `--surface-*`, `--text-*`, `--icon-*`, `--border-*`) that reference primitives. These flip automatically under `[data-theme='dark']`.
3. **Typography, radius, elevation, transitions, z-index, spacing** — non-color scales, theme-independent.

### 2.1 Color Primitives

| Ramp      | Steps             | Notes                               |
| --------- | ----------------- | ----------------------------------- |
| `green`   | 025, 050, 100–900 | Brand ramp (malachite → near-black) |
| `blue`    | 025, 050, 100–900 | Info system color                   |
| `orange`  | 025, 050, 100–900 | Warning system color                |
| `red`     | 025, 050, 100–900 | Error system color                  |
| `neutral` | 025, 050, 100–950 | Grays, includes a 950 dark step     |

Key green steps: `--color-green-700` (`#0C8234`, AA-compliant text/UI workhorse), `--color-green-500` (`#0BDA51`, base Malachite — dark-background use only), `--color-green-900` (`#0E2415`, deep brand background).

### 2.2 Color Aliases (Light Theme Default)

#### System

| Token                    | Value                 | Usage                   |
| ------------------------ | --------------------- | ----------------------- |
| `--system-default`       | `color-black`         | Default ink             |
| `--system-default-hover` | `rgba(14,14,14,0.15)` | Hover overlay           |
| `--system-alt`           | `color-white`         | Inverse ink             |
| `--system-subtle`        | `rgba(14,14,14,0.05)` | Subtle fill/surface-low |
| `--system-subtle-alt`    | `rgba(14,14,14,0.85)` | Strong subtle overlay   |
| `--system-disabled`      | `rgba(14,14,14,0.65)` | Disabled state          |

#### Brand

| Token                   | Value         | Usage                           |
| ----------------------- | ------------- | ------------------------------- |
| `--brand-default`       | `green-900`   | Primary brand surface/ink       |
| `--brand-alt`           | `color-white` | Inverse brand surface           |
| `--brand-accent`        | `green-500`   | Malachite accent (dark bg only) |
| `--brand-accent-alt`    | `green-700`   | AA-safe green accent (light bg) |
| `--brand-primary`       | `green-700`   | Primary CTA color               |
| `--brand-primary-alt`   | `green-200`   | Light primary variant           |
| `--brand-secondary`     | `orange-025`  | Secondary warm tint             |
| `--brand-secondary-alt` | `green-025`   | Secondary green tint            |
| `--brand-subtle`        | `green-050`   | Subtle brand fill               |
| `--brand-subtle-alt`    | `green-100`   | Subtle brand fill, stronger     |

#### Surface (brand + system state)

| Token                             | Value             |
| --------------------------------- | ----------------- |
| `--surface-brand-default`         | `brand-alt`       |
| `--surface-brand-alt`             | `brand-default`   |
| `--surface-brand-secondary`       | `brand-secondary` |
| `--surface-brand-subtle`          | `system-subtle`   |
| `--surface-success-default`       | `green-700`       |
| `--surface-success-default-hover` | `green-200`       |
| `--surface-success-subtle`        | `green-050`       |
| `--surface-info-default`          | `blue-600`        |
| `--surface-info-default-hover`    | `blue-200`        |
| `--surface-info-subtle`           | `blue-050`        |
| `--surface-warning-default`       | `orange-600`      |
| `--surface-warning-default-hover` | `orange-200`      |
| `--surface-warning-subtle`        | `orange-050`      |
| `--surface-error-default`         | `red-600`         |
| `--surface-error-default-hover`   | `red-200`         |
| `--surface-error-subtle`          | `red-050`         |

#### Text

| Token | Value |
| --- | --- |
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
| (each state also has `-subtle`, `-on-color`, `-on-color-hover` variants) |  |

#### Icon

| Token                    | Value              |
| ------------------------ | ------------------ |
| `--icon-brand-default`   | `brand-default`    |
| `--icon-brand-accent`    | `brand-accent-alt` |
| `--icon-success-default` | `green-600`        |
| `--icon-info-default`    | `blue-500`         |
| `--icon-warning-default` | `orange-500`       |
| `--icon-error-default`   | `red-500`          |

#### Border

| Token                                  | Value                       |
| -------------------------------------- | --------------------------- |
| `--border-brand-default`               | `brand-default`             |
| `--border-brand-subtle`                | `system-subtle`             |
| `--border-brand-accent`                | `brand-accent-alt`          |
| `--border-success-default` / `-subtle` | `green-700` / `green-100`   |
| `--border-info-default` / `-subtle`    | `blue-500` / `blue-100`     |
| `--border-warning-default` / `-subtle` | `orange-500` / `orange-100` |
| `--border-error-default` / `-subtle`   | `red-500` / `red-100`       |

### 2.3 Dark Theme (`[data-theme='dark']`)

Overriding the alias layer flips the whole system — downstream CSS never needs `[data-theme]` selectors of its own. Notable flips: `--brand-default` → `orange-025`, `--brand-alt` → `green-900`, `--brand-accent-alt` → `green-400`, and all `-subtle`/`-default-hover` surface, text, and border tokens shift to their `800`/`900` ramp steps.

### 2.4 Accessibility Rules

- `green-500` (`#0BDA51`) on white **fails** WCAG AA for normal text — never use as a text color on light backgrounds
- `green-700` (`#0C8234`) on white **passes** AA — safe for green text and interactive labels
- White text on `green-700` **passes** AA — safe for primary CTA surfaces
- **WCAG AA compliance is required** throughout; all text contrast must meet minimum 4.5:1 ratio

---

## 3. Typography

### 3.1 Font Stack

| Role | Font Family | CSS Variable |
| --- | --- | --- |
| Primary (headings, body, UI) | Objective | `--font-primary` |
| Secondary (Accent labels, nav links, footer headings) | Trade Gothic LT | `--font-secondary` |

**Font Source:** Self-hosted, `design-system/fonts/` (loaded via `css/fonts.css`) Loaded weights: Objective 300, 400, 500, 700, 800 (+ italics) | Trade Gothic LT 400, 700 (+ italics)

Rule: Default body copy uses Objective Regular (400). Buttons use Objective Medium (500). Trade Gothic is reserved for accent labels, desktop navbar links, and desktop footer column headings.

### 3.2 Size Scale

| Token           | rem      | Usage                |
| --------------- | -------- | --------------------- |
| `--text-h1`     | 3.625rem | H1                    |
| `--text-h2`     | 2.25rem  | H2                    |
| `--text-h3`     | 1.5rem   | H3                    |
| `--text-h4`     | 1.125rem | H4                    |
| `--text-h5`     | 1rem     | H5                    |
| `--text-accent` | 0.75rem  | Accent label          |
| `--text-2xs`    | 0.625rem | Micro captions        |
| `--text-xs`     | 0.75rem  | Fine print            |
| `--text-sm`     | 0.875rem | Supporting/meta text  |
| `--text-reg`    | 1rem     | Standard body         |
| `--text-md`     | 1.125rem | Emphasized body       |
| `--text-lg`     | 1.25rem  | Intro paragraphs      |

### 3.3 Line Height & Letter Spacing

| Token                                | Value      |
| ------------------------------------- | ---------- |
| `--leading-h1`                       | 1.1        |
| `--leading-h2`                       | 1.15       |
| `--leading-h3`                       | 1.25       |
| `--leading-h4`                       | 1.3        |
| `--leading-h5`                       | 1.4        |
| `--leading-accent`                   | 1          |
| `--leading-2xs`                      | 1          |
| `--leading-xs`                       | 1.1        |
| `--leading-sm`                       | 1.15       |
| `--leading-reg`                      | 1.5        |
| `--leading-md`                       | 1.55       |
| `--leading-lg`                       | 1.65       |
| `--tracking-h1` / `--tracking-h2`    | -0.0625rem |
| `--tracking-accent`                  | 0.125rem   |

### 3.4 Font Weights

| Token              | Value | Where Used                          |
| ------------------ | ----- | ----------------------------------- |
| `--font-light`     | 300   | Rare, decorative only               |
| `--font-normal`    | 400   | Body text                           |
| `--font-medium`    | 500   | H4, H5, button labels, input labels |
| `--font-bold`      | 700   | H1, H2, H3, accent label text       |
| `--font-extrabold` | 800   | Rare emphasis                       |

---

## 4. Spacing

Spacing uses a `--space()` custom function on a 0.25rem (4px) base increment: `calc(var(--space-base) * multiplier)`.

| Token          | Multiplier | Value           |
| -------------- | ---------- | --------------- |
| `--space-none` | 0          | 0rem            |
| `--space-4xs`  | 0.25       | 0.0625rem (1px) |
| `--space-3xs`  | 0.5        | 0.125rem (2px)  |
| `--space-2xs`  | 0.75       | 0.1875rem (3px) |
| `--space-xs`   | 1          | 0.25rem (4px)   |
| `--space-sm`   | 2          | 0.5rem (8px)    |
| `--space-reg`  | 4          | 1rem (16px)     |
| `--space-md`   | 6          | 1.5rem (24px)   |
| `--space-lg`   | 8          | 2rem (32px)     |
| `--space-xl`   | 12         | 3rem (48px)     |
| `--space-2xl`  | 16         | 4rem (64px)     |
| `--space-3xl`  | 20         | 5rem (80px)     |
| `--space-4xl`  | 25         | 6.25rem (100px) |

---

## 5. Border Radius

| Token            | Value   | Usage                 |
| ---------------- | ------- | --------------------- |
| `--rounded-sm`   | 0.25rem | Small elements        |
| `--rounded`      | 0.5rem  | Buttons, inputs       |
| `--rounded-md`   | 0.75rem | Large buttons, alerts |
| `--rounded-lg`   | 1rem    | Cards, panels         |
| `--rounded-xl`   | 1.5rem  | Large containers      |
| `--rounded-full` | 50vw    | Badges, chips, pills  |

---

## 6. Elevation / Shadows

| Token            | Usage                  |
| ---------------- | ---------------------- |
| `--shadow-xs`    | Subtle lift            |
| `--shadow-sm`    | Resting state          |
| `--shadow-md`    | Hover, elevated panels |
| `--shadow-lg`    | Dropdowns, popovers    |
| `--shadow-xl`    | Modals                 |
| `--shadow-toast` | Toasts                 |

All shadow colors use a green-tinted black (`rgba(14, 36, 21, …)`) rather than pure black, to match the brand's cool-green neutral tone.

---

## 7. Transitions

| Token | Value | Usage |
| --- | --- | --- |
| `--duration-fast` | 150ms | Hover, focus, micro-interactions |
| `--duration-normal` | 250ms | State changes, reveals |
| `--duration-slow` | 400ms | Progress bars, page transitions |
| `--ease-out` | `cubic-bezier(0.16, 1, 0.3, 1)` | Natural deceleration |
| `--ease-in-out` | `cubic-bezier(0.65, 0, 0.35, 1)` | Symmetric motion |

`prefers-reduced-motion` should be respected wherever transitions/animations are implemented — reduce to near-zero.

---

## 8. Z-Index Scale

| Token          | Value | Usage            |
| -------------- | ----- | ---------------- |
| `--z-base`     | 0     | Default stacking |
| `--z-dropdown` | 10    | Menus            |
| `--z-sticky`   | 20    | Sticky header    |
| `--z-fixed`    | 30    | Fixed sidebar    |
| `--z-overlay`  | 40    | Overlays         |
| `--z-modal`    | 50    | Modals           |
| `--z-toast`    | 60    | Toasts           |
| `--z-tooltip`  | 70    | Tooltips         |
