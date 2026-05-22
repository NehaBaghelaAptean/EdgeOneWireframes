# Inspire Design System — Skill Library Update

We've shipped the first version of the Inspire skill library — a set of Claude Code skills that encode our design system rules for AI-assisted work. Here's what's live.

**What it is**
A Claude Code CLI skill library that knows Inspire: our token architecture, typography, spacing, grid, elevation, border radius system, action hierarchy, focus states, and WCAG 2.1 AA baseline. You give it a component or a Figma node — it builds, validates, or audits against the actual ADS file.

---

**5 skills shipped**

| Skill | Command | What it does |
|---|---|---|
| inspire-core | reference | Foundation rules — token architecture, typography scale, spacing, grid, elevation, design philosophy, WCAG 2.1 AA baseline |
| inspire-design-language | reference | As-built design language audit — corner radii across all ADK components, stroke tokens, focus state rules, full action hierarchy with decision framework and placement patterns |
| new-component | `/new-component` | Builds an HTML prototype + spec from a component name, library URL, and optional Jira ticket |
| inspect-spacing | `/inspect-spacing` | Audits spacing token usage in Figma designs or HTML prototypes before handoff |
| inspire-compliance | `/inspire-compliance` | 7-pass A→G audit of any Figma component against Inspire rules |

**What's in inspire-design-language**
This skill captures the design language as it actually exists today — not as aspiration. It includes a full corner radius audit across 20+ ADK components (the system is multi-value: 0px, 2px, 4px, 8px, 9999px — not 0 everywhere), a proposed 4-step token scale for formalizing this, all six stroke tokens, focus state rules, and the complete action hierarchy (Primary / Secondary / Tertiary) with a decision framework, placement patterns for dialogs and toolbars, and copy guidance. Any work touching layout, buttons, or focus behavior should load this skill.

---

**Component gallery**
Two approved components are live with HTML prototypes (ADK + TDK) and machine-authoritative specs:
- Slider — [demo](https://studious-waddle-p376j5k.pages.github.io/components/slider/slider.html)
- Button — [demo](https://studious-waddle-p376j5k.pages.github.io/components/button/button.html)

Gallery: [studious-waddle-p376j5k.pages.github.io](https://studious-waddle-p376j5k.pages.github.io/)

---

**Roadmap**
The full picture is in [`ROADMAP.md`](ROADMAP.md) in the repo — platform context, the complete component inventory with build status, known inconsistencies, and the prioritized skill build plan. If you want to understand what's next or where a component stands, that's the place to start.

---

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

---

**Links**
- Repo + Roadmap: [github.com/Germanedge/Inspire-Design-System](https://github.com/Germanedge/Inspire-Design-System)
- Gallery: [studious-waddle-p376j5k.pages.github.io](https://studious-waddle-p376j5k.pages.github.io/)
- Figma: [GE — Astronaut Design System](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=21272-89388&t=JOMDtPNR998JIUL5-1)

Happy to walk anyone through setup or take feedback on the skills. — Matt
