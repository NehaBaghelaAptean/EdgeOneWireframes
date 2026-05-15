# Inspire Design System

A Claude Code skill library for the Edge.One design system (ADK = Astronaut / TDK = Tokyo). Each component ships as a self-contained HTML prototype and a machine-authoritative markdown spec. Figma is the source of truth — prototypes and specs are validated against it.

> Skills run in the **Claude Code CLI only**. They do not work in Claude Desktop or the Claude.ai web UI.

## Skills

| Skill | Command | Type | What it does |
|---|---|---|---|
| **inspire-core** | (reference) | Foundation | System rules loaded by all other skills — token architecture, ADK/TDK, WCAG 2.1 AA a11y baseline, Germanedge styling constraints, 9-check acceptance process |
| **new-component** | `/new-component` | Generator | Builds a new design system component — HTML prototype + machine-authoritative spec. Optionally creates Figma frames. |
| **inspect-spacing** | `/inspect-spacing` | Validator | Audits spacing token usage in Figma designs (Mode A) or HTML prototypes before engineer handoff (Mode B). Flags mismatches without halting production. |

## Structure

```
components/
  [id]/
    [id].html        — self-contained visual prototype with theme toggle
    [id].md          — machine-authoritative spec (frontmatter + token tables + acceptance criteria)
  README.md          — component registry with live demos and Figma links
.claude/
  skills/
    inspire-core/    — foundation reference loaded by all skills
    new-component/   — /new-component generator skill
    inspect-spacing/ — /inspect-spacing validator skill
ROADMAP.md           — platform context, component inventory, inconsistency flags, skill build plan
```

## Component Registry

See [components/README.md](components/README.md) for the full registry, live demos, spec links, and Figma references.

## Quick start

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

## Key conventions

- **Source of truth: Figma.** Token values, spacing, and states are defined in the GE — Astronaut Design System Figma file (`yck1tcUXgdQ5aYX6iUAwrO`). Prototypes validate against Figma, not the other way around.
- **Accessibility:** WCAG 2.1 AA baseline. Color contrast (4.5:1 text, 3:1 UI elements), keyboard access, and ARIA requirements are encoded in `inspire-core` and checked in the 9-check acceptance process.
- **Border radius:** `0px` everywhere (square corners). Documented exceptions: slider track `2px`, button icon-only `9999px`.
- **Font:** `Inter Tight` for condensed/headings, `Inter` for body.
- **Dark mode:** `html[data-theme="dark"]` — all components support ADK (light) and TDK (dark).

## Prerequisites

- [Claude Code CLI](https://www.npmjs.com/package/@anthropic-ai/claude-code): `npm install -g @anthropic-ai/claude-code`
- Figma MCP (for Figma reads/writes and acceptance checks): `/mcp add figma` inside Claude Code
