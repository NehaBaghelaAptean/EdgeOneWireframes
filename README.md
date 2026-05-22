# Inspire Design System

**Repo:** [Germanedge/Inspire-Design-System](https://github.com/Germanedge/Inspire-Design-System)  
**Live demos:** [studious-waddle-p376j5k.pages.github.io](https://studious-waddle-p376j5k.pages.github.io/)

A Claude Code skill library for the Edge.One design system (ADK = Astronaut / TDK = Tokyo). Each component ships as a self-contained HTML prototype and a machine-authoritative markdown spec. Figma is the source of truth — prototypes and specs are validated against it.

> Skills run in the **Claude Code CLI only**. They do not work in Claude Desktop or the Claude.ai web UI.

---

## About this repository

This repo serves two purposes: it houses the **Inspire skill library** (Claude Code skills that encode design system rules for AI-assisted work) and the **component output** those skills produce (HTML prototypes + specs). Both live here by design — components are the proof-of-work for the skills, and having them together makes cross-referencing easy during development.

As the component library grows, separating the two into distinct repos (skills repo / component repo) is a likely next step. When that happens, the skills repo will reference the component repo as the canonical example set rather than containing it directly.

---

## Skills

| Skill | Command | Type | What it does |
|---|---|---|---|
| **inspire-core** | (reference) | Foundation | System rules loaded by all other skills — token architecture, typography scale, spacing, grid, elevation, design philosophy, WCAG 2.1 AA a11y baseline, 9-check acceptance process |
| **inspire-design-language** | (reference) | Design Language | As-built corner radius audit, proposed token scale (WIP), stroke tokens, focus state rules, full action hierarchy with decision framework and placement patterns |
| **new-component** | `/new-component` | Generator | Builds a new design system component — HTML prototype + machine-authoritative spec. Optionally creates Figma frames. |
| **inspect-spacing** | `/inspect-spacing` | Validator | Audits spacing token usage in Figma designs (Mode A) or HTML prototypes before engineer handoff (Mode B). Includes confirmed global layout rules and grid system. |
| **inspire-compliance** | `/inspire-compliance` | Auditor | 7-pass A→G compliance audit for any Figma component: context, tokens, typography, spacing, elevation, focus, component-specific rules. |

---

## Structure

```
index.html             — component gallery (live demos index)
components/
  [id]/
    [id].html          — self-contained visual prototype with theme toggle
    [id].md            — machine-authoritative spec (frontmatter + token tables + acceptance criteria)
  README.md            — component registry with live demos and Figma links
.claude/
  skills/
    inspire-core/            — foundation reference loaded by all skills
    inspire-design-language/ — design language reference (corner radii, focus, action hierarchy)
    new-component/           — /new-component generator skill
    inspect-spacing/         — /inspect-spacing validator skill
    inspire-compliance/      — /inspire-compliance audit skill
ROADMAP.md             — platform context, component inventory, inconsistency flags, skill build plan
```

---

## Component Registry

See [components/README.md](components/README.md) for the full registry, live demos, spec links, and Figma references.

---

## Quick start

`Checkbox` and the DevExtreme URL below are examples — replace with your actual component and library URL.

```
/new-component
Component: Checkbox
Library URL: https://js.devexpress.com/Documentation/ApiReference/UI_Components/dxCheckBox/
```

```
/inspect-spacing
Mode: Figma
URL: https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/...?node-id=...
```

```
/inspire-compliance
Component: Button
Node: https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/...?node-id=273-11972
Themes: both
```

---

## Key conventions

- **Source of truth: Figma.** Token values, spacing, and states are defined in the GE — Astronaut Design System Figma file (`yck1tcUXgdQ5aYX6iUAwrO`). Prototypes validate against Figma, not the other way around.
- **Accessibility:** WCAG 2.1 AA baseline. Color contrast (4.5:1 text, 3:1 UI elements), keyboard access, and ARIA requirements are encoded in `inspire-core` and checked in the 9-check acceptance process.
- **Font:** `Inter Tight` (condensed/headings) and `Inter` (body) — loaded from Google Fonts in every prototype. Font migration in the Figma file completed May 2026.
- **Border radius:** Multi-value system — 0px (labeled buttons), 2px (tag, tooltip, checkbox), 4px (cards, boardlets, dialog), 8px (tray card), 9999px (icon-only buttons, toggle, progress capsule). See `inspire-design-language` for the full as-built audit.
- **Dark mode:** `html[data-theme="dark"]` — all components support ADK (light) and TDK (dark).

---

## Prerequisites

- [Claude Code CLI](https://www.npmjs.com/package/@anthropic-ai/claude-code): `npm install -g @anthropic-ai/claude-code`
- Figma MCP (for Figma reads/writes and compliance checks): `/mcp add figma` inside Claude Code
