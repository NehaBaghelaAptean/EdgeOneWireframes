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

**Validation chain:**  
Figma → HTML/CSS prototypes → *(future)* App Composer compiled JSON output

The HTML/CSS layer is the current focus. It defines the contracts that App Composer must honor when it compiles a dashboard to JSON in the low-code environment. Validating the compiled JSON output is a future phase — once the HTML layer is solid, the JSON validation follows the same rules.

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

**Source of truth:** Figma layer structure confirmed 2026-05-15 from the
GE - Astronaut Design System file. Organized by the file's own section IDs.
Docs-site names noted where they differ.

### ID 1 — Icons
Icons 24px · Icons 16px · Other Icons & Logo

### ID 2 — Actions / Navigation
Button · Link · Content Switch · Breadcrumb · Navigation Header Bar ·
Navigation Panel · Cell Component · Bottom Navigation ·
Tree (Structured List) · Toolbar · Navigation Menu

### ID 3 — Forms
Text Input · Text Area · Dropdown · Toggle · Number Input · Checkbox · Radio ·
File Upload · Date Picker & Range Picker · Scan Input · Form Element ·
Code Editor · Inline Input · Image Carousel

### ID 4 — Dialog / Popover
Dialog & Modal · Overflow Menu · Tooltip · Notifications

### ID 5 — Containers
Accordion · Boardlet · Bottom Sheet · Card

### ID 6 — Table
Data Grid (Tables) · Filters · Scrollbar

### ID 7 — Display
Browser Bars · Camera · Clock · Empty States · Document Viewer · Image Raster ·
Progress Indicator · Tag · Loader · Global Search · Progress Bar · Rule ·
Video Player

### ID 8 — Data Visualization
Data Lines · Data Points · Label · Planning Board · Charts · Karma

---

### Cross-reference: docs site names vs Figma names

| Figma (authoritative) | Docs site name | Match? |
|---|---|---|
| Text Input | Input | ✅ same |
| Text Area | Textarea | ✅ same |
| Dropdown | Combobox / Single Select / Dropdown | ⚠️ multiple docs names — one Figma component |
| Toggle | Toggle Switch | ✅ same |
| Scan Input | RFID Scanner / Visual Codes Scanner | ⚠️ one Figma component, two docs names |
| Dialog & Modal | Dialog | ✅ confirmed one component (resolves I-06) |
| Notifications | Inline Notification + Toast Notification | ⚠️ one Figma section, split in docs |
| Bottom Sheet | — | ❌ not in docs at all |
| Data Grid | Table | ✅ same |
| Filters | Filter Builder | ⚠️ may be the same — needs confirmation |
| Progress Indicator | Progress States | ✅ same |
| Progress Bar | Progress Bar | ✅ same |
| Loader | — | ❌ not in docs (separate from Progress Bar/Indicator) |
| Rule | Ruler | ⚠️ name differs |
| Image Raster | Raster | ✅ same |
| Planning Board | Kanban Board | ⚠️ different names — same component? |
| Content Switch | — | ❌ not in docs |
| Navigation Header Bar | Dashboard Navigation | ⚠️ name differs |
| Navigation Panel | — | ❌ not in docs |
| Cell Component | — | ❌ not in docs |
| Bottom Navigation | — | ❌ not in docs |
| Toolbar | — | ❌ not in docs |
| Navigation Menu | — | ❌ not in docs |
| Form Element | Form | ⚠️ name differs |
| Inline Input | Input | ⚠️ may be a variant of Text Input |
| Image Carousel | — | ❌ not in docs |
| Scrollbar | — | ❌ not in docs |
| Browser Bars | — | ❌ not in docs |
| Camera | — | ❌ not in docs |
| Global Search | — | ❌ not in docs |
| Data Lines · Data Points · Label | — | ❌ chart sub-components, not in docs |

---

## Current build status

| Component | Skill | Prototype | Spec | Figma |
|---|---|---|---|---|
| Slider | — | ✅ Draft | ✅ Draft | ✅ |
| Filter Builder | — | ✅ Draft | ✅ Draft | ✅ |
| Button | — | ✅ Draft | ✅ Draft | ✅ |

No pattern skills exist yet. No core/foundation skill exists yet.

---

## Figma library — confirmed component inventory

Sourced from `GE - Astronaut Design System` library via Figma MCP search,
2026-05-15. Components appear under two prefixes: `ADK /` (published
component set) and `Master /` (master component, used as base for ADK variants).

