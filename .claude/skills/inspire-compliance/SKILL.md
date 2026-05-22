---
name: inspire-compliance
description: >
  7-pass compliance checklist for auditing Inspire components in Figma.
  Passes run in order A→G: context, tokens/color, typography, spacing/layout,
  elevation, focus indication, component-specific rules. Produces structured
  findings classified as Compliant, Minor Drift, Spec Mismatch, or Open Question.
  Use after /new-component or for standalone Figma audits.
type: auditor
skill-type: auditor
version: 1.0.0
last-updated: 2026-05-22
---

# Inspire Compliance Checklist

Use this skill to evaluate any Inspire component in Figma for compliance in a repeatable, evidence-based way.

**Primary spec:** `inspire-core/SKILL.md` (token architecture, spacing, grid, elevation, acceptance checks)  
**Design language:** `inspire-design-language/SKILL.md` (corner radii, focus states, action hierarchy, stroke tokens)  
**Figma source:** `GE---Astronaut-Design-System` (file key `yck1tcUXgdQ5aYX6iUAwrO`)

---

## Invocation

```
/inspire-compliance
Component: [ID X.X / component name]
Node: [Figma node link]
Themes: [ADK / TDK / both]
States: [default, hover, focus, active, disabled, validation]
```

---

## Scope setup

Before running passes, confirm:

- **Component name:** `<ID X.X / component name>`
- **Figma file key:** `yck1tcUXgdQ5aYX6iUAwrO` (unless another canonical file is specified)
- **Figma node links:** `<page/frame/variant links>`
- **Theme coverage:** `<ADK light / TDK dark / both>`
- **State coverage:** `<default, hover, focus, active, disabled, validation>`
- **Audit date / owner:** `<date> / <name>`

---

## Compliance passes (required order: A → G)

### A. Context and Intended Use

- Confirm component purpose aligns with product intent in `inspire-core` §1 (product context, Creative North Star).
- Confirm usage context is correct (dashboard, boardlet, dialog, form, etc.).
- Confirm no scope drift from related components (for example link vs button vs content action).
- Cross-reference the component's ID against the component registry in `components/README.md`.

### B. Tokens and Color Semantics

- Verify token usage against the SHARED SEMANTIC collection in `inspire-core`.
- Check semantic color roles (Danger, Warning, Success, Note) are used correctly.
- Check ADK/TDK theme consistency and any documented variant exceptions.
- **Contrast (WCAG 2.1 AA minimum):**
  - Normal text: **4.5:1** against background
  - Large text and UI components: **3:1**
  - Do not assume dark theme = accessible — audit both themes
- **Priority contrast failures to check:** Primary button label, disabled state text, placeholder text in inputs, Ghost button labels on light surfaces
- Flag UNSET tokens (do not bind to placeholder `Surface/Subtle`, `Border/Default`, `Icon/*`, etc.)
- Flag COMPONENTS palette aliases used as terminal values (`--generic/theme/theme-80`, `--all-theme-50`)

### C. Typography

- Verify text styles against the type scale in `inspire-core`:
  - Family (Inter Tight for condensed/headings, Inter for body)
  - Size, weight, line-height
- Confirm heading/body/label usage is role-correct for the component.
- Check that underline variants are only used for linked inline text.

### D. Spacing, Layout, and Grid

- Verify local spacing against the Spacing-01–14 scale and SPACING collection (`inspire-core`).
- Verify gap and padding values use confirmed SPACING semantic aliases (`Gap/Gap-08`, `Padding/Padding-24`, etc.) where available.
- For layout-level components: verify page-level rules (24px desktop padding, 8px gap, no max-width).
- Check padding/gap/alignment consistency across states and variants.
- ⚠️ Production docs may reference Bootstrap-derived utility classes (`m-4`, `p-4`) — those are the legacy system. Use SPACING collection variables for new components.

### E. Elevation and Surfaces

- Verify shadows/surface layering against the elevation table in `inspire-core`:
  - `Elevation/ADK Base`, `ADK Height`, `ADK Level 3`, `ADK Level 4`, `ADK Depth`
