---
name: inspire-core
description: >
  Foundation reference for all Inspire design system skills. Encodes system
  philosophy, token architecture, ADK/TDK rules, Germanedge styling constraints,
  Figma file references, GitHub Pages requirements, and the 9-check acceptance
  process. Load this before any component or pattern skill runs.
type: reference
skill-type: foundation
version: 2.0.0
last-updated: 2026-05-22
---

# Inspire Core — Foundation Reference

This document is the authoritative rules layer for every Inspire design system
skill. It does not run interactively. Other skills load it as context to ensure
they apply consistent rules without re-encoding them.

---

## System overview

**Platform:** Edge.One by Germanedge  
**Design system:** Inspire  
**Consumer:** App Composer — a no-code/low-code environment where authorized users
visually build dashboards and applications from pre-built components  
**Maintained by:** UX, Germanedge

Skills in this library serve two directions:
- **Toward code** — HTML prototypes and `.md` specs that developers implement
- **Toward App Composer** — component and pattern definitions that govern how
  dashboards are built in the no-code environment

---

## Creative North Star

**"The Architectural Editor."** Screens built from Inspire building blocks should feel like **deliberately composed structures** — not ad-hoc control dumps. Boardlets, dashboards, and dialogs read as editorial, trustworthy spaces where data and actions are arranged with intent.

**Experience intent:** Inspire avoids heavy border boxing in favor of **surface nesting** and **semantic color** so applications feel calm, premium, and scannable — for both App Composers at work in the editor and end users in the experiences they publish.

---

## Design philosophy

**Voice of the UI:**
- **Clear over clever** — labels and actions are immediately scannable and unambiguous
- **Confident and calm** — steady spacing and grouping so rich, control-heavy surfaces read as ordered, not noisy
- **Hierarchy-first** — the interface communicates priority through structure + emphasis, not borders or clutter

**Visual style:**
- Flat design — clean surfaces, strong typography, restrained depth; no skeuomorphic effects
- Elevation via shadows (surface-on-surface) — shadows communicate **layering**, not decoration; use sparingly

**Interaction philosophy:**
- One obvious next step — each screen/dialog should ideally have one Primary action
- Secondary actions are supportive — available but not competing with Primary
- Tertiary actions stay contextual — inline, low-emphasis, or in overflow

---

## Personas

Three primary personas optimized for in App Composer products:

| Persona | Focus |
|---|---|
| **Application Administrator** | Multitaskers, troubleshooters — precision and prioritization |
| **Internal Stakeholders** | Collaboration, clarity, alignment, growth |
| **Application Users (End Customers)** | Usability, satisfaction, outcome-focused flows |

---

## Product anatomy (composition hierarchy)

Namespace → Applications → Dashboard → Boardlet & Dialog → UI Elements

The **Home Dashboard** is the epicenter for visibility into status and metrics. This hierarchy governs naming and component placement decisions.

---

---

## Source of truth hierarchy

**Figma is the source of truth.** HTML prototypes and `.md` specs are validated
against Figma — not the other way around. When a value in the prototype or spec
conflicts with Figma, Figma wins and the prototype/spec is updated.

In any conflict, the higher tier wins. The lower tier needs updating, not the higher.

| Tier | Source | Authority over |
|---|---|---|
| 1 | **Figma ADS file** | Variable values, component structure, spacing, states |
| 2 | **HTML prototypes** (`.html`) | Living reference implementation |
| 3 | **Markdown specs** (`.md`) | Machine-authoritative contract |
| 4 | **Docs site** (`e1-dev.k8s.myapp.de/help-and-resources/`) | Usage guidance only; lags behind design |

When docs conflict with Figma or prototypes: Figma wins. Flag the inconsistency in
`ROADMAP.md` and update docs separately.

**Future — Storybook:** If a coded Storybook is established as the authoritative
implementation, the validation direction shifts. Figma will validate against
Storybook rather than Storybook validating against Figma. Update the tier table
and all acceptance checks at that point to reflect code as Tier 1.

---

## Themes

| Theme | Code | Context |
|---|---|---|
| Astronaut | **ADK** | Default / light mode |
| Tokyo | **TDK** | Dark mode |

