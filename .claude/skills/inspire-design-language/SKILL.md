---
name: inspire-design-language
description: >
  Design language reference for the Inspire design system. Covers the as-built
  visual design philosophy, overall look and feel, and as-built system state.
  Covers shape language, stroke tokens, focus states, action hierarchy, known
  violations, and WIP proposals for standardization. Load for design-decision
  work, Figma audits, and component authoring where visual language choices
  need justification.
type: reference
skill-type: design-language
version: 1.0.0
last-updated: 2026-05-22
---

# Inspire Design Language

Human-readable design language statement for Inspire. Documents what the system currently is, what's broken, and where it's going.

**Related files:**
- `inspire-core/SKILL.md` — token architecture, typography, spacing, grid, elevation, acceptance checks
- `inspire-compliance/SKILL.md` — 7-pass A→G audit framework
- `components/README.md` — component registry with Figma node links
- `ROADMAP.md` — component inventory, known inconsistencies, prioritized build plan

---

## Current design language snapshot

> Inspire is a flat, enterprise-first design system built on the GE–Astronaut (light) and Tokyo (dark) design systems. It prioritizes clarity and task hierarchy in dense, control-heavy interfaces. The system is functional but has accumulated inconsistencies in corner radii, color contrast, and focus state handling that create friction for accessibility compliance and brand cohesion.

**Visual style**
- Flat design; minimal shadows used only to communicate layering/elevation — not decoration
- Typography-led hierarchy; structure and grouping over borders or decoration
- Enterprise-optimized: dense layouts, many controls per screen, readability over long use

**Known gaps**
- Corner radii have no standardized token scale — 0, 2, 4, 8px, and fully-rounded coexist without a governing rule
- Primary button color (yellow) fails WCAG AA contrast against white backgrounds
- Contrast ratios broadly undocumented and unenforced; additional low-contrast patterns confirmed in active use
- Inset dashed focus indicator is low-visibility and does not reliably communicate focused state
- Action hierarchy visually inverted in practice — Secondary reads as more prominent than Primary
- No explicit Tertiary Button component; the concept exists in guidance only

---

## Corner radii — as-built audit

Manual inspection of published ADK components in the Figma ADS file (`yck1tcUXgdQ5aYX6iUAwrO`).

| Component / area | Corner radius | Notes |
|---|---|---|
| Labeled buttons (Primary / Secondary / Ghost) | **0px** | Desktop and mobile sets |
| Icon-only buttons (Primary / Secondary / Ghost) | **Fully rounded** (9999px) | Circular — half the side length |
| Toolbar shell | **4px top corners; 0px bottom** | `border-radius: 4px 4px 0 0` |
| Toggle switch (track + thumb) | **Fully rounded** (9999px) | Capsule track, circular thumb |
| Checkbox | **2px** | Slight rounding, consistent with icon corner language |
| Calendar — day cell | **2px** | Individual day hit target |
| Tooltip | **2px** | Filled bubble surface |
| Quick Filters | **2px** | `ADK / Quick Filters` |
| Tag (desktop + mobile) | **2px** | Same language as checkbox and Quick Filters |
| Progress bar — capsule/thin | **Fully rounded** (9999px) | `ADK / Progress Capsule Bar` |
| Progress bar — linear (standard) | **4px** | `ADK / Progress Linear Bar`; also used in File Upload |
| Accordion — desktop | **0px** | `ADK / Accordion` |
| Accordion — mobile | **4px** | `ADK / Mobile / Accordion` |
| Boardlet (default shell) | **4px** | `ADK / Boardlet` |
| Boardlet Floating Navigation | **4px** | `ADK / Floating Navigation Boardlet` |
| Bottom Sheet (mobile) | **4px** | `ADK / Mobile / Bottom Sheet` |
| Card (standard family) | **4px** | One variant shows 5px — treat as oversight, normalize to 4px |
| Tray Card | **8px** | Intentionally larger for tile layout |
| File Upload (some surfaces) | **4px** | Not fully consistent across states — treat as open |
| Data grid — column chooser | **4px** | Outer shell only |
| Data grid — filter dropdown menu | **4px bottom; 0px top** | Menu flush with trigger: `border-radius: 0 0 4px 4px` |
| Image carousel — outer wrapper | **4px** | |
| Label (data-viz boxed primitive) | **4px** | `ADK / Label` |
| Planning Board — outer wrapper | **4px** | |

*Extend or correct rows as components ship or radii are reconciled in Figma.*

---

## WIP: Proposed 4-step radius token scale

