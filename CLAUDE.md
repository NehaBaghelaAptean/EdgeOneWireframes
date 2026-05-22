# Inspire Components — Claude Code Guide

## Available Skills

| Skill | Command | What it does |
|---|---|---|
| Inspire Core | (reference) | Foundation rules loaded by all other skills — token architecture, ADK/TDK, acceptance checks, styling constraints. |
| New Component | `/new-component` | Builds a new ADK/TDK design system component — HTML prototype + spec. |
| Inspect Spacing | `/inspect-spacing` | Validates spacing token usage in Figma designs (Mode A) or HTML prototypes before engineer handoff (Mode B). Flags mismatches, never halts. |
| Inspire Design Language | (reference) | Design language philosophy, current state, WIP proposals — corner radii, stroke tokens, focus state, action hierarchy. Load for design-decision work. |
| Inspire Compliance | `/inspire-compliance` | 7-pass compliance checklist (A→G) for auditing Inspire components in Figma: context, tokens, typography, spacing, elevation, focus, component-specific rules. |

Skills are CLI-only. They don't run in Claude Desktop or the Claude.ai web UI.

## Project Structure

```
components/
  [id]/
    [id].html   — self-contained visual prototype with theme toggle
    [id].md     — machine-authoritative spec (source of truth)
  README.md     — component registry
.claude/
  skills/
    inspire-core/SKILL.md           — foundation reference loaded by all skills
    new-component/SKILL.md          — /new-component skill definition
    inspect-spacing/SKILL.md        — /inspect-spacing validator (Figma + code)
    inspire-design-language/SKILL.md — design language, proposals, action hierarchy
    inspire-compliance/SKILL.md      — /inspire-compliance audit checklist
```

## Roadmap

`ROADMAP.md` at the repo root — platform context, full component inventory, known inconsistencies, and the prioritized skill build plan.

## Key Conventions

- The spec (`.md`) is the contract. Code and Figma both reflect the spec.
- Semantic color tokens come from the Figma ADS file (`yck1tcUXgdQ5aYX6iUAwrO`), Variables page, **SHARED SEMANTIC** collection.
- Border radius is a multi-value system — not `0` everywhere. See `inspire-design-language/SKILL.md` for the full as-built audit table (0px, 2px, 4px, 8px, fully-rounded) and the proposed 4-step token scale. The "0px everywhere" assumption is incorrect.
- Font: `Inter Tight` for condensed/headings, `Inter` for body.
- Reference implementation: `components/slider/` is the canonical example.
