# Component Registry

Each component lives in its own subdirectory: `components/[id]/`.

**Source of truth: Figma.** Token values, component structure, spacing, and states are all defined in the GE — Astronaut Design System Figma file. The HTML prototype and `.md` spec are validated against Figma — not the other way around. When a value in the prototype or spec conflicts with Figma, Figma wins and the prototype/spec is updated.

> **Future:** If a coded Storybook is established as the authoritative implementation, the validation direction will shift — Figma will validate against code rather than code validating against Figma. The skills in this library will be updated to reflect that when it happens.

**Files per component:**
- `[id].html` — self-contained visual prototype with theme toggle
- `[id].md` — machine-authoritative spec (frontmatter + token tables + acceptance criteria)

---

## Components

| Component | ID | Status | Live Demo | Spec | Figma |
|---|---|---|---|---|---|
| Slider | `slider` | Draft | [slider.html](https://studious-waddle-p376j5k.pages.github.io/components/slider/slider.html) | [slider.md](slider/slider.md) | [Figma](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=22145-141089) |
| FilterBuilder | `filter-builder` | Draft | [filter-builder.html](https://studious-waddle-p376j5k.pages.github.io/components/filter-builder/filter-builder.html) | [filter-builder.md](filter-builder/filter-builder.md) | [Figma](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=22271-11752) |
| Button | `button` | Draft | [button.html](https://studious-waddle-p376j5k.pages.github.io/components/button/button.html) | [button.md](button/button.md) | [Primary](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=273-11972) · [Secondary](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=639-51015) · [Ghost](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=639-53573) |
| Rich Popover | `rich-popover` | Draft | [rich-popover.html](https://studious-waddle-p376j5k.pages.github.io/components/rich-popover/rich-popover.html) | [rich-popover.md](rich-popover/rich-popover.md) | [Figma](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=22592-3) |

---

## About this repository

This repo serves two purposes: it houses the **Inspire skill library** (Claude Code skills that encode design system rules) and the **component output** those skills produce (HTML prototypes + specs). Both live here by design — components are the proof-of-work for the skills, and having them together makes cross-referencing easy during development.

As the component library grows, separating the two into distinct repos (skills repo / component repo) is a likely next step. When that happens, the skills repo will reference the component repo as the canonical example set rather than containing it directly. This note exists so that decision is made deliberately, not discovered as a mess.

**Repo:** [Germanedge/Inspire-Design-System](https://github.com/Germanedge/Inspire-Design-System)  
**Live demos:** [studious-waddle-p376j5k.pages.github.io](https://studious-waddle-p376j5k.pages.github.io/)

---

## Adding a Component

Use `/new-component` in Claude Code CLI. Provide a component name and a library docs URL. The skill will:
1. Research the library's HTML class names and state classes
2. Confirm the state list with you
3. Build `components/[id]/[id].html` and `components/[id]/[id].md`
4. Optionally create Figma frames via the Figma MCP

**Minimum invocation:**
```
/new-component
Component: Checkbox
Library URL: https://js.devexpress.com/Documentation/ApiReference/UI_Components/dxCheckBox/
```

**With all optional inputs:**
```
/new-component
Component: Checkbox
Library URL: https://js.devexpress.com/Documentation/ApiReference/UI_Components/dxCheckBox/
Figma URL: https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=22145-141089
Create Figma frames? Yes
```

> **CLI only.** Skills don't run in Claude Desktop or the Claude.ai web UI. See `.claude/skills/new-component/SKILL.md` for prerequisites and full guidance.

After adding a component, update the table above.

---

## Checking Component Compliance

Before a component is accepted into the registry, run the acceptance check. The agent performs 7 checks and produces a structured report for the reviewer (who may be the same designer submitting the component).

**What you need:**
- Claude Code CLI installed: `npm install -g @anthropic-ai/claude-code`
- Figma MCP connected: `/mcp add figma` inside Claude Code

**To check a single component**, give Claude the Figma node URL:
```
Run the acceptance check on this component: https://www.figma.com/design/[fileKey]/...?node-id=[nodeId]
```

**To check a full page**, give Claude the page URL:
```
Run the acceptance check on this page as a whole: https://www.figma.com/design/[fileKey]/...?node-id=[pageNodeId]
```

The agent will fetch variable definitions and design context directly from Figma, cross-reference all color tokens against the shared semantic token set, and output a pass/fail report.

**The 9 checks (contrast failures and color-only state are hard blockers; remaining a11y items are flags):**
1. **Semantic variable compliance** — color tokens must use shared semantic vars where a direct replacement exists
2. **Spacing compliance** — gap and padding values must reference SPACING collection aliases
3. **Cross-component variable borrowing** — a component may only reference its own vars and shared semantic vars
4. **State completeness** — all states must be present or explicitly documented as out of scope
5. **Border radius compliance** — multi-value system (0px, 2px, 4px, 8px, fully-rounded by component); verify against the as-built audit in `inspire-design-language`
6. **Dark mode completeness** — every color token must have a TDK value
7. **Token naming convention** — `--[component]-[element]-[property]-[state]`; generic palette aliases are not acceptable
8. **Auto-layout & resize compliance** — Figma layers must use auto-layout; sizing modes (`Fill`/`Hug`/`Fixed`) must be correct
9. **Accessibility baseline** — WCAG 2.1 AA: 4.5:1 text contrast, 3:1 UI element contrast, color never sole state communicator, `aria-label` on icon-only elements, keyboard accessible

> A component is not accepted until all ⛔ blockers are resolved. ⚠️ warnings flag drift or unconfirmed values that need a design decision.