> **Status: Work in progress.** Directional proposal pending design system alignment and Figma token updates. Do not implement until adopted.

Introduce a **4-step radius token scale** to replace the current ad-hoc values:

| Token | Value | Use |
|---|---|---|
| `radius-xs` | 2px | Small controls: Tag, Tooltip, Checkbox, Quick Filters |
| `radius-sm` | 4px | Default containers and interactive controls: Buttons (labeled), Cards, Boardlets, Inputs, Dialog shells, Toolbar, Progress bar linear |
| `radius-md` | 8px | Large tile surfaces: Tray Card |
| `radius-full` | 9999px | Pill/capsule shapes: Toggle, Icon-only buttons, Progress bar capsule |

**Proposed changes from current as-built:**
- Labeled buttons: 0px → 4px (aligns with card/container language)
- Desktop Accordion: 0px → 4px (unify with mobile treatment)
- Cards: converge all variants on 4px (remove the 5px outlier)

---

## Stroke token system

A six-token system governing all component strokes. Stroke weight is **1px** throughout the component library. **2px is reserved for the focus ring only.**

| Token | Weight | Role |
|---|---|---|
| `stroke-default` | 1px | Resting state for inputs and containers |
| `stroke-strong` | 1px | Selected or active state |
| `stroke-accent` | 1px | Brand/theme token — requires contrast validation before use |
| `stroke-error` | 1px | Validation failure |
| `stroke-disabled` | 1px | Disabled state — reduced opacity |
| `stroke-divider` | 1px | Layout separators and region boundaries |

**Component assignments (proposed):**
- Inputs (text, number, dropdown, date picker, textarea): `stroke-default` at rest; `stroke-error` on validation; `stroke-disabled` when disabled
- Cards & Boardlets: `stroke-strong` on selected/active states
- Containers & panels: `stroke-divider` for layout region definition
- Ghost button (Tertiary): existing outline aligned to `stroke-default`
- Tags & badges: `stroke-default` for outline variants

⚠️ `stroke-accent` note: if this token maps to brand yellow, it inherits the primary button contrast failure. Explicit WCAG contrast validation required before use.

---

## Focus states

### Current as-built behavior

There is **no single global rule** that "Inspire focus is always dashed" or "always solid." Two families coexist:

1. **Variable-based focus outlines (most controls):** Many atoms use named focus color tokens without prescribing dash in prose — e.g. `…/Button Focus Outline`, `Input/Focus outline`, `Links/Link Focus Outline`, `Dropdown/Focus Stroke`. For implementation, treat these as **solid 1px outlines** unless the Figma *Focused* frame explicitly shows a dashed stroke for that component.

2. **Contextual dashed (specific callouts):** Color Usage and companion tables call `1px dashed` in specific situations — validated icon focus (`border-bottom: 1px dashed`), tabs (`inner-border: 1px dashed`), card state cells with explicit dashed vs solid by state. Use dashed **only** where the table or component's Focused cell specifies it.

**Current implementation in prototypes:**
```css
outline: 2px dashed var(--border/focus);
outline-offset: 0px;
```
ADK: `#1a88b7` · TDK: `#7c79ff` (via `--border/focus`).

⚠️ The inset placement makes the focus indicator hard to perceive — it competes with the component's own fill and border.

### WIP: Proposed focus update

> **Status: Work in progress.** Pending team alignment.

**Principle:** Maintain the dashed focus pattern as Inspire's brand-consistent focus language, but move the indicator **outside** the component so it is unambiguous and not obscured by the component's own fill or border.

**Proposed button focus standard:**
- Style: Dashed outline, **2px**, drawn **outside** the component boundary (offset 2px from the component edge)
- Shape: Follows the component's corner radius
- Color: High-contrast focus token — must meet 3:1 contrast against adjacent background
- Trigger: `:focus-visible`

**What changes:** Inset dashed → **offset dashed** (same visual language, dramatically more visible)

**Open questions for team:**
- Dash gap and dash length values — define once, tokenize, apply system-wide
- Focus color token — aligned to brand update or a system neutral?
- Tab inner-border dashed: retain as-is or migrate to offset pattern?

---

## Action hierarchy

### Quick reference table

| Level | Control | When to use |
|---|---|---|
| **Primary** | Primary Button | Task completion, main CTA |
| **Primary** | Primary Icon Action | Icon-only, only when clearly recognizable |
| **Secondary** | Secondary Button | Supporting alternative, not the recommended path |
| **Secondary** | Secondary Icon Action | Supporting icon-only |
| **Tertiary** | Ghost Button | Low emphasis, button affordance still needed |
| **Tertiary** | Link (inline or standalone) | Navigation, drill-in, lowest emphasis |
| **Tertiary** | Overflow / Menu action | Rare, advanced, bulk, destructive, or cluttering actions |

