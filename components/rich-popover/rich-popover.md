---
component: Rich Popover
id: rich-popover
version: 0.1.0
status: draft
source-library: Ant Design Popover
source-url: https://ant.design/components/popover
figma-file: yck1tcUXgdQ5aYX6iUAwrO
figma-node: 22582-1562
figma-page: "ADK / Rich Popover"
figma-collection: COMPONENTS
prototype: components/rich-popover/rich-popover.html
spec: components/rich-popover/rich-popover.md
modes:
  light: ADK
  dark: TDK
last-updated: 2026-05-20
---

# Rich Popover

**Status:** Draft · **Modes:** ADK (Light) + TDK (Dark) · **Library:** Ant Design Popover  
**Prototype:** `components/rich-popover/rich-popover.html` · **Figma:** [ADK / Rich Popover](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=22582-1562)

## Who reads what

| Section | Designer | Front End | Product | Agent |
|---|:---:|:---:|:---:|:---:|
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

## States

Each state maps to a CSS trigger and a Figma variant property. Both must be kept in sync.

| id | Label | CSS Trigger | Figma Variant | Notes |
|---|---|---|---|---|
| `default` | Default | base styles (no modifier) | Variant=Default, Footer=None | Title + body; arrow at top (`placement-bottom`) |
| `with-close` | With Close Button | `.ant-popover-close` present in DOM | Variant=With-Close, Footer=None | Title row includes close button |
| `with-actions` | With Actions Footer | `.ant-popover-inner-footer` present in DOM | Variant=With-Close, Footer=Actions | Title + close + body + footer action buttons |
| `no-title` | No Title | `.ant-popover-inner-header` absent | Variant=No-Title, Footer=None | Body content only; no header or divider |
| `close-hover` | Close Button — Hover | `.ant-popover-close:hover` / `.ant-popover-close.is-hover` | State=Hover | Hover background fill on close button |
| `close-focus` | Close Button — Focus | `.ant-popover-close:focus-visible` | State=Focus | Dashed focus ring at close button edge |

**Out of scope for this version:**
- Trigger interaction / show-hide animation — runtime behavior managed by Ant Design JS; not a prototype concern
- 12 placement variants as separate states — arrow direction changes via `.ant-popover-placement-*` modifier; demonstrated as a separate row in the prototype
- Popconfirm variant (Yes/No confirmation) — separate component
- Nested popovers
- `contextMenu` trigger — runtime behavior only

---

## Color Tokens

Authoritative mapping: CSS variable → where it is applied → Figma binding → resolved values in both modes.

**Dark Mode column key:**
- `cascades` — the dark value arrives through the semantic token override in `html[data-theme="dark"]`. No explicit component var needed.
- `explicit: #value` — this component var must be set directly in `html[data-theme="dark"]`. Annotated `†` in the HTML prototype.

### Panel

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--rich-popover-surface` | `.ant-popover-inner → background` | Unknown — requires Figma inspection | COMPONENTS | `#ffffff` · White | `#31313b` · TDK 30 | cascades via `--color-surface-default` |
| `--rich-popover-border` | `.ant-popover-inner → border-color` | Unknown — requires Figma inspection | COMPONENTS | `#e7e6e6` · ADK 20 | `#3c3c44` · TDK 40 | cascades via `--color-border-default` |

### Elevation

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--rich-popover-shadow` | `.ant-popover-inner → box-shadow` | Unknown — requires Figma inspection | COMPONENTS | `0 4px 16px rgba(0,0,0,0.12)` | `0 4px 16px rgba(0,0,0,0.32)` | explicit: `0 4px 16px rgba(0,0,0,0.32)` † |

### Arrow

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--rich-popover-arrow-bg` | `.ant-popover-arrow → background` | Unknown — requires Figma inspection | COMPONENTS | `#ffffff` · White | `#31313b` · TDK 30 | cascades via `--color-surface-default` |
| `--rich-popover-arrow-border` | `.ant-popover-arrow → border-color` | Unknown — requires Figma inspection | COMPONENTS | `#e7e6e6` · ADK 20 | `#3c3c44` · TDK 40 | cascades via `--color-border-default` |

### Header

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--rich-popover-title-color` | `.ant-popover-title → color` | `Text/Default` | SHARED SEMANTIC | `#3f3e3d` · ADK 80 | `#d4d4d5` · TDK 80 | cascades via `--color-text-default` |
| `--rich-popover-header-divider` | `.ant-popover-inner-header → border-bottom-color` | Unknown — requires Figma inspection | COMPONENTS | `#e7e6e6` · ADK 20 | `#3c3c44` · TDK 40 | cascades via `--color-border-default` |

