---
name: inspire-core
description: >
  Foundation reference for all Inspire design system skills. Encodes system
  philosophy, token architecture, ADK/TDK rules, Germanedge styling constraints,
  Figma file references, GitHub Pages requirements, and the 8-check acceptance
  process. Load this before any component or pattern skill runs.
type: reference
skill-type: foundation
version: 1.0.0
last-updated: 2026-05-15
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

**Global rule: `0px` everywhere — square corners.**

Documented exceptions (do not re-litigate these):
- Slider track: `2px`
- Chat list item: `2px`
- Button icon-only variant: `9999px` (circular)

Any new deviation must be documented in the spec's Open Questions with a reason
before it can be accepted.

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

Global rule: `0px` everywhere.
Any deviation must be documented in the spec with a reason.
Known documented exceptions: slider track (2px), chat list item (2px), button icon-only (9999px).

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
| inspire-patterns | TBD | Pattern | 🔲 Planned (Phase 2) |
