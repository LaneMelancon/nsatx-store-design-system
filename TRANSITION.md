# Design System → Shopify Theme Transition

**Project:** NeuroSolution ATX Supplement Store
**Maintained By:** Lane Melancon — Onn Grid, LLC
**Last Updated:** 2026-06-30

This file documents everything that needs to be considered, reconciled, or built when applying the design system to the Shopify theme (`nsatx-store-shopify-theme`). Use it as the source of truth for planning the full implementation.

---

## Strategy

**Tinker's default components are being kept.** The visual quality of Tinker's built-in components (cards, buttons, nav, product grids, etc.) is the primary reason for choosing it, and replacing them wholesale would eliminate that advantage.

The approach is therefore:

1. **Override Tinker's token layer** with brand colors, fonts, and spacing — Tinker's components inherit the new values automatically
2. **Add custom components** from the design system only where Tinker has no equivalent (alerts, toasts, badges, filter chips, etc.)
3. **Add spacing utility classes** as an additive layer — Tinker doesn't have them but they don't conflict

The design system's role is **brand token source of truth + custom component library**, not a replacement for Tinker's component CSS.

---

## Theme Context

The Shopify theme is built on **Tinker** — an exported default Shopify theme. Tinker uses:
- CSS custom properties for all tokens, defined in `snippets/theme-styles-variables.liquid`
- Its own naming conventions for colors, fonts, and spacing that differ from the design system
- Web Components (custom elements) for interactive UI, following the Shopify Dawn pattern
- `{% render %}` snippets for icons and reusable partials
- Shopify's font picker and color scheme system for merchant customization

---

## 1. Font Loading — Highest Risk

**The problem:** Tinker loads fonts through Shopify's font picker (`settings.type_body_font`, `settings.type_heading_font`, etc.) and generates CSS variables like `--font-paragraph--family`, `--font-h1--family`. The design system fonts — Objective and Trade Gothic LT — are custom fonts hosted on jsDelivr CDN. They do not exist in Shopify's font library, so the Theme Editor font picker is irrelevant.

**What needs to happen:**
- Add custom `<link rel="preload">` tags for the jsDelivr font files directly in `snippets/fonts.liquid` (or a new dedicated snippet)
- Bridge Tinker's font variable names to the design system's font stack:
  - `--font-paragraph--family` → Objective
  - `--font-h1--family` through `--font-h6--family` → Objective
  - Define a variable for Trade Gothic LT for eyebrow/label roles
- This ensures all of Tinker's existing component rules inherit the correct fonts without rewriting every rule

**Design system font variables:**

| DS Variable | Font | Role |
|---|---|---|
| `--font-primary` | Objective | Headings, body, UI |
| `--font-label` | Trade Gothic LT | Eyebrow, nav links, badges |
| `--font-mono` | SF Mono / Fira Code | Code, token display |

---

## 2. Color Tokens

**The problem:** Tinker uses semantic color variables generated from the Theme Editor's color scheme settings — `--color-background`, `--color-foreground`, `--color-primary-button-background`, etc. The design system uses `--color-green-700`, `--color-primary`, `--surface-bg`, etc. These are completely different naming conventions.

**What needs to happen:**
- After loading `tokens.css`, set Tinker's semantic vars to point at design system tokens
- Manage one source of truth (the design system tokens); Tinker's vars become aliases

**Mapping to establish (partial — expand during implementation):**

| Tinker Variable | Design System Token |
|---|---|
| `--color-background` | `var(--surface-bg)` |
| `--color-foreground` | `var(--color-gray-900)` |
| `--color-foreground-subdued` | `var(--color-gray-600)` |
| `--color-border` | `var(--color-gray-300)` |
| `--color-primary-button-background` | `var(--color-green-700)` |
| `--color-primary-button-text` | `var(--color-white)` |
| `--color-primary-button-hover-background` | `var(--color-green-600)` |
| `--color-secondary-button-background` | `var(--surface-high)` |
| `--color-input-background` | `var(--color-white)` |
| `--color-input-border` | `var(--color-gray-300)` |
| `--color-error` | `var(--sys-error-icon)` |

---

## 3. Spacing Tokens

**The problem:** The design system uses a numeric scale (`--space-1` through `--space-24`). Tinker uses named semantic tokens (`--padding-xs`, `--padding-sm`, `--padding-md`, `--padding-lg`, `--gap-sm`, `--gap-md`, `--margin-xs`, `--margin-md`, `--margin-lg`).

**What needs to happen:**
- Do not add spacing utility classes — Tinker does not use them and they won't carry over
- After loading `tokens.css`, map Tinker's spacing vars to the design system scale
- Do not hardcode pixel values in Tinker's vars — point them at `--space-*` tokens