| Component | Figma name(s) | Notes |
|---|---|---|
| Button | `ADK / Button / Primary` · `ADK / Button / Secondary` · `ADK / Button / Ghost` · `Master / Button / Primary / Small` · `Master / Button / Secondary / Small` | Small sub-variant confirmed in Master layer |
| Input | `ADK / Input` · `ADK / Mobile / Input` | Desktop + mobile variants |
| Textarea | `ADK / Input-area` | Named "Input-area" in Figma, "Textarea" in docs |
| Dropdown | `ADK / Dropdown` | Single-select |
| Dialog | `ADK/ Dialog` · `Master / Modal` | Two names — needs resolution (see I-06) |
| Tooltip | `ADK / Tooltip` | |
| Tag | `ADK / Tag` · `Master / Tag` | |
| Icon | `ADK / Icon / 24x24 / *` | Named icons: Add, Close, Delete, Edit, Import, Info, Menu, More, Reset, Search |
| Boardlet | `Master / Boardlet / Header` | Only header found; full boardlet may be on a different page |
| Card | `Master / Card` · `Master / Card / Top-bar` | |
| Breadcrumb | `Master / Breadcrumb` | |
| Tree | `Master / Tree` · `ADK / Tree / New Component` | Two versions — active vs legacy unclear |
| Calendar | `Master / Calendar / Monthsfield` · `Master / Dayfield` | Month field + day field sub-components |
| Toast / Notification | `Master / ToastNotification / Element / Content` | |
| Inline Notification | `Master/ ADK / Success` · `Master/ ADK / Warning` | Named by state, not as a component |
| Progress State | `Master / Progress State Mobile` | Mobile-labelled — desktop version may exist |
| Text | `Master / Text` | Typography component |
| Tile | `Master / Tile` | Not in docs (see I-10) |
| Column Chooser | `ADK / Column-chooser / 3-columns` | Not in docs (see I-11) |
| PB / Cell + List | `Master/PB/Cell` · `Master/PB/List` | PB meaning unknown — Progress Bar? Pick Board? (see I-12) |
| Slider | Confirmed from prior work (node `22145:141089`) | |
| Filter Builder | Confirmed from prior work (node `22271:11752`) | |

---

## Known inconsistencies — docs to be updated

**Authority:** Figma and the HTML prototypes are the source of truth.
The docs site (`e1-dev.k8s.myapp.de/help-and-resources/`) lags behind the
design system. Inconsistencies listed here mean the **docs need updating**,
not the prototype or Figma.

### Naming and scope mismatches

| # | Component | Inconsistency | Docs (outdated) | Figma (authoritative) | Action |
|---|---|---|---|---|---|
| I-01 | Button | Size tier names | `medium`, `large`, `extra_large` | `XS`, `S`, `M`, `XL`, `3L` | Update docs to match Figma size scale |
| I-02 | All | Theme naming | "Astronaut" (light) / "Tokyo" (dark) | ADK (light) / TDK (dark) | Cosmetic — both acceptable; prototypes use ADK/TDK |
| I-03 | All | Spacing token names | CSS class strings (`row-gap-4`, `p-4`) | SPACING collection variables (`Gap/Gap-08`, `Padding/Padding-24`) | Update docs to reference token names |
| I-04 | Button | Icon-only variant | Docs say don't replace text with icon-only | Prototype has icon-only circular variant as a supported sub-variant | Update docs to document icon-only as valid |
| I-05 | All | Token values | No token values or color hex values in docs | Figma SHARED SEMANTIC and COMPONENTS collections are the source | Docs should link to token system |
| I-06 | Dialog / Modal | ~~Two names for one component?~~ | "Dialog" | `ADK/ Dialog` / `Master / Modal` | ✅ Resolved — Figma layer ID 4.1 is "Dialog & Modal" confirming one component, two names. Docs should use "Dialog & Modal" |
| I-07 | Textarea | Component name | "Textarea" | `ADK / Input-area` | Update docs or align Figma name — pick one |
| I-08 | Inline Notification | Named by state not component | "Inline Notification" (one component) | `Master/ ADK / Success`, `Master/ ADK / Warning` (individual state components) | Confirm if these should be one component with variants or stay separate |
| I-09 | Progress State | Mobile-only label | "Progress States" (no platform qualifier) | `Master / Progress State Mobile` | Confirm if desktop variant exists; if not, docs should note mobile-only |

