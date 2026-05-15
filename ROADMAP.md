---
name: inspire-skills-roadmap
description: >
  Platform context, complete component inventory, known inconsistencies,
  and prioritized roadmap for building Inspire Design System skills — the
  machine-readable standards that govern AI-led component development and
  App Composer application design on the Edge.One platform.
---

# Inspire Design System — Skills Roadmap
**Platform:** Edge.One by Germanedge  
**Design System:** Inspire (ADK = Astronaut / TDK = Tokyo)  
**Skill format:** Claude Code CLI (`/skill-name`)  
**Output:** HTML prototype + machine-authoritative markdown spec  
**Maintained by:** UX, Germanedge

---

## What this is and why it exists

Inspire is Germanedge's open-source design system. It powers the UI of
Edge.One — an enterprise platform built around **App Composer**, a no-code/
low-code environment that lets authorized users visually build dashboards and
applications from pre-built components.

The design system spans two directions:

- **Toward code** — HTML prototypes and specs that developers implement
- **Toward App Composer** — component and pattern definitions that govern how
  dashboards are built in the no-code environment

Skills in this library serve both directions. A skill for a component like
Button encodes the visual contract between Figma, the HTML prototype, and the
App Composer configuration panel. A pattern skill like Dashboard Layout encodes
the structural rules for how App Composer dashboards should be composed.

**Source of truth hierarchy:**
1. **Figma** — variable values, component structure, spacing, states
2. **HTML prototypes** — the living reference implementation
3. **Markdown specs** (`.md`) — the machine-authoritative contract
4. **Docs site** (`e1-dev.k8s.myapp.de/help-and-resources/`) — usage guidance for App Composer; lags behind design. When docs conflict with Figma/prototype, Figma wins and the docs need updating.

**Without these skills**, AI-assisted development will:
- Build components with the wrong size tiers, tokens, or states
- Assemble dashboards that violate action hierarchy or boardlet rules
- Miss dark mode (Tokyo theme) on any component that isn't explicitly checked
- Introduce hardcoded values instead of design token references
- Create inconsistencies between what the docs site says and what Figma defines

**With these skills**, it will do none of those things — without a designer
in the room.

---

## Themes

| Theme | Code name | Context |
|---|---|---|
| Astronaut | ADK (light) | Default / light mode |
| Tokyo | TDK (dark) | Dark mode |

> **Note on naming:** The docs site uses "Astronaut" and "Tokyo" as the
> official theme names. Internally in specs and prototypes we use ADK/TDK
> as the shorthand. Both refer to the same themes.

---

## Complete component inventory

Sourced from `e1-dev.k8s.myapp.de/help-and-resources/` — the official
Edge.One platform documentation.

### Containers
Accordion · Boardlet · Card · Grid Container · Section · Tab · Vertical Tab

### General
Button · Icon · Label · Link · Overflow Menu · Title

### Data Display
Attachment Viewer · Document Viewer · IFrame · Image Displayer · Image Point Viewer ·
List · Pivot Grid · Table · Tree View · Video Player

### Charts
Box Plot · Gantt · Histogram · Line · Stacked Bar

### Data Entry
Checkbox · Combobox · Date Picker · Date Range Picker · File Upload · Files Table ·
Form · Input · Lookup Input · Multi Select · Number Input · Radio Group ·
RFID Scanner · Single Select · Table Selection · Tabs Form · Textarea ·
Toggle Switch · Translation Input · Translation Textarea · Visual Codes Scanner

### Feedback
Inline Notification · Progress Bar · Progress States · Tooltip · Validation

### Navigation
Dashboard Navigation

### Specialized
Calendar · Chat · Clock · Code Editor · Countdown · Date Interval Counter ·
Kanban Board · Karma · Pictogram · Raster · Ruler · Static Boardlet Wrapper · Tag

---

## Current build status

| Component | Skill | Prototype | Spec | Figma |
|---|---|---|---|---|
| Slider | — | ✅ Draft | ✅ Draft | ✅ |
| Filter Builder | — | ✅ Draft | ✅ Draft | ✅ |
| Button | — | ✅ Draft | ✅ Draft | ✅ |

No pattern skills exist yet. No core/foundation skill exists yet.

---

## Known inconsistencies — docs to be updated

**Authority:** Figma and the HTML prototypes are the source of truth.
The docs site (`e1-dev.k8s.myapp.de/help-and-resources/`) lags behind the
design system. Inconsistencies listed here mean the **docs need updating**,
not the prototype or Figma.

| # | Component | Inconsistency | Docs (outdated) | Figma / Prototype (authoritative) | Action |
|---|---|---|---|---|---|
| I-01 | Button | Size tier names | `medium`, `large`, `extra_large` | `XS`, `S`, `M`, `XL`, `3L` | Update docs to match Figma size scale |
| I-02 | All | Theme naming | "Astronaut" (light) / "Tokyo" (dark) | ADK (light) / TDK (dark) | Cosmetic — both in use; docs may use either, prototypes use ADK/TDK |
| I-03 | All | Spacing token names | CSS class strings (`row-gap-4`, `p-4`) | SPACING collection variables (`Gap/Gap-08`, `Padding/Padding-24`) | Update docs to reference token names, not raw class strings |
| I-04 | Button | Icon-only variant | Docs say don't replace text with icon-only | Prototype has icon-only circular variant as a supported sub-variant | Update docs to document icon-only as a valid pattern |
| I-05 | All | Token values | No token values or color hex values in docs | Figma SHARED SEMANTIC and COMPONENTS collections | Docs should link to or reference the token system |

