---
component: Button
id: button
version: 0.1.0
status: draft
source-library: DevExtreme dxButton
source-url: https://js.devexpress.com/jQuery/Documentation/ApiReference/UI_Components/dxButton/
figma-file: yck1tcUXgdQ5aYX6iUAwrO
figma-node: 273-11972
figma-page: "ADK / Buttons"
figma-collection: COMPONENTS
prototype: components/button/button.html
spec: components/button/button.md
modes:
  light: ADK (complete)
  dark: TDK (stub — dark mode pass TBD)
last-updated: 2026-05-13
---

# Button

**Status:** Draft · **Modes:** ADK (Light) complete; TDK (Dark) in progress · **Library:** DevExtreme dxButton  
**Prototype:** `components/button/button.html` · **Figma:** [Primary](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=273-11972) · [Secondary](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=639-51015) · [Ghost](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=639-53573)

## Who reads what

| Section | Designer | Front End | Product | Agent |
|---|:---:|:---:|:---:|:---:|
| Variants | ✓ | ✓ | ✓ | ✓ |
| States | ✓ | ✓ | ✓ | ✓ |
| Color Tokens | ✓ | ✓ | — | ✓ |
| Dimension Tokens | — | ✓ | — | ✓ |
| HTML Structure | — | ✓ | — | ✓ |
| Variable Architecture | — | ✓ | — | ✓ |
| Acceptance Criteria — Visual | ✓ | — | ✓ | ✓ |
| Acceptance Criteria — Functional | — | ✓ | ✓ | ✓ |
| Acceptance Criteria — Figma Binding | ✓ | — | — | ✓ |
| Open Questions | ✓ | ✓ | ✓ | ✓ |

---

## Variants

Three visual variants sharing the same state structure and HTML root. Each has an independent token table.

| Variant | Class | DevExtreme `stylingMode` | Description |
|---|---|---|---|
| Primary | `.dx-button-primary` | `contained` | Brand yellow — highest emphasis |
| Secondary | `.dx-button-secondary` | `contained` | Neutral gray — medium emphasis |
| Ghost | `.dx-button-ghost` | `outlined` or `text` | Transparent BG, border only — lowest emphasis |

---

## States

Applies to all three variants.

| id | Label | CSS Trigger | Figma Variant | Notes |
|---|---|---|---|---|
| `default` | Default | base styles (no class) | `State=Default` | |
| `hover` | Hover | `.dx-state-hover` | `State=Hover` | DevExtreme applies at runtime |
| `focused` | Focused | `.dx-state-focused` | `State=Focused` | 2px dashed focus ring via `--border/focus`; `--corner-radius/xs` = 2px |
| `active` | Active | `.dx-state-active` | `State=Active` | BG and border color shift; no font weight change |
| `disabled` | Disabled | `.dx-state-disabled` | `State=Disabled` | `cursor: not-allowed` on root; interaction blocked in JS |