The docs site uses "Astronaut" and "Tokyo". Specs and prototypes use ADK/TDK.
Both refer to the same themes — never mix the long and short forms in a single document.

---

## Figma file references

| Resource | Key / ID |
|---|---|
| ADS file key | `yck1tcUXgdQ5aYX6iUAwrO` |
| Variables page node | `21891:8273` |
| SHARED SEMANTIC collection | on Variables page, collection name "SHARED SEMANTIC" |
| COMPONENTS collection | on Variables page, collection name "COMPONENTS" |
| SPACING collection | on Variables page, collection name "SPACING" |

Always use the Figma MCP (`get_variable_defs`) to fetch live values — never copy
from another component's file or from a prior session's memory. Memory values
may be stale.

---

## Token architecture

### Two tiers

**Tier 1 — SHARED SEMANTIC (default)**

Use when the visual role maps to a defined semantic group:
`Text/`, `Surface/`, `Colors/`, `Border/`

CSS variable format: slash path, lowercase, spaces become dashes.
Example: `Text/Default` → `--text/default`, `Colors/Brand/Brand 100` → `--colors/brand/brand-100`

**Tier 2 — Component-scoped (exception only)**

Use when the component has a unique visual role with no semantic equivalent
(e.g. filled track, circular handle, progress bar fill).

Naming: `--[component]-[element]-[property]-[state]`
Example: `--slider-track-fill-default`

### Rules

- Component vars declared in `:root` must reference semantic tokens — never raw hex.
- Raw hex is allowed only in `html[data-theme="dark"]` for values that cannot
  cascade from the semantic layer. Annotate each with `†`.
- Never bind a component to an UNSET token (see list below).
- Never use COMPONENTS collection palette aliases as terminal values
  (e.g. `--generic/theme/theme-80`, `--all-theme-50`). Replace with the SHARED
  SEMANTIC equivalent.

### UNSET tokens — do not bind to these

