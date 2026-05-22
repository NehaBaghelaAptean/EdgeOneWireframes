# Inspire Design System — Skill Library Update

We've shipped the first version of the Inspire skill library — a set of Claude Code skills that encode our design system rules for AI-assisted work. Here's what's live.

**What it is**
A Claude Code CLI skill library that knows Inspire: our token architecture, typography, spacing, grid, elevation, border radius system, action hierarchy, focus states, and WCAG 2.1 AA baseline. You give it a component or a Figma node — it builds, validates, or audits against the actual ADS file.

**5 skills shipped**

| Skill | Command | What it does |
|---|---|---|
| inspire-core | reference | Foundation rules loaded by all other skills |
| inspire-design-language | reference | Corner radius audit, stroke tokens, focus states, action hierarchy |
| new-component | `/new-component` | Builds an HTML prototype + spec from a component name and library URL |
| inspect-spacing | `/inspect-spacing` | Audits spacing token usage in Figma or HTML before handoff |
| inspire-compliance | `/inspire-compliance` | 7-pass A→G audit of any Figma component against Inspire rules |

**Component gallery**
Two approved components are live with HTML prototypes (ADK + TDK) and machine-authoritative specs:
- Slider — [demo](https://studious-waddle-p376j5k.pages.github.io/components/slider/slider.html)
- Button — [demo](https://studious-waddle-p376j5k.pages.github.io/components/button/button.html)

Gallery: [studious-waddle-p376j5k.pages.github.io](https://studious-waddle-p376j5k.pages.github.io/)

**Quick start**
```
/new-component
Component: [your component]
Library URL: [DevExtreme or other docs URL]
Jira: [paste ticket description and AC]
```
```
/inspect-spacing
Mode: Figma
URL: https://www.figma.com/design/...
```
```
/inspire-compliance
Component: Button
Node: https://www.figma.com/design/...?node-id=273-11972
Themes: both
```

**Requirements:** [Claude Code CLI](https://www.npmjs.com/package/@anthropic-ai/claude-code) + Figma MCP (`/mcp add figma` inside Claude Code). Skills are CLI-only — they don't run in Claude Desktop or claude.ai.

**Links**
- Repo: [github.com/Germanedge/Inspire-Design-System](https://github.com/Germanedge/Inspire-Design-System)
- Figma: [GE — Astronaut Design System](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=21272-89388&t=JOMDtPNR998JIUL5-1)

Happy to walk anyone through setup or take feedback on the skills. — Matt