**Out of scope for this version:**
- Icon variants (Left icon / Right icon / Icon-only) — present in Figma, next iteration
- Loading state — not present in Figma
- Dark mode (TDK) — light mode complete; dark pass is separate work (see Open Questions #6)

---

## Color Tokens

Authoritative mapping: CSS variable → applied selector → Figma variable path → resolved values.

**Dark Mode column key:**  
`stub` — dark values not yet defined; light mode only for this version  
`cascades` — will arrive via semantic token override in `html[data-theme="dark"]` once dark pass is complete  
`explicit: #value †` — will need a direct override in the dark block

† marks values with no current SHARED SEMANTIC equivalent — candidates for new token definitions.

---

### Primary — Background

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--button-primary-bg` | `.dx-button-primary → background` | `Buttons/Primary/Button Default BG` | COMPONENTS | `#fcd515 · Brand 100` | — | stub |
| `--button-primary-bg-hover` | `.dx-button-primary.dx-state-hover → background` | `Buttons/Primary/Button Hover BG` | COMPONENTS | `#fae164 · Brand 60` | — | stub |
| `--button-primary-bg-focus` | `.dx-button-primary.dx-state-focused → background` | `Buttons/Primary/Button Focused BG` | COMPONENTS | `#fae164 · Brand 60` | — | stub |
| `--button-primary-bg-active` | `.dx-button-primary.dx-state-active → background` | `Buttons/Primary/Button Active BG` | COMPONENTS | `#fff2b2 · †` | — | stub |
| `--button-primary-bg-disabled` | `.dx-button-primary.dx-state-disabled → background` | `Buttons/Primary/Button Disabled BG` | COMPONENTS | `#f2f2f2 · ADK 10` | — | stub |

### Primary — Border

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--button-primary-border` | `.dx-button-primary → border-color` | `Buttons/Primary/Button Border Default` | COMPONENTS | `#ab900e · Brand Strong` | — | stub |
| `--button-primary-border-hover` | `.dx-button-primary.dx-state-hover → border-color` | `Buttons/Primary/Button Border Hover` | COMPONENTS | `#e3c013 · †` | — | stub |
| `--button-primary-border-active` | `.dx-button-primary.dx-state-active → border-color` | `Buttons/Primary/Button Border Active` | COMPONENTS | `#e3c013 · †` | — | stub |
| `--button-primary-border-disabled` | `.dx-button-primary.dx-state-disabled → border-color` | `Buttons/Primary/Button Border Disabled` | COMPONENTS | `#cfcece · ADK 30` | — | stub |

### Primary — Text

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--button-primary-text` | `.dx-button-primary .dx-button-text → color` | `Buttons/Primary/Button Default Title` | COMPONENTS | `#3f3e3d · ADK 80` | — | stub |
| `--button-primary-text-hover` | `.dx-button-primary.dx-state-hover .dx-button-text → color` | `Buttons/Primary/Button Hover Title` | COMPONENTS | `#000000 · ADK 100` | — | stub |
| `--button-primary-text-focus` | `.dx-button-primary.dx-state-focused .dx-button-text → color` | `Buttons/Primary/Button Focus Title` | COMPONENTS | `#000000 · ADK 100` | — | stub |
| `--button-primary-text-active` | `.dx-button-primary.dx-state-active .dx-button-text → color` | `Buttons/Primary/Button Active Title` | COMPONENTS | `#3f3e3d · ADK 80` | — | stub |
| `--button-primary-text-disabled` | `.dx-button-primary.dx-state-disabled .dx-button-text → color` | `Buttons/Primary/Button Disabled Title` | COMPONENTS | `#cfcece · ADK 30` | — | stub |

---

### Secondary — Background

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--button-secondary-bg` | `.dx-button-secondary → background` | `Buttons/Secondary/Button Default BG` | COMPONENTS | `#e7e6e6 · ADK 20` | — | stub |
| `--button-secondary-bg-hover` | `.dx-button-secondary.dx-state-hover → background` | `Buttons/Secondary/Button Hover BG` | COMPONENTS | `#f2f2f2 · ADK 10` | — | stub |
| `--button-secondary-bg-focus` | `.dx-button-secondary.dx-state-focused → background` | `Buttons/Secondary/Button Focused BG` | COMPONENTS | `#f2f2f2 · ADK 10` | — | stub |
| `--button-secondary-bg-active` | `.dx-button-secondary.dx-state-active → background` | `Buttons/Secondary/Button Active BG` | COMPONENTS | `#fafafa · ADK 00` | — | stub |
| `--button-secondary-bg-disabled` | `.dx-button-secondary.dx-state-disabled → background` | `Buttons/Secondary/Button Disabled BG` | COMPONENTS | `#f2f2f2 · ADK 10` | — | stub |

### Secondary — Border

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--button-secondary-border` | `.dx-button-secondary → border-color` | `Buttons/Secondary/Button Border Default` | COMPONENTS | `#cfcece · ADK 30` | — | stub |
| `--button-secondary-border-hover` | `.dx-button-secondary.dx-state-hover → border-color` | `Buttons/Secondary/Button Border Hover` | COMPONENTS | `#b7b6b6 · ADK 40` | — | stub |
| `--button-secondary-border-focus` | `.dx-button-secondary.dx-state-focused → border-color` | `Buttons/Secondary/Button Border Focused` | COMPONENTS | `#b7b6b6 · ADK 40` | — | stub |
| `--button-secondary-border-active` | `.dx-button-secondary.dx-state-active → border-color` | `Buttons/Secondary/Button Border Active` | COMPONENTS | `#b7b6b6 · ADK 40` | — | stub |
| `--button-secondary-border-disabled` | `.dx-button-secondary.dx-state-disabled → border-color` | `Buttons/Secondary/Button Border Disabled` | COMPONENTS | `#e7e6e6 · ADK 20` | — | stub |

### Secondary — Text

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--button-secondary-text` | `.dx-button-secondary .dx-button-text → color` | `Buttons/Secondary/Button Default Title` | COMPONENTS | `#3f3e3d · ADK 80` | — | stub |
| `--button-secondary-text-hover` | `.dx-button-secondary.dx-state-hover .dx-button-text → color` | `Buttons/Secondary/Button Hover Title` | COMPONENTS | `#272625 · ADK 90` | — | stub |
| `--button-secondary-text-focus` | `.dx-button-secondary.dx-state-focused .dx-button-text → color` | `Buttons/Secondary/Button Focus Title` | COMPONENTS | `#272625 · ADK 90` | — | stub |
| `--button-secondary-text-active` | `.dx-button-secondary.dx-state-active .dx-button-text → color` | `Buttons/Secondary/Button Active Title` | COMPONENTS | `#272625 · ADK 90` | — | stub |
| `--button-secondary-text-disabled` | `.dx-button-secondary.dx-state-disabled .dx-button-text → color` | `Buttons/Secondary/Button Disabled Title` | COMPONENTS | `#cfcece · ADK 30` | — | stub |

---

### Ghost — Background

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--button-ghost-bg` | `.dx-button-ghost → background` | `Buttons/Ghost/Button Default BG` | COMPONENTS | `transparent` | — | stub |
| `--button-ghost-bg-hover` | `.dx-button-ghost.dx-state-hover → background` | `Buttons/Ghost/Button Hover BG` | COMPONENTS | `rgba(255,255,255,0.2)` | — | stub |
| `--button-ghost-bg-focus` | `.dx-button-ghost.dx-state-focused → background` | `Buttons/Ghost/Button Focused BG` | COMPONENTS | `rgba(255,255,255,0.2)` | — | stub |
| `--button-ghost-bg-active` | `.dx-button-ghost.dx-state-active → background` | `Buttons/Ghost/Button Active BG` | COMPONENTS | `rgba(255,255,255,0.2)` | — | stub |
| `--button-ghost-bg-disabled` | `.dx-button-ghost.dx-state-disabled → background` | `Buttons/Ghost/Button Disabled BG` | COMPONENTS | `transparent` | — | stub |

### Ghost — Border

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--button-ghost-border` | `.dx-button-ghost → border-color` | `Buttons/Ghost/Button Border Default` | COMPONENTS | `#e7e6e6 · ADK 20` | — | stub |
| `--button-ghost-border-hover` | `.dx-button-ghost.dx-state-hover → border-color`, `.dx-button-ghost.dx-state-focused → border-color`, `.dx-button-ghost.dx-state-active → border-color` | `Buttons/Ghost/Button Border Hover` | COMPONENTS | `#cfcece · ADK 30` | — | stub |

### Ghost — Text

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--button-ghost-text` | `.dx-button-ghost .dx-button-text → color` | `Buttons/Ghost/Button Default Title` | COMPONENTS | `#3f3e3d · ADK 80` | — | stub |
| `--button-ghost-text-hover` | `.dx-button-ghost.dx-state-hover .dx-button-text → color` | `Buttons/Ghost/Button Hover Title` | COMPONENTS | `#000000 · ADK 100` | — | stub |
| `--button-ghost-text-focus` | `.dx-button-ghost.dx-state-focused .dx-button-text → color` | `Buttons/Ghost/Button Focus Title` | COMPONENTS | `#000000 · ADK 100` | — | stub |
| `--button-ghost-text-active` | `.dx-button-ghost.dx-state-active .dx-button-text → color` | `Buttons/Ghost/Button Active Title` | COMPONENTS | `#000000 · ADK 100` | — | stub |
| `--button-ghost-text-disabled` | `.dx-button-ghost.dx-state-disabled .dx-button-text → color` | `Buttons/Ghost/Button Disabled Title` | COMPONENTS | `#cfcece · ADK 30` | — | stub |

---

### Shared — Focus Ring

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--button-focus-ring-color` | `.dx-button.dx-state-focused → outline-color` | `Border/Focus` | SHARED SEMANTIC | `#000000` (black) | — | stub |
| `--button-focus-ring-radius` | `.dx-button.dx-state-focused → border-radius` | `Corner Radius/XS` | Unknown — requires Figma inspection | `2px` | — | — |
| `--button-focus-ring-offset` | `.dx-button.dx-state-focused → outline-offset` | — | — | `2px` | — | — |

---

## Dimension Tokens

M size is confirmed from Figma. XS, S, XL, and 3L dimension values are estimated — see Open Questions #1.

| CSS Variable | Selector → Property | Value | Figma Variable | Notes |
|---|---|---|---|---|
| `--button-height-xs` | `.dx-button.button-xs → height` | `20px` | Unknown — requires Figma inspection | Estimated |
| `--button-height-s` | `.dx-button.button-s → height` | `24px` | Unknown — requires Figma inspection | Estimated |
| `--button-height-m` | `.dx-button.button-m → height` | `32px` | Unknown — requires Figma inspection | Confirmed from M-size Figma frame |
| `--button-height-xl` | `.dx-button.button-xl → height` | `40px` | Unknown — requires Figma inspection | Estimated |
| `--button-height-3l` | `.dx-button.button-3l → height` | `48px` | Unknown — requires Figma inspection | Estimated |
| `--button-padding-xs` | `.dx-button.button-xs .dx-button-content → padding` | `0 8px` | Unknown — requires Figma inspection | Estimated |
| `--button-padding-s` | `.dx-button.button-s .dx-button-content → padding` | `0 10px` | Unknown — requires Figma inspection | Estimated |
| `--button-padding-m` | `.dx-button.button-m .dx-button-content → padding` | `0 16px` | Unknown — requires Figma inspection | Estimated |
| `--button-padding-xl` | `.dx-button.button-xl .dx-button-content → padding` | `0 20px` | Unknown — requires Figma inspection | Estimated |
| `--button-padding-3l` | `.dx-button.button-3l .dx-button-content → padding` | `0 24px` | Unknown — requires Figma inspection | Estimated |
| `--button-font-size-xs` | `.dx-button.button-xs .dx-button-text → font-size` | `11px` | Unknown — requires Figma inspection | Estimated |
| `--button-font-size-s` | `.dx-button.button-s .dx-button-text → font-size` | `12px` | Unknown — requires Figma inspection | Estimated |
| `--button-font-size-m` | `.dx-button.button-m .dx-button-text → font-size` | `13px` | Unknown — requires Figma inspection | Confirmed from Figma |
| `--button-font-size-xl` | `.dx-button.button-xl .dx-button-text → font-size` | `14px` | Unknown — requires Figma inspection | Estimated |
| `--button-font-size-3l` | `.dx-button.button-3l .dx-button-text → font-size` | `16px` | Unknown — requires Figma inspection | Estimated |
| `--button-border-width` | `.dx-button → border-width` | `1px` | — | All variants, all states |
| `--button-border-radius` | `.dx-button → border-radius` | `0px` | — | Square corners; Germanedge convention |
| `--button-focus-ring-offset` | `.dx-button.dx-state-focused → outline-offset` | `0px` | — | Focus ring hugs the button edge |

---

## HTML Structure

DevExtreme dxButton renders the following DOM structure at runtime:

```html
<div class="dx-widget dx-button dx-button-mode-contained [variant-class] [size-class] [state-class]"
     role="button"
     tabindex="0"
     aria-label="Button Label">
  <div class="dx-button-content">
    <span class="dx-button-text">Button Label</span>
  </div>
</div>
```

**Variant classes** — added to root `.dx-button`:

| Class | Variant |
|---|---|
| `.dx-button-primary` | Primary |
| `.dx-button-secondary` | Secondary |
| `.dx-button-ghost` | Ghost |

**Size classes** — added to root `.dx-button`:

| Class | Height |
|---|---|
| `.button-xs` | 20px |
| `.button-s` | 24px |
| `.button-m` | 32px (reference) |
| `.button-xl` | 40px |
| `.button-3l` | 48px |

**Runtime state classes** (DevExtreme applies these automatically):

| Class | Trigger |
|---|---|
| `.dx-state-hover` | Mouse over |
| `.dx-state-focused` | Tab focus / keyboard navigation |
| `.dx-state-active` | Mouse down / Enter / Space |
| `.dx-state-disabled` | `disabled: true` option set |

---

## Variable Architecture

Buttons are predominantly **Tier 1 (shared semantic)** for text and disabled states, with **Tier 2 (component-scoped)** for the brand-surface and neutral-surface layers.

**Primary:** Default BG (`#fcd515`) maps to `--color-brand-default`; hover/focus BG (`#fae164`) maps to `--color-brand-subtle`; default border (`#ab900e`) maps to `--color-brand-strong`. Text states map cleanly to `--color-text-default`, `--color-text-hover`, and `--color-text-disabled`. Two values have no current semantic equivalent: the active BG (`#fff2b2`) and the hover/active border (`#e3c013`). These are new values introduced in the redesign and are candidates for new SHARED SEMANTIC tokens (`Colors/Brand/Brand 20` and `Colors/Brand/Brand 80` respectively).

**Secondary:** Neutral gray backgrounds and borders use theme primitives (ADK 10–40, 90) with no direct semantic surface/border equivalents defined in the SHARED SEMANTIC collection today. These are component-scoped. The text value `#272625` (ADK 90) has no semantic text token — `--color-text-strong` is defined in this prototype as a local semantic alias.

**Ghost:** Backgrounds use CSS `transparent` and `rgba(255,255,255,0.2)`. The alpha channel value has no semantic equivalent. Ghost is designed for use on colored or dark surfaces; on a white page background the hover state is nearly invisible by design.

**Rule:** Component vars in `:root` must reference `var(--color-*)` semantic tokens wherever a match exists. Raw hex appears only where no semantic equivalent exists (annotated `†`).

---

## Acceptance Criteria

### Visual (Designer · Agent)

- [ ] Primary Default: `#fcd515` BG, `#ab900e` border, `#3f3e3d` text
- [ ] Primary Hover: `#fae164` BG, `#e3c013` border, `#000000` text
- [ ] Primary Focused: `#fae164` BG, `#ab900e` border, `#000000` text, 2px dashed `#1a88b7` focus ring
- [ ] Primary Active: `#fff2b2` BG, `#e3c013` border, `#3f3e3d` text, font-weight 600
- [ ] Primary Disabled: `#f2f2f2` BG, `#cfcece` border, `#cfcece` text, `cursor: not-allowed`
- [ ] Secondary Default: `#e7e6e6` BG, `#cfcece` border, `#3f3e3d` text
- [ ] Secondary Hover: `#f2f2f2` BG, `#b7b6b6` border, `#272625` text
- [ ] Secondary Focused: `#f2f2f2` BG, `#b7b6b6` border, `#272625` text, 2px dashed focus ring
- [ ] Secondary Active: `#fafafa` BG, `#b7b6b6` border, `#272625` text
- [ ] Secondary Disabled: `#f2f2f2` BG, `#e7e6e6` border, `#cfcece` text, `cursor: not-allowed`
- [ ] Ghost Default: transparent BG, `#e7e6e6` border, `#3f3e3d` text
- [ ] Ghost Hover: `rgba(255,255,255,0.2)` BG, `#cfcece` border, `#000000` text
- [ ] Ghost Focused: `rgba(255,255,255,0.2)` BG, `#cfcece` border, focus ring, `#000000` text
- [ ] Ghost Active: `rgba(255,255,255,0.2)` BG, `#cfcece` border, `#000000` text
- [ ] Ghost Disabled: transparent BG, `#e7e6e6` border, `#cfcece` text, `cursor: not-allowed`
- [ ] Focus ring: `outline: 2px dashed #1a88b7`, `outline-offset: 0px`, `border-radius: 2px`
- [ ] All five sizes render at correct height and padding proportions

### Functional (Front End · Agent)

- [ ] Tab key focuses button; focus ring appears
- [ ] Enter and Space keys trigger active state on focused button
- [ ] Disabled button does not respond to hover, focus, or click events
- [ ] `cursor: not-allowed` displays on disabled (no `pointer-events: none` on children blocking it)
- [ ] Active state communicated by BG/border color shift only — no font weight change
- [ ] Border width is `1px` on all variants and states
- [ ] Border radius is `0px`
- [ ] Focus ring `outline-offset` is `0px` — ring hugs the button edge
- [ ] Ghost hover BG (`rgba(255,255,255,0.2)`) is visible on dark/colored surfaces, invisible on white

### Figma Binding (Designer · Agent)

- [ ] All three variant frames present in the COMPONENTS collection
- [ ] All five states present per variant
- [ ] Active BG (`#fff2b2`) and hover border (`#e3c013`) flagged for new SHARED SEMANTIC token creation
- [ ] Color tokens resolve through PRIMITIVES — no raw hex bound directly to component fills
- [ ] Variant properties match: `State=Default|Hover|Focused|Active|Disabled`, `Size=XS|S|M|XL|3L`

---

## Open Questions

| # | Question | Owner | Status |
|---|---|---|---|
| 1 | Height, horizontal padding, and font-size for XS, S, XL, 3L sizes — all need Figma measurement | Designer | Open |
| 2 | Should `#fff2b2` (Primary active BG) be added to SHARED SEMANTIC as `Colors/Brand/Brand 20`? | Designer | Open |
| 3 | Should `#e3c013` (Primary hover/active border) be added to SHARED SEMANTIC? Possible `Colors/Brand/Brand 80`? | Designer | Open |
| 4 | Ghost button hover BG is `rgba(255,255,255,0.2)` — nearly invisible on a white surface. Confirm ghost is intended only for use on colored or dark backgrounds | Designer | Open |
| 5 | Primary focused state uses default border (`#ab900e`), not hover border. Secondary focused uses hover border (`#b7b6b6`). Is the Primary discrepancy intentional? | Designer | Open |
| 6 | TDK (dark mode) token values for all three variants — dark pass required before acceptance | Designer | Open |
| 7 | DevExtreme `stylingMode` mapping: confirm whether Ghost maps to `text` or `outlined` in the actual app implementation | Front End | Open |
| 8 | Icon variant token structure (icon color, gap between icon and label, icon sizes per size tier) — needed for next iteration | Designer | Open |