The following SHARED SEMANTIC variables have placeholder values (#ffffff/#000000)
and are not ready for use. Check with Figma before assuming they have been defined.

```
Surface/Subtle, Surface/Hover, Surface/Disabled, Surface/Overlay,
Surface/Selected, Surface/Selected Alt, Surface/Selected Hover, Surface/Highlight,
Border/Subtle, Border/Default, Border/Strong, Border/Emphasis,
all Icon/*, all Status/*, all Brand/*
```

### Safe-to-use SHARED SEMANTIC tokens (confirmed values)

| Group | ADK | TDK |
|---|---|---|
| `--text/default` | #3f3e3d | #d4d4d5 |
| `--text/hover` | #000000 | #ffffff |
| `--text/subtle` | #6f6e6d | #a9a9ac |
| `--text/disabled` | #cfcece | #50505d |
| `--text/selected-default` | #3f3e3d | #d4d4d5 |
| `--text/selected-hover` | #000000 | #f8f8f8 |
| `--surface/page` | #f2f2f2 | #202026 |
| `--surface/default` | #ffffff | #31313b |
| `--border/focus` | #1a88b7 | #7c79ff |
| `--colors/theme/theme-00` | #fafafa | #202026 |
| `--colors/theme/theme-10` | #f2f2f2 | #24242b |
| `--colors/theme/theme-20` | #e7e6e6 | #292930 |
| `--colors/theme/theme-30` | #cfcece | #31313b |
| `--colors/theme/theme-40` | #b7b6b6 | #3c3c44 |
| `--colors/theme/theme-50` | #878686 | #50505d |
| `--colors/theme/theme-60` | #6f6e6d | #a9a9ac |
| `--colors/theme/theme-70` | #575655 | #bcbcbe |
| `--colors/theme/theme-80` | #3f3e3d | #d4d4d5 |
| `--colors/theme/theme-90` | #272625 | #efefef |
| `--colors/theme/theme-100` | #000000 | #f8f8f8 |
| `--colors/brand/brand-100` | #fcd515 | #ffd14a |
| `--colors/brand/brand-60` | #fae164 | #f5dd66 |
| `--colors/brand/brand-40` | #fbe67e | #fceb98 |
| `--colors/danger/danger-100` | #f93838 | #f55150 |
| `--colors/danger/danger-60` | #ff6464 | #f33231 |
| `--colors/danger/danger-40` | #f68f8f | #b80c0b |
| `--colors/success/success-100` | #74cf06 | #96c85a |
| `--colors/success/success-60` | #8fda34 | #87d32b |
| `--colors/success/success-40` | #afe96a | #6da12e |
| `--colors/warning/warning-100` | #ff9b05 | #ffb443 |
| `--colors/warning/warning-60` | #ffb23f | #ffa800 |
| `--colors/warning/warning-40` | #ffc46b | #b77411 |
| `--colors/note/note-100` | #2acff3 | #2acff3 |
| `--colors/note/note-60` | #55dbf4 | #42f1fc |
| `--colors/note/note-40` | #9eefff | #7fdae7 |
| `--colors/inline-link/inline-link-default` | #1a88b7 | #7c79ff |
| `--colors/inline-link/inline-link-hover` | #009ec0 | #534ffd |
| `--colors/inline-link/inline-link-visit` | #82c6e2 | #4f4da7 |

### Invalid COMPONENTS palette aliases

These are COMPONENTS collection re-exports, not SHARED SEMANTIC paths. Using
them is a Check 7 blocker. Replace with the SHARED SEMANTIC path.

| Invalid | Replace with |
|---|---|
| `--generic/theme/theme-80` | `--colors/theme/theme-80` or `--text/default` |
| `--generic/theme/theme-90` | `--colors/theme/theme-90` |
| `--generic/theme/theme-30` | `--colors/theme/theme-30` |
| `--generic/theme/theme-50` | `--colors/theme/theme-50` |
| `--generic/theme/white` | `--surface/default` |
| `--generic/danger/danger-100` | `--colors/danger/danger-100` |
| `--all-theme-50` | `--colors/theme/theme-50` |
| `--all-theme-*` (any step) | `--colors/theme/theme-*` |

---

## SPACING collection

Two tiers in the ADS Figma file:
1. **Primitives** — full scale of raw numeric values. Not applied directly.
2. **Semantic aliases** — `Gap/` and `Padding/` variables built on primitives.
   As-needed only — not every value has a semantic alias.

### Confirmed semantic aliases

| Figma Variable | Value |
|---|---|
| `Gap/Gap-08` | 8px |
| `Gap/Gap-24` | 24px |
| `Gap/Gap-48` | 48px |
| `Padding/Padding-08` | 8px |
| `Padding/Padding-16` | 16px |
| `Padding/Padding-24` | 24px |
| `Padding/Padding-48` | 48px |

This set is partial. Always check the SPACING collection in Figma before assuming
an alias doesn't exist. If none exists for the needed value: use the primitive
and note `SPACING primitive — no semantic alias yet`.

---

## Accessibility requirements

**Baseline: WCAG 2.1 Level AA.** This is the minimum for all Inspire components.
No specific WCAG level is currently stated in the Edge.One docs site — we are
setting AA as the explicit floor.

The docs site (`e1-dev.k8s.myapp.de/help-and-resources/`) contains the following
a11y guidance that aligns with these rules. Reference it for component-specific
notes:
- **Boardlet:** provide localized `boardletNameTranslations` + `titleTranslations`
  for assistive technology; supplement color with recognizable icons and text;
  keep overflow actions reachable via `moreIconVisible`
- **Accordion / Accordion Item:** meaningful unique titles; avoid icon-only labels;
  predictable expansion order; avoid color-only meaning

---

### Design-level rules (Figma audit)

These apply when auditing or creating components in Figma.

| Rule | Standard | Notes |
|---|---|---|
| Text contrast | 4.5:1 minimum against background | WCAG 2.1 AA — normal text |
| Large text contrast | 3:1 minimum | 18px+ regular or 14px+ bold |
| UI element contrast | 3:1 minimum against adjacent color | Applies to borders, icons, focus rings, toggle states |
| Color-only state | Never use color as the sole communicator | Pair with shape, icon, pattern, or text. Docs: Boardlet, Accordion |
| Focus indicator | Visible, 3:1 contrast against adjacent colors | Our focus ring (`2px dashed --border/focus`) satisfies this |
| Touch targets | 24×24px minimum for interactive elements | Already our icon-only button floor |
| Text labels | All interactive elements have visible text or a paired icon+label | Docs: "avoid icon-only labels" (Accordion) |
| Localized strings | Provide translations for all text exposed to assistive technology | Docs: Boardlet `boardletNameTranslations`, Accordion `titleTranslations` |

**Known violation to resolve — Toggle Switch:**
The "on" state currently uses brand yellow `#fcd515` against white `#ffffff`.
Contrast ratio ≈ 1.07:1. This fails the 3:1 UI element threshold by a wide
margin. The on-state indicator must use a high-contrast approach independent
of the yellow token. This is the primary reason Toggle Switch is in the
component update list.

---

### Code-level rules (HTML/CSS audit)

These apply when auditing or building HTML prototypes before engineer handoff.

| Rule | Implementation | Notes |
|---|---|---|
| Icon-only buttons | Must have `aria-label` | Applies to all icon-only variants in every component |
| Form fields | Must have an associated `<label>` (via `for`/`id`) or `aria-label` | No unlabelled inputs |
| Keyboard access | Tab, Enter/Space, and Arrow keys must work for all interactive elements | Per-component keyboard map belongs in each component's spec |
| ARIA state | Use `aria-expanded`, `aria-selected`, `aria-current`, `aria-live` where applicable | Do not omit state ARIA on disclosure, selection, and live-update patterns |
| Focus ring | `outline: 2px dashed var(--border/focus); outline-offset: 0px` | Already required in styling rules — the a11y rationale is visible focus |
| Disabled elements | `cursor: not-allowed` + visual muting; never `pointer-events: none` alone | Disabled ≠ hidden — element must still be perceivable and announced |
| Color-only state | Never rely on color alone — pair with icon, pattern, or text | Docs: Boardlet, Accordion. Applies to all interactive and status states |
| `dataTestId` | Expose on all interactive elements | Docs: Boardlet, Accordion. Enables automated a11y regression testing |

---

### Severity in acceptance reports

| Failure type | Severity | Rationale |
|---|---|---|
| Contrast failure (text or UI element) | ⛔ BLOCKER | Hard barrier for users with low vision; not resolvable by the user |
| Color-only state | ⛔ BLOCKER | Excludes color-blind users; resolvable at design time |
| Missing `aria-label` on icon-only | ⚠️ FLAG | Screen reader fails silently; must be resolved before production |
| Missing form field label | ⚠️ FLAG | Must be resolved before production |
| Missing keyboard access | ⚠️ FLAG | Must be resolved before production |
| Missing ARIA state | ⚠️ FLAG | Must be resolved before production |
| Missing `dataTestId` | ⚠️ NOTE | Best practice; does not block production |

---

## Typography

**Fonts:** `Inter Tight` (substitutes for GermanedgeSansCn — condensed/headings) and `Inter` (substitutes for GermanedgeSans — body). Load both from Google Fonts in every prototype.

**Figma page:** `Typeface` (page `0:1`), guideline frame `5423:304180`.

### Focus headlines — `Headline-focus/*` (communication / hero-style)

Uses **Inter Bold (700)**.

| Token | Size / line-height |
|---|---|
| `headline-focus-header` | 24px / 24px |
| `headline-focus-01` | 24px / 30px |
| `headline-focus-02` | 32px / 40px |
| `headline-focus-03` | 42px / 50px |
| `headline-focus-04` | 72px / 80px |

### Product headlines — `Headline/*` (UI content headings)

Uses **Inter SemiBold (600)**.

| Token | Size / line-height |
|---|---|
| `headline-01` | 12px / 16px |
| `headline-02` | 14px / 18px |
| `headline-03` | 18px / 24px |

### Body — `Body/*`

Uses **Inter Tight** (Regular 400 or SemiBold 600).

| Token | Weight | Size / line-height |
|---|---|---|
| `body-01` | Regular / SemiBold | 12px / 16px |
| `body-02` | Regular / SemiBold | 14px / 18px |
| `body-03` | Regular / SemiBold | 16px / 20px |
| `body-05` | Regular / SemiBold | 20px / 24px |

Underline variants (`body-underline-*`) exist for all sizes — use for inline linked body text.

### Caption — `Caption/*`

Uses **Inter Tight Regular**.

| Token | Size / line-height |
|---|---|
| `caption-01` | 8px / 8px |
| `caption-02` | 12px / 12px |

### Controls (buttons, inputs)

Default: `Body/Regular/body-02` (Inter Tight, 14px Regular, 18px line-height) unless the variant specifies SemiBold.

---

## Spacing

**Figma page:** `Spacings` (page `24:1995`), guideline frame `5517:220986`.

### Spacing primitive scale — `Spacing-01` → `Spacing-14`

| Token | Value |
|---|---|
| Spacing-01 | 2px |
| Spacing-02 | 4px |
| Spacing-03 | 8px |
| Spacing-04 | 12px |
| Spacing-05 | 16px |
| Spacing-06 | 20px |
| Spacing-07 | 24px |
| Spacing-08 | 32px |
| Spacing-09 | 48px |
| Spacing-10 | 64px |
| Spacing-11 | 80px |
| Spacing-12 | 96px |
| Spacing-13 | 112px |
| Spacing-14 | 128px |

Use Spacing-* tokens for layout between regions. For component internal spacing, prefer component-specific tokens (e.g. `Button/paddingInline`, `Input/paddingBlock`).

### Row tokens — fixed vertical heights

Row tokens define fixed vertical heights for layout rhythm across breakpoints. Button variants also use row-scale size values (§row-XS through §row-3L).

| Token | Value |
|---|---|
| §row-01 | 24px |
| §row-02 | 32px |
| §row-03 | 40px |
| §row-04 | 48px |
| §row-05 | 56px |
| §row-06 | 64px |
| §row-07 | 72px |

---

## Grid

**Figma page:** `Grid` (page `1044:137823`), guideline frame `5423:311928`.

> *"The grid is fundamental to everything we design. The 24/12 fluid grid is the geometric foundation of all of Inspire's visual elements."*

### Orientation rules

| Orientation | Grid | Use |
|---|---|---|
| Landscape (desktop, tablet landscape) | **24 columns × 12 rows** | Width is the longer side |
| Portrait (tablet portrait, mobile) | **12 columns × 24 rows** | Height is the longer side |

### Gutters and margins

| | Value |
|---|---|
| Gutter (between columns) | **8px** |
| Margin — mobile | **8px** left/right |
| Margin — tablet/desktop | **24px** left/right |

### Global layout rules (confirmed 2026-05-22)

| Rule | Value | Token |
|---|---|---|
| Page padding — desktop/tablet | 24px | `Padding/Padding-24` |
| Page padding — mobile | 16px | `Padding/Padding-16` |
| Universal gap between major layout zones | 8px | `Gap/Gap-08` |
| Navigation sidebar — open width | 340px | structural constant (no token) |
| Navigation sidebar — default state | hidden | — |
| Navigation sidebar — states | open or closed only (no collapsed/icon state) | — |
| Header height — desktop/tablet | 72px | structural constant (no token) |
| Header height — mobile | 64px | structural constant (no token) |
| Content width | Always full-bleed — no max-width cap | — |
| Bottom padding (72px desktop / 64px mobile) | ⚠️ FLAGGED — source conflict, do not use | see GOVERNANCE |

### Grid conflict flag (D29)

⚠️ **D29:** Dashboard docs reference a 16-column / 9-row grid. The canonical spec (`DESIGN.md §5`) defines **24×12 landscape / 12×24 portrait**. Use the DESIGN.md values. Flag D29 is tracked in GOVERNANCE.md.

---

## Elevation

**Figma page:** `Elevation ` (trailing space in file name — page `244:11803`).

Inspire encodes elevation as **named shadow effect styles** in Figma, not ad-hoc blur/opacity rules. Use these names — do not invent shadow values.

| Style name | Type | Summary |
|---|---|---|
| `Elevation/ADK Base` | Drop shadow | `#000000` ~18% alpha, offset (0, 1), blur 4 |
| `Elevation/ADK Height` | Drop shadow | `#0F0E0D` ~18% alpha, offset (0, 1), blur 8 |
| `Elevation/ADK Level 3` | Drop shadow | `#0F0E0D` ~24% alpha, offset (0, 8), blur 16 |
| `Elevation/ADK Level 4` | Drop shadow | `#0F0E0D` ~18% alpha, offset (0, 1), blur 32 |
| `Elevation/ADK Depth` | Inner shadow | `#0F0E0D` ~10% alpha, offset (0, 1), blur 5 |

Use depth primarily through tonal nesting (surface shifts). Reserve stronger elevation steps for overlays, popovers, and modals. TDK may reuse ADK elevation names — confirm per component before assuming separate TDK-only effect tokens.

---

## Production codebase vs Figma tokens — important distinction

The production Edge.One codebase uses a Bootstrap-derived utility class spacing
system (`m-4`, `p-4`, `row-gap-4`). This is **not** the SPACING collection.
The docs site reflects this old system — that is the root cause of inconsistency
I-03 in the ROADMAP.

**New components must use SPACING collection variables, not utility classes.**
When you see docs or production SCSS referencing utility class names, those are
from the legacy system. Ignore them and use the SPACING collection.

The production SCSS also uses `GermanedgeSans` / `GermanedgeSansCn` font names.
These map to `Inter` / `Inter Tight` in prototypes and specs.

---

## Germanedge styling rules

These rules apply to every component and prototype. They are non-negotiable
without an explicit design decision captured in the spec's Open Questions.

### Typography

- **Condensed / headings:** `Inter Tight` (substitutes for GermanedgeSansCn)
- **Body:** `Inter` (substitutes for GermanedgeSans)
- Load both from Google Fonts in every prototype.

### Border radius

**The system uses multiple radius values — not `0px` everywhere.** See `inspire-design-language/SKILL.md` for the full as-built component audit.

Quick reference (as-built):

| Value | Components |
|---|---|
| 0px | Labeled buttons (Primary, Secondary, Ghost) |
| 2px | Checkbox, Tag, Tooltip, Quick Filters, Calendar day cell |
| 4px | Cards, Boardlets, Dialog shells, Toolbar (top corners), Progress bar linear, Bottom Sheet, Tray Card → except 8px |
| 8px | Tray Card |
| 9999px / fully rounded | Icon-only buttons, Toggle switch, Progress bar capsule |

Any new radius value must be documented in the spec's Open Questions with a reason before it can be accepted. When the proposed 4-step token scale (radius-xs/sm/md/full) is adopted, update this reference.

### Focus rings

```css
outline: 2px dashed var(--border/focus);
outline-offset: 0px;  /* at the element edge, not offset */
```

ADK: `#1a88b7` · TDK: `#7c79ff` (via `--border/focus`).

### Disabled state

```css
.dx-state-disabled { cursor: not-allowed; }
```

Do NOT use `pointer-events: none` on interactive child elements — it prevents
the cursor from displaying. Block interaction via JS guard:
```js
if (el.classList.contains('dx-state-disabled')) return;
```

### Inline link colors

Always use `--colors/inline-link/*` tokens. Never hardcode link colors.

```css
a { color: var(--colors/inline-link/inline-link-default); }
a:hover { color: var(--colors/inline-link/inline-link-hover); }
```

ADK default: `#1a88b7` · TDK default: `#7c79ff`  
ADK hover: `#009ec0` · TDK hover: `#534ffd`

### Spacing

All gap and padding values must use explicit CSS variables — never omit or
hardcode. Reference the SPACING collection (see above).

---

## Dark mode rules

Dark mode is toggled by adding `data-theme="dark"` to the `<html>` element.

### CSS structure

```css
/* 1. Semantic tokens — light mode */
:root {
  --text/default: #3f3e3d;
  /* ... */
}

/* 2. Component variables referencing semantic tokens */
:root {
  --[component]-[element]-[property]: var(--text/default);
}

/* 3. Dark mode overrides */
html[data-theme="dark"] {
  /* Semantic token overrides */
  --text/default: #d4d4d5;
  /* Component explicit overrides (annotate †) */
  --[component]-[element]-[property]: #explicit-hex; /* † */
  /* REQUIRED: explicit body background */
  body { background: #202026; }
}
```

### Dark mode cascade failure — known failure mode

CSS variable cascade can fail on CDN-served pages (GitHub Pages edge nodes)
even when it works locally. Always add explicit property declarations in the
dark mode block for body background and any hardcoded structural colors:

```css
html[data-theme="dark"] body { background: #202026; }
```

Do not rely solely on a CSS variable reference for `body { background }` — add
the explicit hex as well.

### Page chrome dark mode

The prototype page chrome (headers, tab bars, labels, code blocks, rule lines)
must have dark overrides. No hardcoded hex colors anywhere in the page chrome.
Every hardcoded color in the light layout needs a corresponding dark override.

---

## GitHub Pages requirements

Apply these to every HTML prototype. They prevent two known failure modes.

### No-cache meta tags

Add to `<head>` in every prototype:

```html
<meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate" />
<meta http-equiv="Pragma" content="no-cache" />
<meta http-equiv="Expires" content="0" />
```

Without these, the GitHub Pages CDN serves stale files after updates are pushed.

### `.nojekyll` file

A file named `.nojekyll` (empty, no extension) must exist at the repo root.
Without it, GitHub Pages runs Jekyll, which intercepts `.md` files with YAML
frontmatter and returns 404 or renders them as HTML instead of serving them raw.

This is a one-time repo-level requirement — check before pushing a new component,
not per-component.

---

## Acceptance check process

Run these 8 checks after every spec and prototype is complete, before wrapping up.
All items marked ⛔ are blockers — the component cannot be accepted until resolved.

### Check 1 — Semantic Variable Compliance ⛔

Every color token must reference the SHARED SEMANTIC collection where a match exists.

| Status | Meaning |
|---|---|
| ✅ PASS | Uses a valid SHARED SEMANTIC token, or no semantic equivalent exists |
| ⛔ FAIL | A SHARED SEMANTIC equivalent exists but a cross-component or primitive alias is used |
| ⚠️ DRIFT | ADK matches semantic ADK but TDK value diverged (needs design decision) |
| — NO MATCH | No semantic equivalent defined yet (acceptable; flag for future token creation) |

### Check 2 — Spacing Compliance ⛔

All gap and padding values must reference a SPACING collection alias if one exists.
Hardcoded values without a variable are blockers.

### Check 3 — Cross-Component Variable Borrowing ⛔

A component may only reference its own component-scoped vars and SHARED SEMANTIC vars.
Referencing another component's scoped vars is a blocker.

Real example: ADK / Chat / List Item used `--input/hover-bg` instead of a semantic
hover token.

### Check 4 — State Completeness ⛔

Required states: Default, Hover, Focus, Active, Disabled, Error.
Each must either be present or explicitly listed as out-of-scope in the spec's
Open Questions. Silent omissions are blockers.

### Check 5 — Border Radius Compliance ⛔

The system uses multiple radius values. Verify the component's radius matches the as-built audit in `inspire-design-language/SKILL.md`.

Quick reference: 0px (labeled buttons) · 2px (checkbox, tag, tooltip, quick filters, calendar day) · 4px (cards, boardlets, dialog, toolbar top, progress linear, bottom sheet) · 8px (tray card) · 9999px (icon-only buttons, toggle, progress capsule).

Any deviation from the as-built table must be documented in the spec with a reason.

### Check 6 — Dark Mode Completeness ⛔

Every color token must have an explicit TDK value. Blank or missing TDK values are blockers.

### Check 7 — Token Naming Convention ⛔

Component vars must follow `--[component]-[element]-[property]-[state]`.

Blockers:
- COMPONENTS collection palette aliases used as terminal values
  (`--generic/theme/theme-80`, `--all-theme-50`, `--generic/danger/danger-100`)
  must be replaced with their SHARED SEMANTIC equivalents.

Not a Check 7 violation:
- Cross-component borrows (e.g. `--input/hover-bg` used in Chat) → that's Check 3.
- Correct SHARED SEMANTIC paths (`--text/default`, `--colors/brand/brand-100`) are valid.

### Check 8 — Auto-layout & Resize Compliance ⛔

| Sub-check | Rule |
|---|---|
| Auto-layout coverage | Every container with more than one child must use auto-layout. |
| Sizing modes | `Fill` for stretch, `Hug` for wrap, `Fixed` only when intentionally locked. |
| Min/max width | Required when the component spec defines responsive behavior. |
| Resize smoke test | Stretch horizontally and vertically; confirm text reflows, icons stay anchored, spacing holds. |

| Status | Meaning |
|---|---|
| ✅ PASS | Auto-layout throughout, sizing modes correct, min/max set where needed |
| ⛔ FAIL | Multiple children with absolute positioning; incorrect sizing mode; missing min/max where required |
| ⚠️ PARTIAL | Auto-layout applied but sizing modes wrong or min/max missing |
| N/A | Single-layer or purely decorative component |

### Check 9 — Accessibility Baseline

Run design-level checks when auditing Figma. Run code-level checks when
auditing an HTML prototype. Both sets run on a full acceptance check.

**Design-level:**

| Item | Rule | Status |
|---|---|---|
| Text contrast | 4.5:1 minimum | ✅ / ⛔ |
| UI element contrast | 3:1 minimum (borders, icons, toggle states) | ✅ / ⛔ |
| Color-only state | Paired with icon, shape, or text | ✅ / ⛔ |
| Text labels | All interactive elements have visible or announced label | ✅ / ⚠️ |
| Touch targets | 24×24px minimum | ✅ / ⚠️ |

**Code-level:**

| Item | Rule | Status |
|---|---|---|
| Icon-only `aria-label` | Present on all icon-only buttons | ✅ / ⚠️ |
| Form field labels | `<label>` or `aria-label` on all inputs | ✅ / ⚠️ |
| Keyboard access | Tab/Enter/Space/Arrow work as expected | ✅ / ⚠️ |
| ARIA state | `aria-expanded`, `aria-selected`, etc. where applicable | ✅ / ⚠️ |
| Focus ring | `outline: 2px dashed var(--border/focus)` visible | ✅ / ⚠️ |
| Disabled behavior | `cursor: not-allowed`, no `pointer-events: none` | ✅ / ⚠️ |

---

### Acceptance report format

```
# Acceptance Check — [Component Name]
Date: [YYYY-MM-DD]
Spec: components/[id]/[id].md
Reviewer: [name or "self-review"]

## 1. Semantic Variable Compliance
| Token | ADK hex | TDK hex | Status | Action |
...

## 2. Spacing Compliance
| CSS Variable | Value | SPACING alias | Status |
...

## 3. Cross-Component Variable Borrowing
None found ✅  OR  ⛔ [variable] — belongs to [component], used in [this component]

## 4. State Completeness
| State | Present | Notes |
...

## 5. Border Radius Compliance
Compliant ✅  OR  ⛔ [element] uses [value] — not documented

## 6. Dark Mode Completeness
All tokens have TDK values ✅  OR  ⛔ [token] — TDK value missing

## 7. Token Naming Convention
Compliant ✅  OR  ⛔ [token] — uses generic alias directly

## 8. Auto-layout & Resize
| Sub-check | Status | Notes |
...

## 9. Accessibility Baseline
### Design
| Item | Status | Notes |
...
### Code
| Item | Status | Notes |
...

## Summary
PASS — ready for Figma binding and registry entry
OR
FAIL — [N] blockers must be resolved before acceptance
```

---

## Known deferred items

These are explicitly deferred — do not flag them as blockers in acceptance checks.

| Item | Status | Reason |
|---|---|---|
| Button horizontal padding values | Estimated | Requires full Figma button component refactor before values can be confirmed. Marked "Estimated" in spec. |
| Surface/Hover, Surface/Subtle, all Border/* (except Focus), Icon/*, Status/*, Brand/* | UNSET | Placeholder values in Figma. Do not bind until defined. |

---

## Skill registry

| Skill | Command | Type | Status |
|---|---|---|---|
| inspire-core | (reference only) | Foundation | ✅ Active |
| new-component | `/new-component` | Generator | ✅ Active |
| inspect-spacing | `/inspect-spacing` | Validator | ✅ Active |
| inspire-design-language | (reference only) | Design Language | ✅ Active |
| inspire-compliance | `/inspire-compliance` | Auditor | ✅ Active |
| inspire-patterns | TBD | Pattern | 🔲 Planned (Phase 2) |