**Important:** Tinker's spacing tokens are defined in `snippets/theme-styles-variables.liquid` using `rem` values on a non-standard scale (`--padding-md: 0.8rem`, `--gap-md: 0.9rem`, etc.). They do not align cleanly with the design system's px-based scale. Rather than trying to alias them precisely, the recommended approach is to **override Tinker's spacing vars entirely** to match the design system scale during the bridge step.

**Suggested overrides (set in the token bridge file):**

| Tinker Variable | Override Value | DS Token Reference |
|---|---|---|
| `--padding-xs` | `var(--space-2)` | 8px |
| `--padding-sm` | `var(--space-3)` | 12px |
| `--padding-md` | `var(--space-4)` | 16px |
| `--padding-lg` | `var(--space-6)` | 24px |
| `--padding-xl` | `var(--space-8)` | 32px |
| `--gap-xs` | `var(--space-2)` | 8px |
| `--gap-sm` | `var(--space-3)` | 12px |
| `--gap-md` | `var(--space-4)` | 16px |
| `--gap-lg` | `var(--space-6)` | 24px |
| `--margin-xs` | `var(--space-2)` | 8px |
| `--margin-sm` | `var(--space-3)` | 12px |
| `--margin-md` | `var(--space-4)` | 16px |
| `--margin-lg` | `var(--space-6)` | 24px |
| `--margin-xl` | `var(--space-8)` | 32px |

**In design system CSS, always use `--space-*` tokens directly — never reference Tinker's vars.** The bridge is one-directional: Tinker's vars point at DS tokens, not the reverse.

**Spacing utility classes** (`.mt-16`, `.mb-8`, etc.) are being added as an additive layer in `layout.css`. Tinker has no equivalent classes so there is no conflict — they simply extend what the theme can do without touching any existing Tinker rules.

---

## 4. CSS Load Order

**The problem:** `snippets/stylesheets.liquid` currently loads only `overflow-list.css` and `base.css`. The design system token file and custom component CSS need to be added in the correct order.

**Required load order:**
```
overflow-list.css         ← Tinker (keep as-is)
tokens.css                ← DS: establishes all brand custom properties
ds-token-bridge.css       ← new file: maps Tinker's vars → DS tokens (colors, fonts, spacing)
base.css (Tinker)         ← Tinker: keep as-is
ds-base.css               ← DS: typography fundamentals only (audit for conflicts, see §5)
ds-components.css         ← DS: custom components Tinker doesn't have (alerts, toasts, badges, etc.)
ds-utilities.css          ← DS: spacing utility classes (.mt-16, .mb-8, etc.)
```

**What's NOT being loaded:** Tinker's existing component CSS (`base.css`) is kept intact. The DS `components.css` only covers components that Tinker does not provide.

**Note:** `tokens.css` and `ds-token-bridge.css` must load before everything else so all variable references resolve correctly throughout Tinker's existing styles.

---

## 5. CSS Typography Conflict Audit

**The problem:** Since Tinker's component CSS is being kept, the DS `base.css` should only contribute typography fundamentals — not a full reset. Tinker already has its own reset. Loading a second reset on top risks overriding Tinker's carefully tuned base styles.

**What needs to happen before implementation:**
- Strip the DS `base.css` down to typography-only rules (font-family assignments, heading scale, body text, eyebrow/label styles)
- Remove any reset or box-model rules that duplicate Tinker's reset
- Audit heading rules specifically — Tinker sets `font-family` per heading level via `--font-h1--family` etc.; the DS needs to set those variables, not override the selectors directly

---

## 6. Button Appearance via Token Override

**The situation:** Tinker's `.button` and `.button-secondary` classes are kept as-is — Shopify generates them on built-in elements and they cannot be renamed. Rather than rewriting Tinker's button CSS, the brand appearance is achieved by overriding Tinker's button color variables in `ds-token-bridge.css`.

**What needs to happen:**
- Map `--color-primary-button-background` → `var(--color-green-700)`
- Map `--color-primary-button-hover-background` → `var(--color-green-600)`
- Map `--color-primary-button-text` → `var(--color-white)`
- Map `--color-secondary-button-*` → appropriate DS surface/gray tokens
- Map `--button-font-family-primary` → `var(--font-primary)`
- Verify border-radius, padding, and font-weight visually match the DS button spec after token override
- If minor adjustments are needed, add targeted overrides in `ds-token-bridge.css` — do not modify Tinker's `base.css`

---

## 7. Interactive Components — Custom Only

**The situation:** Tinker already has JavaScript for its own interactive components (drawers, modals, accordions, etc.). Only components from the design system that Tinker does not provide need to be built with JS.

**What needs to happen:**
- Audit Tinker's existing interactive components before building anything new
- Only build JS Web Components for DS components with no Tinker equivalent
- Follow Tinker's existing pattern: `customElements.define`, vanilla JS, no frameworks
- Use `CustomEvent` on `document` for cross-component communication
- All new interactive components must be keyboard accessible

