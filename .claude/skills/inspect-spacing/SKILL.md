---
name: inspect-spacing
description: >
  Spacing and layout validator for the Inspire design system. Two modes:
  (A) Figma Audit — checks whether a Figma design has spacing values correctly
  bound to SPACING collection variables; (B) Code Handoff — cross-references an
  HTML/CSS prototype against Figma-specified spacing values before handing off to
  engineers. Flags mismatches and hardcoded values without halting production.
type: validator
skill-type: validator
version: 1.0.0
last-updated: 2026-05-15
---

# inspect-spacing — Spacing & Layout Validator

Validates spacing and layout token usage in Figma designs and HTML/CSS prototypes.
References `inspire-core` for token architecture and SPACING collection rules.

**Philosophy:** Flag and annotate over halting. Spacing mismatches are warnings,
not blockers. The goal is forward motion with a clear paper trail — not stopped
production.

---

## When to use each mode

| Situation | Mode |
|---|---|
| A new component or layout is being designed in Figma and needs to enter the library | **Mode A — Figma Audit** |
| A component prototype is being handed off to engineers for implementation | **Mode B — Code Handoff** |

---

## Inputs

**Mode A — Figma Audit**
```
/inspect-spacing
Mode: Figma
URL: https://www.figma.com/design/[fileKey]/...?node-id=[nodeId]
```

**Mode B — Code Handoff**
```
/inspect-spacing
Mode: Code
Component: [component-id]
```
If `Mode` is omitted, infer from context: a Figma URL → Mode A, a component name → Mode B.

---

## Status key

Used in all report tables. All statuses allow work to continue — none are hard stops.

| Status | Meaning | Action required |
|---|---|---|
| ✅ BOUND | Value is bound to the correct semantic SPACING alias (`Gap/` or `Padding/`) | None |
| ⚠️ PRIMITIVE | Bound to a SPACING primitive, not a semantic alias | Preferred: swap to semantic alias if one exists; otherwise annotate |
| ⚠️ UNBOUND | A SPACING semantic alias exists for this value but is not being used | Replace with the alias before finalising |
| ⚠️ HARDCODED | Hardcoded px with no SPACING alias available | Document as intentional; create alias if value recurs |
| ⚠️ DRIFT | (Mode B only) Prototype CSS value does not match the Figma-specified value | Reconcile before handoff |
| ⚠️ UNVERIFIED | (Mode B only) CSS variable present in prototype but no Figma binding found | Verify manually |
| ⚠️ MISSING | (Mode B only) Figma binding present but no corresponding CSS variable in prototype | Add to prototype |

---

## Mode A — Figma Audit

### Steps

1. **Parse the URL** — extract `fileKey` and `nodeId`.

2. **Fetch variable bindings** — call `get_variable_defs(fileKey, nodeId)`.
   Also call `get_screenshot` for visual context.

3. **Separate spacing variables** — from the binding map, isolate all entries
   whose key starts with `Gap/`, `Padding/`, or any known spacing-adjacent group
   (e.g. `Elevation/`). Also note any raw numeric values that are not bound.

4. **Classify each value** against the SPACING collection rules from `inspire-core`:
   - Semantic alias (`Gap/Gap-08`, `Padding/Padding-24`) → ✅ BOUND
   - Primitive (a raw numeric not wrapped in a semantic alias) → ⚠️ PRIMITIVE
   - No binding, but a matching semantic alias exists → ⚠️ UNBOUND
   - No binding, no matching alias → ⚠️ HARDCODED

5. **Check against the Pattern Library** (see below) — if the node is a known
   layout pattern, verify the gap/padding values match the established rules.
   Flag any deviation as ⚠️ DRIFT.

6. **Output the report.**

7. **Promote to Pattern Library** — if all values are ✅ BOUND or documented
   ⚠️ warnings, extract the validated spacing rules and add them to the Pattern
   Library section of this file under a new named pattern entry.

---

## Mode B — Code Handoff

### Steps

1. **Locate the component spec** — read `components/[id]/[id].md` for:
   - `figma-file` and `figma-node` from frontmatter
   - `source-url` (DevExtreme or other library URL)