### In Figma but not in docs

| # | Component | Figma name | Notes |
|---|---|---|---|
| I-10 | Tile | `Master / Tile` | Dashboard tile component — undocumented |
| I-11 | Column Chooser | `ADK / Column-chooser / 3-columns` | Sub-component of Data Grid — undocumented separately |
| I-12 | Planning Board cells | `Master/PB/Cell` · `Master/PB/List` | PB = Planning Board (ID 8.4); sub-components of the Planning Board |
| I-23 | Bottom Sheet | ID 5.3 in Figma | Container component — entirely absent from docs |
| I-24 | Content Switch | ID 2.3 in Figma | Navigation component — absent from docs |
| I-25 | Navigation Panel | ID 2.6 in Figma | Absent from docs |
| I-26 | Cell Component | ID 2.7 in Figma | Absent from docs — purpose unclear |
| I-27 | Bottom Navigation | ID 2.8 in Figma | Absent from docs |
| I-28 | Toolbar | ID 2.10 in Figma | Absent from docs |
| I-29 | Navigation Menu | ID 2.11 in Figma | Absent from docs |
| I-30 | Inline Input | ID 3.13 in Figma | Absent from docs — possibly a variant of Text Input |
| I-31 | Image Carousel | ID 3.14 in Figma | Absent from docs |
| I-32 | Scrollbar | ID 6.3 in Figma | Absent from docs |
| I-33 | Browser Bars | ID 7.1 in Figma | Absent from docs |
| I-34 | Camera | ID 7.2 in Figma | Absent from docs |
| I-35 | Loader | ID 7.9 in Figma | Absent from docs — distinct from Progress Bar and Progress Indicator |
| I-36 | Global Search | ID 7.10 in Figma | Absent from docs |

### In docs but not found in Figma

These components appear in the docs site but were not returned in any Figma
library search. They may exist under different names, on unpublished pages,
or may not yet have Figma definitions.

| # | Component | Docs name | Status |
|---|---|---|---|
| I-13 | Accordion | Accordion | Not found in Figma searches |
| I-14 | Grid Container | Grid Container | Not found in Figma searches |
| I-15 | Tab / Vertical Tab | Tab · Vertical Tab | Not found in Figma searches |
| I-16 | Table | Table | Not found in Figma searches |
| I-17 | Checkbox / Radio / Toggle | Checkbox · Radio Group · Toggle Switch | Not found in Figma searches |
| I-18 | Select variants | Single Select · Multi Select · Combobox · Lookup Input | Not found in Figma searches |
| I-19 | Overflow Menu | Overflow Menu | Not found in Figma searches |
| I-20 | Kanban Board | Kanban Board | Not found in Figma searches |
| I-21 | Charts | Box Plot · Gantt · Histogram · Line · Stacked Bar | Not found in Figma searches |
| I-22 | Specialized inputs | Date Range Picker · Number Input · File Upload · RFID Scanner | Not found in Figma searches |

> **Note on I-13 to I-22:** Figma search returns a limited result set. These
> components may exist in the file on pages not currently indexed by the search
> tool. Absence from search results is not confirmed absence from Figma —
> each should be verified by browsing the Figma file directly before concluding
> it is missing.

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

### Phase 0 — Foundation ✅ Complete
**inspire-core** — `.claude/skills/inspire-core/SKILL.md`  
The root skill. Covers: what Inspire is, what App Composer is, the ADK/TDK
token architecture, the two-file output format (HTML prototype + MD spec),
border radius rules, font rules, the acceptance check process, GitHub Pages
requirements, SHARED SEMANTIC token list, and the one rule that overrides
everything else. Every other skill references this.

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

### Phase 7 — App Composer compiled JSON validation *(future)*
App Composer compiles dashboard configurations to JSON. This phase extends
the validation chain from HTML/CSS contracts down to the runtime output of the
low-code environment — verifying that what App Composer generates honors the
same spacing, token, and layout rules defined in the HTML prototypes.

Prerequisite: the HTML/CSS layer (Phases 0–6) must be stable before this
phase begins. The JSON schema and the property names App Composer uses will
inform what checks are possible.

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
- App Composer compiled JSON validation — tracked in Phase 7; begins after HTML/CSS layer is stable

---

*Built by the Germanedge UX Guild.*  
*Inspire Design System · Edge.One Platform*