### Body

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--rich-popover-body-color` | `.ant-popover-inner-content → color` | `Text/Default` | SHARED SEMANTIC | `#3f3e3d` · ADK 80 | `#d4d4d5` · TDK 80 | cascades via `--color-text-default` |
| `--rich-popover-body-color-subtle` | `.ant-popover-inner-content .text-subtle → color` | `Text/Subtle` | SHARED SEMANTIC | `#6f6e6d` · ADK 60 | `#a9a9ac` · TDK 60 | cascades via `--color-text-subtle` |

### Footer

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--rich-popover-footer-divider` | `.ant-popover-inner-footer → border-top-color` | Unknown — requires Figma inspection | COMPONENTS | `#e7e6e6` · ADK 20 | `#3c3c44` · TDK 40 | cascades via `--color-border-default` |

### Close Button

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--rich-popover-close-icon` | `.ant-popover-close → color` | Unknown — requires Figma inspection | COMPONENTS | `#878686` · ADK 50 | `#bcbcbe` · TDK 70 | cascades via `--color-icon-default` |
| `--rich-popover-close-icon-hover` | `.ant-popover-close:hover → color` | Unknown — requires Figma inspection | COMPONENTS | `#3f3e3d` · ADK 80 | `#d4d4d5` · TDK 80 | cascades via `--color-icon-hover` |
| `--rich-popover-close-bg-hover` | `.ant-popover-close:hover → background` | Unknown — requires Figma inspection | COMPONENTS | `#e7e6e6` · ADK 20 | `#3c3c44` · TDK 40 | cascades via `--color-surface-hover` |
| `--rich-popover-close-focus-ring` | `.ant-popover-close:focus-visible → outline-color` | `Border/Focus` | SHARED SEMANTIC | `#1a88b7` · Inline Link ADK | `#7c79ff` · Inline Link TDK | explicit: `#7c79ff` † |

---

## Dimension Tokens

Dimension tokens are not bound to Figma variables. Values are fixed across both modes unless noted.

| CSS Variable | Selector → Property | Value | Figma Variable | Notes |
|---|---|---|---|---|
| `--rich-popover-min-width` | `.ant-popover-inner → min-width` | `200px` | Unknown — requires Figma inspection | Estimated — confirm in Figma |
| `--rich-popover-max-width` | `.ant-popover-inner → max-width` | `320px` | Unknown — requires Figma inspection | Estimated — confirm in Figma |
| `--rich-popover-border-width` | `.ant-popover-inner → border-width` | `1px` | — | — |
| `--rich-popover-border-radius` | `.ant-popover-inner → border-radius` | `0px` | — | Square corners per Germanedge rule |
| `--rich-popover-header-padding-v` | `.ant-popover-inner-header → padding-top/bottom` | `10px` | Unknown — requires Figma inspection | SPACING primitive — no semantic alias yet |
| `--rich-popover-header-padding-h` | `.ant-popover-inner-header → padding-left/right` | `16px` | `Padding/Padding-16` | Estimated |
| `--rich-popover-content-padding-v` | `.ant-popover-inner-content → padding-top/bottom` | `12px` | Unknown — requires Figma inspection | SPACING primitive — no semantic alias yet |
| `--rich-popover-content-padding-h` | `.ant-popover-inner-content → padding-left/right` | `16px` | `Padding/Padding-16` | Estimated |
| `--rich-popover-footer-padding-v` | `.ant-popover-inner-footer → padding-top/bottom` | `8px` | Unknown — requires Figma inspection | SPACING primitive — no semantic alias yet |
| `--rich-popover-footer-padding-h` | `.ant-popover-inner-footer → padding-left/right` | `16px` | `Padding/Padding-16` | Estimated |
| `--rich-popover-close-size` | `.ant-popover-close → width, height` | `24px` | Unknown — requires Figma inspection | Estimated |
| `--rich-popover-close-font-size` | `.ant-popover-close → font-size` | `16px` | Unknown — requires Figma inspection | — |
| `--rich-popover-arrow-size` | `.ant-popover-arrow → width, height` | `8px` | — | Visual size of the rotated square caret |
| `--rich-popover-title-font-family` | `.ant-popover-title → font-family` | `'Inter Tight', Arial, sans-serif` | Unknown — requires Figma inspection | Condensed heading font |
| `--rich-popover-title-font-size` | `.ant-popover-title → font-size` | `14px` | Unknown — requires Figma inspection | Estimated |
| `--rich-popover-title-line-height` | `.ant-popover-title → line-height` | `20px` | Unknown — requires Figma inspection | Estimated |
| `--rich-popover-title-font-weight` | `.ant-popover-title → font-weight` | `600` | Unknown — requires Figma inspection | SemiBold |
| `--rich-popover-title-letter-spacing` | `.ant-popover-title → letter-spacing` | `0` | Unknown — requires Figma inspection | — |
| `--rich-popover-body-font-family` | `.ant-popover-inner-content → font-family` | `'Inter', Arial, sans-serif` | Unknown — requires Figma inspection | Body font |
| `--rich-popover-body-font-size` | `.ant-popover-inner-content → font-size` | `14px` | Unknown — requires Figma inspection | Estimated |
| `--rich-popover-body-line-height` | `.ant-popover-inner-content → line-height` | `20px` | Unknown — requires Figma inspection | Estimated |
| `--rich-popover-body-font-weight` | `.ant-popover-inner-content → font-weight` | `400` | Unknown — requires Figma inspection | Regular |
| `--rich-popover-body-letter-spacing` | `.ant-popover-inner-content → letter-spacing` | `0` | Unknown — requires Figma inspection | — |