2. **Fetch Figma variable bindings** — call `get_variable_defs` using the
   spec's `figma-file` + `figma-node`.

3. **Read the HTML prototype** — parse `components/[id]/[id].html` for:
   - All `--[component]-*` CSS variables with spacing/sizing values
   - All `gap`, `padding`, `margin`, `width`, `height` property declarations

4. **Cross-reference** — for each spacing value in the prototype:
   - Find the matching Figma binding by value
   - If values match → ✅ BOUND
   - If values differ → ⚠️ DRIFT (note both values)
   - If in prototype but not in Figma → ⚠️ UNVERIFIED
   - If in Figma but absent from prototype → ⚠️ MISSING

5. **If a `source-url` is present** — optionally fetch the library docs URL and
   note any documented dimension constraints (e.g. DevExtreme minimum handle
   size) that may explain hardcoded values.

6. **Output the report.**

---

## Report format

```
# Spacing Audit — [Mode A: Figma / Mode B: Code Handoff]
Date: [YYYY-MM-DD]
Target: [Figma URL or components/[id]/[id].html]
Figma node: [fileKey / nodeId]
Mode: [Figma Audit / Code Handoff]

---

## Spacing variable map

| Element / Layer | Property | Value | SPACING alias | Status | Notes |
|---|---|---|---|---|---|
| [layer name] | gap | 8px | Gap/Gap-08 | ✅ BOUND | — |
| [layer name] | padding | 24px | Padding/Padding-24 | ✅ BOUND | — |
| [layer name] | gap | 12px | — | ⚠️ HARDCODED | No alias; recurs 3× — candidate for new Gap/Gap-12 |
| [layer name] | padding | 16px | Padding/Padding-16 | ⚠️ UNBOUND | Bound to primitive; semantic alias exists |

## Pattern check (Mode A only)

| Pattern | Expected | Actual | Status |
|---|---|---|---|
| Desktop Dashboard Layout — boardlet gap | Gap/Gap-08 (8px) | Gap/Gap-08 (8px) | ✅ MATCH |

## Prototype vs Figma (Mode B only)

| CSS variable | Prototype value | Figma value | Status |
|---|---|---|---|
| --slider-track-height | 4px | 4px | ✅ BOUND |
| --slider-handle-size | 14px | 16px | ⚠️ DRIFT |

---

## Summary

[N] bound · [N] warnings  
Forward motion: YES / PARTIAL

Warnings to resolve before handoff:
- [list each ⚠️ item with the recommended action]

Patterns promoted: [list any new patterns added to the library, or "none"]
```

---

## Global layout rules

Confirmed 2026-05-22. These are the baseline rules for all Inspire layouts.
Reference these in Step 5 of Mode A before checking component-specific patterns.

| Rule | Value | Token | Notes |
|---|---|---|---|
| Page padding — desktop/tablet | 24px | `Padding/Padding-24` | All four sides |
| Page padding — mobile | 16px | `Padding/Padding-16` | All four sides |
| Universal gap (major layout zones, boardlet grid) | 8px | `Gap/Gap-08` | |
| Navigation sidebar — open width | 340px | structural constant | No token |
| Navigation sidebar — default state | hidden | — | Open or closed only; no collapsed/icon state |
| Header height — desktop/tablet | 72px | structural constant | No token |
| Header height — mobile | 64px | structural constant | No token |
| Content width | Always full-bleed | — | No max-width cap at any breakpoint |
| Bottom padding (docs: 72px desktop / 64px mobile) | ⚠️ FLAGGED | do not use | Source mismatch; revisit when footer/action bar behavior is defined |

### Grid system reference

| Orientation | Grid | Gutter |
|---|---|---|
| Landscape (desktop, tablet landscape) | 24 columns × 12 rows | 8px |
| Portrait (tablet portrait, mobile) | 12 columns × 24 rows | 8px |

⚠️ **Conflict D29:** Dashboard docs reference a 16-column / 9-row grid. The canonical spec (`DESIGN.md §5`) defines 24×12 landscape / 12×24 portrait. Use the DESIGN.md values. Flag deviations as ⚠️ DRIFT in audit reports.

---

## Pattern Library