### Decision framework

**Pick the action level:**
- Is this the main task completion? → **Primary**
- Is it a valid alternative/support step? → **Secondary**
- Is it contextual, optional, or dense-layout-friendly? → **Tertiary** (Ghost / Link / Overflow)

**Pick the control type:**
- Does it commit/submit/save? → Button (Primary/Secondary)
- Does it navigate/drill-in? → Link (Inline/Basic)
- Is it rare, advanced, or would create clutter? → Overflow menu
- Is it an icon-only affordance? → Icon Action (Primary/Secondary) *only when recognizable*

**Limits:**
- Prefer **1 Primary** per view region (page main area, dialog footer, etc.)
- Avoid more than 1–2 Secondary actions adjacent to a Primary in the same region

### Placement patterns

**Dialogs:**
- Primary action in the First-Action slot
- Secondary in the Second-Action slot
- Keep tertiary actions out of dialog footers — prefer links in the body or overflow

**Toolbars and row-level actions:**
- Prefer one visible primary-ish action; others become secondary/tertiary
- In tables/rows, default to tertiary (inline actions or overflow) to protect readability

**Destructive actions:**
- Default to tertiary via overflow unless the destructive action is the explicit purpose of the current screen
- If destructive must be prominent: use secondary emphasis + strong confirmation patterns

### ADK component names (Figma library)

**Primary:** `ADK / Button / Primary`, `ADK / Mobile / Button / Primary`, `ADK / Icon / Elements / Primary Action`

**Secondary:** `ADK / Button / Secondary`, `ADK / Mobile / Button / Secondary`, `ADK / Icon / Elements / Secondary Action`
- Dialog slots: `Master / Dialog / Element / First-Action`, `Master / Dialog / Element / Second-Action`

**Tertiary:**
- Ghost: `ADK / Button / Ghost`, `ADK / Mobile / Button / Ghost`
- Links: `ADK / Basic Link`, `ADK / Inline Link`, `ADK / Dropdown-Link`
- Overflow: `ADK / Overflow Menu`, `ADK / Inline Overflow Menu`, `ADK / Overflow / Menu-link / Light`, `ADK / Overflow / Menu-link / Dark`
- Dense action clusters: `ADK / Row-Item / Actions`

### Copy guidance

- Use **verb-first labels**: "Create dashboard", "Save changes", "Apply filter"
- Avoid vague labels: "OK", "Yes", "Do it"
- Prefer outcomes over mechanics: "Publish app" over "Submit"
- Be consistent across surfaces: identical user intent → identical label

---

## Known as-built violations

| Issue | Status | Notes |
|---|---|---|
| Primary button yellow on white | ⚠️ WCAG fail | Contrast ~1.07:1 for UI element; fails 3:1 threshold. Tracked in `ROADMAP.md`. |
| Toggle "on" state brand yellow on white | ⚠️ WCAG fail | Same yellow on white issue |
| Secondary button visually overpowers Primary | ⚠️ Hierarchy inversion | Dark/heavy secondary competes with yellow primary |
| Inset focus indicator | ⚠️ Visibility | Dashed ring inside component boundary competes with component fill |
| No corner radius token scale | ⚠️ Inconsistency | 0, 2, 4, 8px, fully-rounded coexist; proposed fix is the 4-step token scale above |

---

## Industry alignment notes

The proposed updates align with leading design systems:

- **Token-driven shape systems:** Material Design 3 and Ant Design 5 both define corner radius as a token concern. Ant Design 5 exposes `borderRadius`, `borderRadiusSM`, `borderRadiusLG`, `borderRadiusXS` with a 6px default. Our proposed 4-step scale follows the same principle.
- **Offset focus rings:** Material Design 3 and Ant Design 5 both position the focus indicator outside the component boundary via `outline-offset`. Apple HIG requires focus indicators clearly perceivable against adjacent surfaces. Inset focus is treated as an anti-pattern in all three.
- **Outlined components as default affordance:** Outlined Text Field is the default in Material Design 3. Ant Design 5 uses a consistent 1px border (`colorBorder`) as the default for inputs, selects, tables, and cards. Atlassian Design System follows the same pattern.
- **Accessibility:** Material Design 3's color system is built on color roles designed to meet WCAG 2.1 AA by construction. IBM Carbon treats accessibility compliance as a design system gate.