---

## Guiding principles for prioritization

1. **Frequency in App Composer dashboards** — components that appear on
   every screen get built first
2. **UX failure risk** — areas where AI defaults to technically correct but
   design-wrong behavior
3. **Pattern before component** — a dashboard layout pattern is more valuable
   than a specialized chart component
4. **Inconsistency surface area** — components with I-XX flags above get
   resolved before their skill is written

---

## Skill build roadmap

### Phase 0 — Foundation (now)
**inspire-core** _(not yet built)_  
The root skill. Covers: what Inspire is, what App Composer is, the ADK/TDK
token architecture, the two-file output format (HTML prototype + MD spec),
border radius rules, font rules, the acceptance check process, and the
one rule that overrides everything else. Every other skill references this.

---

### Phase 1 — Core structural components
These appear on virtually every App Composer dashboard.

**Boardlet** _(not yet built)_  
The primary structural unit of every dashboard. Three variants (Default,
Ghost, Graphic), header/body/footer anatomy, toolbar action limits (max 3
visible + overflow), footer button rules. Highest frequency of any container.

**Button** _(prototype exists, skill not yet written)_  
Resolve I-01 (size tier names) before writing. Rules for Primary/Secondary/
Ghost hierarchy, one primary per dashboard, icon usage, dialog layout rules
(single = full width, two = 50/50, three = 33/33/33).

**Grid Container** _(not yet built)_  
The layout foundation within boardlets. Gap/padding token usage, responsive
behavior, relationship to the SPACING collection.

---

### Phase 2 — Patterns (higher value than individual components)
Pattern skills encode compositional decisions that no single component skill
can capture. These are the most valuable skills in the library.

**Dashboard Layout Pattern** _(not yet built)_  
How to structure a complete dashboard: boardlet placement, grid, primary
action placement, header vs footer vs toolbar actions. The canonical
Edge.One page layout.

**Action Placement Pattern** _(not yet built)_  
The three action categories (Toolbar, Footerbar, Content), hierarchy rules,
reading flow, footer placement (bottom-right), overflow menu thresholds.
Documented in the docs site — encode it as a skill.

**Form Layout Pattern** _(not yet built)_  
Field grouping, label placement, required field conventions, validation
placement, save/cancel position. Aligns with the spacing/layout skill
initially requested.

---

### Phase 3 — Data entry components
Form components have the highest UX failure risk after containers — AI
will build them without understanding the label/validation/state rules
specific to this system.

**Input / Form** · **Single Select / Combobox** · **Checkbox / Radio Group** ·
**Toggle Switch** · **Date Picker** · **Textarea** · **Multi Select**

---

### Phase 4 — Data display
**Table** _(not yet built)_  
The most-used data display component in supply chain software. Row actions
(max 3 including overflow), column types, pagination, empty state.

**List** · **Tree View** · **Pivot Grid**

---

### Phase 5 — Feedback and navigation
**Inline Notification** · **Progress Bar** · **Progress States** · **Tag** ·
**Tooltip** · **Dashboard Navigation**

---

### Phase 6 — Specialized and chart components
**Calendar** · **Charts** (Line, Stacked Bar, Gantt, Histogram, Box Plot) ·
**Kanban Board** · **Chat** · **Accordion** · **Tab / Vertical Tab**

---

## What each skill must include

Every component skill must follow this structure:

1. **What this component is** — one paragraph; what it does and where it lives in App Composer
2. **When to use / When NOT to use** — explicit guidance; no component is for everything
3. **Figma reference** — file key + node ID; the spec is the contract
4. **Prototype reference** — link to live demo on GitHub Pages
5. **Variants** — all documented variants with when to use each
6. **States** — complete state list; missing states are blockers
7. **Token rules** — which SHARED SEMANTIC tokens apply; component-scoped exceptions
8. **Spacing and sizing** — confirmed values from Figma; estimated values flagged
9. **App Composer configuration** — key properties from the docs site; maps to the prototype
10. **What AI must never do** — explicit anti-patterns (encoded from docs + Figma + team knowledge)
11. **Known inconsistencies** — any I-XX flags that apply to this component
12. **Acceptance criteria** — the 10-check acceptance process (from reference_acceptance_criteria.md)

---

## What this roadmap does not cover (yet)

- Accessibility requirements — not yet specified in docs or Figma
- Responsive/mobile behavior — App Composer is primarily desktop
- Animation and transition tokens — not yet defined in the system
- Contribution workflow — how components move from Draft → Accepted
- Third-party component library integration (DevExtreme versions, upgrade path)

---

*Built by the Germanedge UX Guild.*  
*Inspire Design System · Edge.One Platform*