---

## HTML Structure

Class names follow the Ant Design Popover naming convention. Rich variant additions (`.ant-popover-inner-header`, `.ant-popover-close`, `.ant-popover-inner-footer`) extend the base Ant Design DOM structure for structured content with title, optional close, and optional footer actions.

```html
<!-- Default — Title + Body, placement-bottom (arrow at top) -->
<div class="ant-popover ant-popover-placement-bottom">
  <div class="ant-popover-content">
    <div class="ant-popover-arrow"></div>
    <div class="ant-popover-inner">
      <div class="ant-popover-inner-header">
        <div class="ant-popover-title">Popover Title</div>
      </div>
      <div class="ant-popover-inner-content">
        <p>Content text describing the item or context.</p>
      </div>
    </div>
  </div>
</div>

<!-- With Close Button -->
<div class="ant-popover ant-popover-placement-bottom">
  <div class="ant-popover-content">
    <div class="ant-popover-arrow"></div>
    <div class="ant-popover-inner">
      <div class="ant-popover-inner-header">
        <div class="ant-popover-title">Popover Title</div>
        <button class="ant-popover-close" aria-label="Close">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
            <path d="M3 3L13 13M13 3L3 13" stroke="currentColor"
                  stroke-width="1.5" stroke-linecap="square"/>
          </svg>
        </button>
      </div>
      <div class="ant-popover-inner-content">
        <p>Content text describing the item or context.</p>
      </div>
    </div>
  </div>
</div>

<!-- With Actions Footer -->
<div class="ant-popover ant-popover-placement-bottom">
  <div class="ant-popover-content">
    <div class="ant-popover-arrow"></div>
    <div class="ant-popover-inner">
      <div class="ant-popover-inner-header">
        <div class="ant-popover-title">Popover Title</div>
        <button class="ant-popover-close" aria-label="Close">...</button>
      </div>
      <div class="ant-popover-inner-content">
        <p>Content text describing the item or context.</p>
      </div>
      <div class="ant-popover-inner-footer">
        <button class="ant-popover-action">Cancel</button>
        <button class="ant-popover-action ant-popover-action-primary">Proceed</button>
      </div>
    </div>
  </div>
</div>

<!-- No Title — body content only -->
<div class="ant-popover ant-popover-placement-bottom">
  <div class="ant-popover-content">
    <div class="ant-popover-arrow"></div>
    <div class="ant-popover-inner ant-popover-no-header">
      <div class="ant-popover-inner-content">
        <p>Content text only — no header section.</p>
      </div>
    </div>
  </div>
</div>
```

**Ant Design Popover runtime behavior:**

| Behavior | Mechanism | Applied to |
|---|---|---|
| Visibility | `ant-popover-hidden` class or `display: none` on root | `.ant-popover` |
| Placement | `.ant-popover-placement-{top|bottom|left|right|topLeft|...}` | `.ant-popover` |
| Arrow direction | Derived from placement class | `.ant-popover-arrow` |
| Trigger | `hover`, `click`, `focus`, `contextMenu` — controls `open` state | Trigger element (child) |

---

## Variable Architecture

The Rich Popover is a **Tier 1 component** — nearly all visual roles map cleanly to shared semantic tokens. Panel background, border, dividers, text, icon, and focus ring all cascade from the SHARED SEMANTIC layer without component-scoped overrides. The single Tier 2 exception is `--rich-popover-shadow`: elevation/box-shadow values have no semantic equivalent in the SHARED SEMANTIC collection and must be defined at the component level. In dark mode, shadow opacity deepens and is set explicitly with a `†` annotation.