**DS components likely needing JS (verify Tinker doesn't already have these):**

| Component | Behavior Needed |
|---|---|
| Toast / notification | Auto-dismiss timer, manual close |
| Filter chips | Toggle active state, emit filter event |
| Quantity selector | Increment/decrement with min/max bounds |
| Toggle / Switch | Toggle active state |
| Step indicator | Driven by parent flow, may not need standalone JS |

---

## 8. Theme Editor Section Padding

**The problem:** Tinker injects `--padding-block-start`, `--padding-block-end`, `--padding-inline-start`, `--padding-inline-end` inline on section elements via the Theme Editor. The design system has no awareness of this pattern. If section wrappers don't consume these variables, merchants lose the ability to control section spacing from the Theme Editor.

**What needs to happen:**
- Every section's outermost wrapper must include:
  ```css
  padding-block: var(--padding-block-start) var(--padding-block-end);
  padding-inline: var(--padding-inline-start) var(--padding-inline-end);
  ```
- Expose padding controls in each section's `{% schema %}` settings using Tinker's standard padding input pattern
- Never hardcode section padding in component CSS — always delegate to these variables

---

## 9. Icons — Liquid Snippets

**The problem:** The design system uses inline Lucide SVGs directly in HTML. In Shopify, the standard pattern is `{% render 'icon-name' %}` — each icon is a `.liquid` snippet file in `snippets/`.

**What needs to happen:**
- Inventory all icons used across the design system pages
- Create one `snippets/icon-[name].liquid` file per icon containing the SVG markup
- Replace all inline SVGs in Liquid templates with `{% render 'icon-[name]' %}`
- Standardize size and stroke-width via CSS, not SVG attributes, for flexibility

**Icons to create snippets for (from design system CLAUDE.md):**
search, shopping-cart, heart, package, circle-check, info, triangle-alert, x-circle, x, shield-check, lock, user, mail, credit-card, map-pin, truck, settings, log-out, eye, plus, minus, chevron-right, chevron-down, arrow-left, clipboard-list

---

## 10. Localization

**The problem:** The design system has hardcoded English strings throughout all demo pages. Shopify requires all customer-facing strings to use translation keys — `{{ 'key' | t }}` — with definitions in `locales/en.default.json`.

**What needs to happen:**
- Identify every customer-facing string in Liquid templates during the port
- Add a `locales/en.default.json` entry for each
- Never hardcode English copy in `.liquid` files — even for a single-locale store
- Common strings to plan for: button labels, form labels, error messages, empty states, navigation labels, cart strings, order summary labels

---

## 11. Image Handling

**The problem:** The design system uses CSS placeholder backgrounds (`green-50`) for card images. In Shopify, all product and collection images must use the `image_url` filter with explicit `width` and `height`, and `srcset` for responsive delivery.

**What needs to happen:**
- Replace all `.card-image` CSS placeholder divs with proper Shopify image rendering
- Use `image_tag` filter which auto-generates `srcset`
- Always provide `loading="lazy"` for below-the-fold images
- Use `fetchpriority="high"` and `loading="eager"` for above-the-fold hero images
- Never output raw CDN URLs or hardcoded image sizes

---

## Recommended Implementation Order

Execute in this sequence to minimize rework and keep the theme functional at each step:

1. **Finalize DS spacing token naming** — rename to pixel-value convention (`--space-16` = 1rem) and add missing values (`--space-14`, `--space-28`) before any token bridge work
2. **Font loading** — add jsDelivr preload tags to `snippets/fonts.liquid`; disable Shopify font picker
3. **Build `ds-token-bridge.css`** — map all Tinker color, font, and spacing vars to DS tokens; load via `stylesheets.liquid` after `tokens.css`
4. **Base typography audit** — strip DS `base.css` to typography-only, resolve any heading rule conflicts with Tinker
5. **CSS load order** — wire all files into `stylesheets.liquid` in correct sequence
6. **Verify Tinker components look correct** — buttons, cards, nav, inputs should all reflect brand tokens at this point with no component CSS written yet
7. **Audit Tinker's interactive components** — identify what JS already exists before building new Web Components
8. **Icon snippets** — build the full set once before working on any sections
9. **Add DS custom components** — alerts, toasts, badges, filter chips; only what Tinker doesn't provide
10. **Add spacing utility classes** — `ds-utilities.css` with `.mt-*`, `.mb-*`, `.gap-*` etc.
11. **Localization pass** — establish `locales/en.default.json` structure before copy proliferates in templates
12. **Section-by-section build** — Homepage → PLP → PDP → Cart → Checkout → Account → Login → Order Confirmation
    - Each section: wire schema padding controls, use icon snippets, use translation keys, use Shopify image rendering

---

## Open Questions

- [ ] How should dark-background sections (`.nav--dark`, `green-900` footers) integrate with Tinker's color scheme system?
- [ ] Will the jsDelivr font CDN be used in production, or should font files be self-hosted in `assets/`?
- [ ] Which Tinker interactive components already have JS (audit needed before building new Web Components)?