Each entry is a named spacing pattern derived from a validated Figma layout.
New patterns are added here after a Mode A audit passes.

Patterns serve as reference rules for Mode A (deviation check) and for
building new layouts and components.

---

### Pattern: Desktop Dashboard Layout
**Source:** GE — Astronaut Design System · node `21272:87900`  
**Validated:** 2026-05-15  
**Frame size:** 1920 × 1024

This is the canonical full-page desktop layout for an App Composer dashboard.
It establishes the baseline spacing rules for page-level structure.

#### Layout zones

| Zone | Description |
|---|---|
| Top navigation bar | Full-width header: hamburger, breadcrumb, brand, action icons |
| Left navigation panel | ~265px fixed width; contains boardlet sections + full-width CTA button |
| Main content grid | Remaining width; two-row boardlet grid |

#### Confirmed spacing bindings

All values in this frame are bound to semantic SPACING aliases — no hardcoded
pixel values found.

| Role | SPACING alias | Value | Applied to |
|---|---|---|---|
| Page layout — column gap | `Gap/Gap-24` | 24px | Between left nav panel and main content area |
| Page layout — major section gap | `Gap/Gap-48` | 48px | Between major layout zones |
| Boardlet grid — gap between boardlets | `Gap/Gap-08` | 8px | Gap between individual boardlets in the grid |
| Boardlet internal padding — standard | `Padding/Padding-24` | 24px | Default content padding within a boardlet |
| Boardlet internal padding — large | `Padding/Padding-48` | 48px | Hero or feature boardlet padding |
| Component padding — medium | `Padding/Padding-16` | 16px | Mid-density component internal spacing |
| Component padding — dense | `Padding/Padding-08` | 8px | Compact / nested element spacing |

#### Non-spacing variables confirmed in this frame

These are included for reference — they confirm which tokens are active at the
page level and may be relevant when building layout-level components.

| Variable | Value | Role |
|---|---|---|
| `Colors/Theme/Theme 10` | #f2f2f2 | Page background |
| `Colors/Theme/Theme 20` | #e7e6e6 | Panel/divider surfaces |
| `Colors/Theme/Theme 30` | #cfcece | Borders, rule lines |
| `Boardlets/Boardlet Background` | #ffffff | Boardlet card surface |
| `Elevation/ADK Base` | DROP_SHADOW 0 1 4 | Default boardlet shadow |
| `Elevation/ADK Height` | DROP_SHADOW 0 1 8 | Elevated boardlet shadow |
| `Colors/Brand/Brand 100` | #fcd515 | Brand accent (navigation overline) |

#### Rules derived from this pattern

When building or validating a desktop dashboard layout:

1. Column gap between the nav panel and main content **must** use `Gap/Gap-24`.
2. Gap between individual boardlets in the grid **must** use `Gap/Gap-08`.
3. Default boardlet content padding **must** use `Padding/Padding-24`.
4. Any spacing value that doesn't resolve to a semantic `Gap/` or `Padding/` alias
   **must** be flagged as ⚠️ and documented before the layout can be promoted.

---

## Adding a new pattern

After a Mode A audit passes on a new Figma layout:

1. Give the pattern a short descriptive name (e.g. `Form Layout`, `Dialog`).
2. Note the source node ID, date validated, and frame dimensions.
3. List the confirmed spacing bindings in the same table format above.
4. List the rules derived from those bindings.
5. Append the entry to the Pattern Library section above.

Do not subdivide into separate files until the Pattern Library exceeds ~5 patterns
or patterns need to cross-reference each other. Keep it flat.

---

## Relationship to inspect-core and other skills

- **inspire-core** — defines the SPACING collection structure, confirmed semantic
  aliases, and the two-tier system (primitives vs semantic). Always load it for
  the current alias list before running an audit.
- **new-component** — Mode B of this skill runs after a new component prototype
  is complete, as a pre-handoff gate. It does not replace the new-component
  acceptance check — it supplements it with a spacing-specific deep-dive.
- **App Composer compiled JSON** (future Phase 7) — when that validation layer is
  built, Mode C will extend this skill to cross-check compiled JSON output against
  the spacing rules established in the Pattern Library.