**Rules for this component:**
- All `--rich-popover-*` color variables in `:root` must reference semantic tokens — no raw hex.
- Raw hex is only permitted in `html[data-theme="dark"]` for values that cannot cascade from the semantic layer (marked `†`).
- Footer action buttons use the Button component in production — the prototype applies minimal styling via semantic tokens for visual fidelity only. Do not reference `--button-*` variables inside this component.

---

## Acceptance Criteria

### Visual (Designer · Agent)

Verify against `components/rich-popover/rich-popover.html`. Toggle dark mode with the button in the prototype header.

**Light mode (ADK):**
- [ ] Panel: white `#ffffff` background, `1px solid #e7e6e6` border, elevation shadow
- [ ] Arrow: white `#ffffff` fill, `#e7e6e6` border on outward-facing edges only
- [ ] Title: `#3f3e3d`, Inter Tight SemiBold 14px/20px
- [ ] Header divider: `1px solid #e7e6e6` separating header from body
- [ ] Body text: `#3f3e3d`, Inter Regular 14px/20px
- [ ] Close button icon: `#878686` (ADK 50), 16px
- [ ] Close button hover: icon `#3f3e3d`, background `#e7e6e6`
- [ ] Close button focus: `2px dashed #1a88b7` ring at button edge (no offset)
- [ ] Footer divider: `1px solid #e7e6e6` above action row
- [ ] Footer: Cancel (secondary) + Proceed (primary) buttons visible

**Dark mode (TDK):**
- [ ] Panel: `#31313b` background, `1px solid #3c3c44` border, deeper shadow
- [ ] Arrow: `#31313b` fill, `#3c3c44` border on outward-facing edges
- [ ] Title: `#d4d4d5`
- [ ] Header divider: `#3c3c44`
- [ ] Body text: `#d4d4d5`
- [ ] Close button icon: `#bcbcbe` (TDK 70)
- [ ] Close button hover: icon `#d4d4d5`, background `#3c3c44`
- [ ] Close button focus: `2px dashed #7c79ff` ring
- [ ] Page background switches correctly (`#fafafa` → `#202026`)
- [ ] Panel background switches correctly (`#ffffff` → `#31313b`)

### Functional (Front End · Agent)

- [ ] Popover shown inline in prototype (no runtime positioning JS required for design review)
- [ ] All 4 placement variants render correct arrow position (top / bottom / left / right)
- [ ] Arrow borders show only on the outward-facing edges (no border bleed into panel interior)
- [ ] Close button reachable via Tab key
- [ ] Close button `aria-label="Close"` present
- [ ] Focus ring appears at close button edge with `outline-offset: 0`
- [ ] Footer action buttons visually distinct: primary has brand fill, secondary is outlined

**Spacing verification:**
- [ ] Header padding: `10px 16px` (vertical / horizontal)
- [ ] Content padding: `12px 16px`
- [ ] Footer padding: `8px 16px`
- [ ] Close button: `24px × 24px` hit target
- [ ] Arrow: `8px × 8px`
- [ ] No-Title variant: content top padding equals header padding

### Figma Binding (Designer · Agent)

- [ ] All color fills in Figma frames are bound to Figma variables — no unbound hex
- [ ] COMPONENTS collection variables created and named for all component-scoped roles in Color Tokens
- [ ] Each COMPONENTS variable aliases a PRIMITIVES entry — no raw hex in Figma
- [ ] SHARED SEMANTIC collection used for `Text/Default`, `Text/Subtle`, and `Border/Focus`
- [ ] Both ADK mode and TDK mode values set on every COMPONENTS variable
- [ ] Variable scopes set explicitly — not ALL_SCOPES
- [ ] `Border/Focus` confirmed as `#1a88b7` ADK / `#7c79ff` TDK

---

## Open Questions

| # | Question | Owner | Status |
|---|---|---|---|
| 1 | Panel min/max-width — are `200px` / `320px` correct for the application context? | Design | Open |
| 2 | Footer action buttons — should the prototype use Button component tokens or minimal semantic styling? | Design + FE | Open |
| 3 | Arrow shadow — should the arrow inherit the panel shadow or have its own shadow treatment? | Design | Open |
| 4 | COMPONENTS Figma variable paths — all are Unknown; requires Figma design work to define and name variables | Design | Open |
| 5 | Spacing values — header, content, footer padding are estimated from convention; confirm against Figma text/spacing audit | Design | Open |
| 6 | Font sizes — `14px/20px` for title and body are estimated; confirm against Figma text styles | Design | Open |
| 7 | `figma-node` — updated to `22582-1562` per confirmed Figma URL | Agent | Resolved |