- Confirm elevation intent matches interaction/state changes.
- Verify tonal nesting follows the 4-level surface hierarchy (Base/Sections/Interactive/Accents).
- Do not use elevation as decoration — only for conveying stacking and focus.

### F. Focus Indication (keyboard)

- Verify **Focused / Focus** variants in Figma match implementation for keyboard users (`focus-visible` where product allows).
- **Default assumption for most controls:** solid focus stroke from published tokens (e.g. `…/Button Focus Outline`, `Input/Focus outline`).
- **Use dashed only** where the Color Usage matrix or the component's Focused cell specifies it (validated icon: `border-bottom: 1px dashed`; tabs: `inner-border: 1px dashed`).
- Current prototype implementation: `outline: 2px dashed var(--border/focus); outline-offset: 0px`
- ⚠️ The inset dashed ring is the current standard but is flagged as low-visibility. See `inspire-design-language` for the proposed offset dashed approach.
- Do not invent a new focus pattern per screen — any deviation is non-compliant until the design system is updated.

### G. Component-Specific Rules

- Validate variant matrix and state behavior against the component section in `DESIGN.md §7`.
- Verify corner radius matches the as-built audit table in `inspire-design-language/SKILL.md`.
- Verify action controls follow the action hierarchy in `inspire-design-language/SKILL.md` (one Primary per region, etc.).
- Verify any known caveats in `GOVERNANCE.md` are either respected or explicitly flagged.

---

## Findings classification

Use one label per finding:

| Classification | Meaning |
|---|---|
| **Compliant** | Matches spec as written |
| **Minor Drift** | Copy/metadata/link/editorial mismatch with no visual/behavioral spec break |
| **Spec Mismatch** | Token/state/layout/behavior violates canonical spec |
| **Open Question** | Conflicting or incomplete source-of-truth; decision required |

---

## Evidence log (fill per finding)

```
- Finding ID: <local id, e.g. F1>
- Type: <Compliant / Minor Drift / Spec Mismatch / Open Question>
- Pass: <A / B / C / D / E / F / G>
- Where: <Figma node link>
- Spec reference: <inspire-core section or DESIGN.md section>
- What was observed: <short factual statement>
- Expected: <short expected statement>
- Recommendation: <fix or decision needed>
```

---

## Disposition rules

- Concrete mismatch → add/update a row in `GOVERNANCE.md` under the relevant mismatch section.
- Unresolved/ambiguous → add to **Open Questions** in `GOVERNANCE.md`.
- Only update `DESIGN.md` or `inspire-core` when canonical spec text itself must change.

---

## Audit summary template

```
# Inspire Compliance Audit — [Component Name]
Date: [YYYY-MM-DD]
Component: [ID X.X / name]
Figma node: [fileKey / nodeId]
Themes: [ADK / TDK / both]
States: [list]

## Passes

### A. Context and Intended Use
[findings or "No issues found"]

### B. Tokens and Color Semantics
[findings or "No issues found"]

### C. Typography
[findings or "No issues found"]

### D. Spacing, Layout, and Grid
[findings or "No issues found"]

### E. Elevation and Surfaces
[findings or "No issues found"]

### F. Focus Indication
[findings or "No issues found"]

### G. Component-Specific Rules
[findings or "No issues found"]

## Result counts
- Compliant: <n>
- Minor Drift: <n>
- Spec Mismatch: <n>
- Open Question: <n>

## Governance updates made
<Dxx rows and/or open-question bullets added, or "None">

## Spec updates needed
<Yes + note, or No>
```

---

## Quick starter prompt

```
Audit <component> in Figma for Inspire compliance using /inspire-compliance.
Load inspire-core and inspire-design-language as reference.
Check passes A→G in order: context, tokens/color, typography, spacing/layout,
elevation, focus, component-specific rules.
Classify findings as Compliant, Minor Drift, Spec Mismatch, or Open Question.
Record governance updates needed.
```
