---
component: Chat
id: chat
version: 0.1.0
status: draft
source-library: DevExtreme dxChat
source-url: https://js.devexpress.com/jQuery/Documentation/ApiReference/UI_Components/dxChat/
figma-file: yck1tcUXgdQ5aYX6iUAwrO
figma-node: 22619-2
figma-page: "ADK / Chat"
figma-collection: COMPONENTS
prototype: components/chat/chat.html
spec: components/chat/chat.md
modes:
  light: ADK
  dark: TDK
last-updated: 2026-05-29
---

# Chat

**Status:** Draft · **Modes:** ADK (Light) + TDK (Dark) · **Library:** DevExtreme dxChat  
**Prototype:** `components/chat/chat.html` · **Figma:** [ADK / Chat](https://www.figma.com/design/yck1tcUXgdQ5aYX6iUAwrO/GE---Astronaut-Design-System?node-id=22619-2)

---

## Who reads what

| Section | Designer | Front End | Product | Agent |
|---|:---:|:---:|:---:|:---:|
| States | ✓ | ✓ | ✓ | ✓ |
| Color Tokens | ✓ | ✓ | — | ✓ |
| Dimension Tokens | — | ✓ | — | ✓ |
| HTML Structure | — | ✓ | — | ✓ |
| Variable Architecture | — | ✓ | — | ✓ |
| Acceptance Criteria — Visual | ✓ | — | ✓ | ✓ |
| Acceptance Criteria — Functional | — | ✓ | ✓ | ✓ |
| Acceptance Criteria — Figma Binding | ✓ | — | — | ✓ |
| Open Questions | ✓ | ✓ | ✓ | ✓ |

---

## States

Each state maps to a CSS trigger and a Figma variant property. Both must be kept in sync.

| id | Label | CSS Trigger | Figma Variant | Notes |
|---|---|---|---|---|
| `default-empty` | Default — Empty | base styles, no messages | State=Default, Messages=Empty | Empty-state placeholder icon and text |
| `default-messages` | Default — With Messages | messages present in `.dx-chat-messagelist` | State=Default, Messages=Filled | Received (left) and sent (right) bubbles visible |
| `hover` | Hover | `.dx-state-hover` on root; `:hover` on sub-elements | State=Hover | Applied to send button and any message-action buttons |
| `focus` | Focus | `.dx-state-focused` on root; `:focus-visible` on textarea | State=Focus | 2px dashed focus ring on message input textarea |
| `active` | Active (Sending) | `.dx-state-active` on root during async; `chat-disabled` class on container | State=Active | Muted/locked while message is in flight |
| `disabled` | Disabled | `.dx-state-disabled` on root `.dx-chat` | State=Disabled | Full component disabled; all interaction blocked |

**Out of scope for this version:**
- Typing indicator animation (requires live WebSocket / SSE data)
- File upload / attachment variant (`fileUploaderOptions`)
- Message editing and deletion (`editing` config)
- RTL layout (`rtlEnabled: true`)
- Custom `messageTemplate` and `emptyViewTemplate`
- AI streaming response state (demo-specific Angular integration)
- Mobile layout breakpoints

---

## Color Tokens

Authoritative mapping: CSS variable → where it is applied → Figma binding → resolved values in both modes.

**Dark Mode column key:**
- `cascades` — dark value arrives through the semantic token override in `html[data-theme="dark"]`. No explicit component var needed.
- `explicit: #value` — this component var must be set directly in `html[data-theme="dark"]`. Annotated `†` in the HTML prototype.

> **Figma variable status:** Figma node 22619-2 was not accessible at spec-creation time (Figma MCP not authenticated). All COMPONENTS collection paths are marked `Unknown — requires Figma inspection`. SHARED SEMANTIC paths (e.g. `Text/Default`, `Border/Focus`) are confirmed from the ADS file.

### Chat Container

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--chat-bg` | `.dx-chat → background` | Unknown — requires Figma inspection | COMPONENTS | `#ffffff` · White | `#31313b` · TDK 30 | cascades via `--color-surface-default` |
| `--chat-border` | `.dx-chat → border-color` | Unknown — requires Figma inspection | COMPONENTS | `#e7e6e6` · ADK 20 | `#3c3c44` · TDK 40 | cascades via `--color-border-default` |

### Message List

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--chat-messagelist-bg` | `.dx-chat-messagelist → background` | Unknown — requires Figma inspection | COMPONENTS | `#ffffff` · White | `#31313b` · TDK 30 | cascades via `--color-surface-default` |

### Received Message Bubble

Messages from other users, left-aligned (`.dx-chat-messagegroup-alignment-start`).

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--chat-bubble-received-bg` | `.dx-chat-messagegroup-alignment-start .dx-chat-messagebubble-content → background` | Unknown — requires Figma inspection | COMPONENTS | `#f2f2f2` · ADK 10 | `#24242b` · TDK 10 | cascades via `--color-theme-10` |
| `--chat-bubble-received-text` | `.dx-chat-messagegroup-alignment-start .dx-chat-messagebubble-content → color` | Unknown — requires Figma inspection | COMPONENTS | `#3f3e3d` · ADK 80 | `#d4d4d5` · TDK 80 | cascades via `--color-text-default` |

### Sent Message Bubble

Messages from the current user, right-aligned (`.dx-chat-messagegroup-alignment-end`).

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--chat-bubble-sent-bg` | `.dx-chat-messagegroup-alignment-end .dx-chat-messagebubble-content → background` | Unknown — requires Figma inspection | COMPONENTS | `#fcd515` · Brand 100 | `#ffd14a` · Brand 100 TDK | cascades via `--color-brand-default` |
| `--chat-bubble-sent-text` | `.dx-chat-messagegroup-alignment-end .dx-chat-messagebubble-content → color` | Unknown — requires Figma inspection | COMPONENTS | `#3f3e3d` · ADK 80 | `#3f3e3d` · ADK 80 | explicit: `#3f3e3d` † |

Dark mode note: sent bubble text is fixed at `#3f3e3d` in both modes to maintain contrast against the yellow bubble (`#fcd515` / `#ffd14a`). It does not inherit TDK text-default (`#d4d4d5`).

### Message Metadata

Avatar, sender name, and timestamp elements.

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--chat-avatar-bg` | `.dx-chat-avatar → background` | Unknown — requires Figma inspection | COMPONENTS | `#cfcece` · ADK 30 | `#3c3c44` · TDK 40 | explicit: `#3c3c44` † |
| `--chat-avatar-text` | `.dx-chat-avatar → color` | Unknown — requires Figma inspection | COMPONENTS | `#3f3e3d` · ADK 80 | `#d4d4d5` · TDK 80 | cascades via `--color-text-default` |
| `--chat-username-text` | `.dx-chat-messagegroup-sender → color` | `Text/Subtle` | SHARED SEMANTIC | `#6f6e6d` · ADK 60 | `#a9a9ac` · TDK 60 | cascades via `--color-text-subtle` |
| `--chat-timestamp-text` | `.dx-chat-messagebubble-time → color` | `Text/Subtle` | SHARED SEMANTIC | `#6f6e6d` · ADK 60 | `#a9a9ac` · TDK 60 | cascades via `--color-text-subtle` |

Dark mode note: avatar uses TDK 40 (`#3c3c44`) rather than TDK 30 (`#31313b`) because TDK 30 equals `--color-surface-default` — the avatar would be invisible against the container.

### Day Header

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--chat-dayheader-text` | `.dx-chat-dayheader-text → color` | `Text/Subtle` | SHARED SEMANTIC | `#6f6e6d` · ADK 60 | `#a9a9ac` · TDK 60 | cascades via `--color-text-subtle` |
| `--chat-dayheader-line` | `.dx-chat-dayheader::before, ::after → background` | Unknown — requires Figma inspection | COMPONENTS | `#e7e6e6` · ADK 20 | `#3c3c44` · TDK 40 | cascades via `--color-border-default` |

### Message Box

The input container at the bottom of the chat.

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--chat-messagebox-bg` | `.dx-chat-messagebox → background` | Unknown — requires Figma inspection | COMPONENTS | `#ffffff` · White | `#31313b` · TDK 30 | cascades via `--color-surface-default` |
| `--chat-messagebox-border` | `.dx-chat-messagebox → border-top-color` | Unknown — requires Figma inspection | COMPONENTS | `#cfcece` · ADK 30 | `#3c3c44` · TDK 40 | explicit: `#3c3c44` † |
| `--chat-input-border` | `.dx-chat-messagebox-input → border-color` | Unknown — requires Figma inspection | COMPONENTS | `#cfcece` · ADK 30 | `#3c3c44` · TDK 40 | explicit: `#3c3c44` † |
| `--chat-input-border-focus` | `.dx-chat-messagebox-input:focus → border-color` | `Border/Focus` | SHARED SEMANTIC | `#1a88b7` · ADK Inline Link | `#7c79ff` · TDK Inline Link | explicit: `#7c79ff` † |
| `--chat-input-text` | `.dx-chat-messagebox-input → color` | `Text/Default` | SHARED SEMANTIC | `#3f3e3d` · ADK 80 | `#d4d4d5` · TDK 80 | cascades via `--color-text-default` |
| `--chat-input-placeholder` | `.dx-chat-messagebox-input::placeholder → color` | Unknown — requires Figma inspection | SHARED SEMANTIC | `#6f6e6d` · ADK 60 | `#a9a9ac` · TDK 60 | cascades via `--color-text-subtle` |
| `--chat-focus-ring` | `.dx-chat-messagebox-input:focus → outline-color` | `Border/Focus` | SHARED SEMANTIC | `#1a88b7` · ADK Inline Link | `#7c79ff` · TDK Inline Link | explicit: `#7c79ff` † |

Dark mode note: `--chat-messagebox-border` and `--chat-input-border` use TDK 40 (`#3c3c44`) rather than TDK 30 (`#31313b`) because TDK 30 equals `--color-surface-default` — the border would be invisible.

### Send Button

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--chat-send-bg` | `.dx-chat-messagebox-button → background` | Unknown — requires Figma inspection | COMPONENTS | `#fcd515` · Brand 100 | `#ffd14a` · Brand 100 TDK | cascades via `--color-brand-default` |
| `--chat-send-bg-hover` | `.dx-chat-messagebox-button:hover → background` | Unknown — requires Figma inspection | COMPONENTS | `#fbe67e` · Brand 40 | `#fceb98` · Brand 40 TDK | cascades via `--color-brand-hover` |
| `--chat-send-icon` | `.dx-chat-messagebox-button svg → fill` | Unknown — requires Figma inspection | COMPONENTS | `#3f3e3d` · ADK 80 | `#3f3e3d` · ADK 80 | explicit: `#3f3e3d` † |

Dark mode note: send icon fixed at `#3f3e3d` in both modes — same contrast-on-yellow pattern as `--chat-bubble-sent-text`.

### Empty State

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--chat-empty-icon` | `.dx-chat-messagelist-empty-image → color` | `Text/Disabled` | SHARED SEMANTIC | `#cfcece` · ADK 30 | `#50505d` · TDK 50 | cascades via `--color-text-disabled` |
| `--chat-empty-text` | `.dx-chat-messagelist-empty-message → color` | `Text/Subtle` | SHARED SEMANTIC | `#6f6e6d` · ADK 60 | `#a9a9ac` · TDK 60 | cascades via `--color-text-subtle` |

### Disabled State

| CSS Variable | Selector → Property | Figma Variable | Collection | ADK Light | TDK Dark | Dark Mode |
|---|---|---|---|---|---|---|
| `--chat-disabled-input-bg` | `.dx-state-disabled .dx-chat-messagebox-input → background` | Unknown — requires Figma inspection | COMPONENTS | `#f2f2f2` · ADK 10 | `#24242b` · TDK 10 | cascades via `--color-theme-10` |
| `--chat-disabled-input-text` | `.dx-state-disabled .dx-chat-messagebox-input → color` | `Text/Disabled` | SHARED SEMANTIC | `#cfcece` · ADK 30 | `#50505d` · TDK 50 | cascades via `--color-text-disabled` |
| `--chat-disabled-send-bg` | `.dx-state-disabled .dx-chat-messagebox-button → background` | Unknown — requires Figma inspection | COMPONENTS | `#e7e6e6` · ADK 20 | `#292930` · TDK 20 | cascades via `--color-border-default` |
| `--chat-disabled-send-icon` | `.dx-state-disabled .dx-chat-messagebox-button svg → fill` | `Text/Disabled` | SHARED SEMANTIC | `#cfcece` · ADK 30 | `#50505d` · TDK 50 | cascades via `--color-text-disabled` |

---

## Dimension Tokens

| CSS Variable | Selector → Property | Value | Figma Variable | Notes |
|---|---|---|---|---|
| `--chat-height` | `.dx-chat → height` | `480px` | Unknown — requires Figma inspection | Prototype fixed height; production likely fluid |
| `--chat-messagelist-padding-v` | `.dx-chat-messagelist → padding-top / bottom` | `16px` | `Padding/Padding-16` | SPACING semantic alias |
| `--chat-messagelist-padding-h` | `.dx-chat-messagelist → padding-left / right` | `16px` | `Padding/Padding-16` | SPACING semantic alias |
| `--chat-group-gap` | `.dx-chat-messagelist → gap` | `16px` | Unknown — requires Figma inspection | SPACING primitive — no semantic alias confirmed for 16px |
| `--chat-bubble-gap` | `.dx-chat-messagegroup → gap` | `4px` | Unknown — requires Figma inspection | SPACING primitive — no semantic alias |
| `--chat-bubble-radius` | `.dx-chat-messagebubble-content → border-radius` | `4px` | Unknown — requires Figma inspection | Assumed — matches cards/boardlets in as-built audit |
| `--chat-bubble-padding-v` | `.dx-chat-messagebubble-content → padding-top / bottom` | `8px` | `Padding/Padding-08` | SPACING semantic alias |
| `--chat-bubble-padding-h` | `.dx-chat-messagebubble-content → padding-left / right` | `12px` | Unknown — requires Figma inspection | SPACING primitive |
| `--chat-avatar-size` | `.dx-chat-avatar → width, height` | `28px` | Unknown — requires Figma inspection | Estimated — not confirmed in Figma |
| `--chat-avatar-radius` | `.dx-chat-avatar → border-radius` | `9999px` | Unknown — requires Figma inspection | Fully rounded — matches icon-only button pattern |
| `--chat-avatar-gap` | `.dx-chat-messagegroup-info → gap` | `8px` | `Gap/Gap-08` | SPACING semantic alias |
| `--chat-messagebox-padding-v` | `.dx-chat-messagebox → padding-top / bottom` | `12px` | Unknown — requires Figma inspection | SPACING primitive |
| `--chat-messagebox-padding-h` | `.dx-chat-messagebox → padding-left / right` | `16px` | `Padding/Padding-16` | SPACING semantic alias |
| `--chat-messagebox-gap` | `.dx-chat-messagebox → gap` | `8px` | `Gap/Gap-08` | SPACING semantic alias |
| `--chat-input-min-height` | `.dx-chat-messagebox-input → min-height` | `40px` | Unknown — requires Figma inspection | Matches §row-03 (40px) row token |
| `--chat-send-size` | `.dx-chat-messagebox-button → width, height` | `40px` | Unknown — requires Figma inspection | Matches §row-03 (40px) row token |
| `--chat-send-radius` | `.dx-chat-messagebox-button → border-radius` | `0px` | — | Square corners — Germanedge rule for action elements |

---

## HTML Structure

Class names are emitted by DevExtreme at runtime. Do not invent or rename them.

> **Verification needed:** Sub-element class names (`.dx-chat-avatar`, `.dx-chat-messagegroup-sender`, `.dx-chat-messagebubble-time`, `.dx-chat-dayheader`, `.dx-chat-dayheader-text`) are inferred from the DevExtreme `dx-chat-*` naming pattern. Primary container class names (`.dx-chat`, `.dx-chat-messagelist`, `.dx-chat-messagegroup-alignment-start`, `.dx-chat-messagebubble`, `.dx-chat-messagebubble-content`, `.dx-chat-messagebox`) are confirmed from demo inspection.

```html
<!-- Default — Empty -->
<div class="dx-chat">
  <div class="dx-chat-messagelist">
    <div class="dx-chat-messagelist-empty">
      <div class="dx-chat-messagelist-empty-image"><!-- SVG icon --></div>
      <span class="dx-chat-messagelist-empty-message">No messages yet</span>
    </div>
  </div>
  <div class="dx-chat-messagebox">
    <textarea class="dx-chat-messagebox-input" placeholder="Message..." rows="1"
              aria-label="Message input"></textarea>
    <button class="dx-chat-messagebox-button" aria-label="Send message">
      <!-- Send SVG icon -->
    </button>
  </div>
</div>

<!-- Default — With Messages -->
<div class="dx-chat">
  <div class="dx-chat-messagelist">
    <!-- Day header separator -->
    <div class="dx-chat-dayheader">
      <span class="dx-chat-dayheader-text">Today</span>
    </div>
    <!-- Received message group (left-aligned: other user) -->
    <div class="dx-chat-messagegroup dx-chat-messagegroup-alignment-start">
      <div class="dx-chat-messagegroup-info">
        <div class="dx-chat-avatar">AI</div>
        <span class="dx-chat-messagegroup-sender">AI Assistant</span>
      </div>
      <div class="dx-chat-messagebubble">
        <div class="dx-chat-messagebubble-content">How can I help you today?</div>
        <span class="dx-chat-messagebubble-time">09:41</span>
      </div>
    </div>
    <!-- Sent message group (right-aligned: current user) -->
    <div class="dx-chat-messagegroup dx-chat-messagegroup-alignment-end">
      <div class="dx-chat-messagebubble">
        <div class="dx-chat-messagebubble-content">Can you explain how the dashboard works?</div>
        <span class="dx-chat-messagebubble-time">09:42</span>
      </div>
    </div>
  </div>
  <div class="dx-chat-messagebox">
    <textarea class="dx-chat-messagebox-input" placeholder="Message..." rows="1"
              aria-label="Message input"></textarea>
    <button class="dx-chat-messagebox-button" aria-label="Send message">
      <!-- Send SVG icon -->
    </button>
  </div>
</div>

<!-- Disabled — dx-state-disabled on root, aria-disabled on interactive children -->
<div class="dx-chat dx-state-disabled" aria-disabled="true">
  <!-- same inner structure; JS guard prevents interaction -->
</div>
```

**DevExtreme runtime state classes** (applied by the library at runtime):

| Class | Applied to | Trigger |
|---|---|---|
| `.dx-state-hover` | root `.dx-chat` | Mouse enter |
| `.dx-state-focused` | root `.dx-chat` | Keyboard focus enters component |
| `.dx-state-active` | root `.dx-chat` | During message send / async operation |
| `.dx-state-disabled` | root `.dx-chat` | `disabled: true` prop |

---

## Variable Architecture

Chat uses a **Tier 2 component-scoped variable exception** for elements with unique visual roles that have no direct SHARED SEMANTIC equivalent.

**Tier 1 (SHARED SEMANTIC)** is used for text colors (`Text/Default`, `Text/Subtle`, `Text/Disabled`), surface (`Surface/Default`), and focus ring (`Border/Focus`). These cascade correctly between ADK and TDK.

**Tier 2 (component-scoped)** is required for:
- **Received bubble background** — a tinted surface (ADK 10 / TDK 10) that has no `Surface/` semantic equivalent. The system's `Surface/Disabled` token resolves to ADK 10 in light but TDK 40 in dark — an incorrect cascade for this role.
- **Sent bubble background** — brand yellow applied as a message surface; semantically distinct from `Colors/Brand/Brand 100`'s primary use as a button fill.
- **Avatar background** — neutral fill on a circular container; no `Avatar/` or `Surface/Avatar` semantic token exists yet.
- **Message box and input borders** — ADK 30 (`#cfcece`) in light; must be explicitly TDK 40 (`#3c3c44`) in dark because TDK 30 (`#31313b`) equals `Surface/Default`, making the border invisible.
- **Sent bubble and send icon text** — fixed at `#3f3e3d` in both modes to maintain contrast against brand yellow. Would incorrectly cascade to TDK 80 (`#d4d4d5`) without an explicit override.

**Rules for this component:**
- All `--chat-*` variables in `:root` must reference semantic tokens — no raw hex.
- Raw hex permitted only in `html[data-theme="dark"]` for cascade failures (marked `†`).
- If future semantic tokens are added for avatar surfaces or tinted bubble surfaces, migrate component vars to reference them.

---

## Acceptance Criteria

### Visual (Designer · Agent)

Verify against `components/chat/chat.html`. Toggle dark mode with the button in the prototype header.

**Light mode (ADK):**
- [ ] Container: white `#ffffff` background, `#e7e6e6` border
- [ ] Received bubbles: `#f2f2f2` (ADK 10) background, `#3f3e3d` text, 4px border-radius
- [ ] Sent bubbles: `#fcd515` (Brand 100) background, `#3f3e3d` text (dark on yellow), 4px border-radius
- [ ] Avatar: `#cfcece` circle (28px, fully rounded), `#3f3e3d` initials
- [ ] Username and timestamp: `#6f6e6d` (ADK 60), Inter Tight 12px/16px
- [ ] Day header: `#6f6e6d` text centered, `#e7e6e6` horizontal rule lines
- [ ] Message input: white background, `#cfcece` border (1px solid), `#3f3e3d` text, Inter Tight 14px/18px
- [ ] Input placeholder: `#6f6e6d` (ADK 60)
- [ ] Send button: `#fcd515` background (40×40px, 0px radius), `#3f3e3d` send icon
- [ ] Send button hover: `#fbe67e` (ADK Brand 40)
- [ ] Focus: 2px dashed `#1a88b7` ring on input textarea at element edge (no offset); border changes to `#1a88b7`
- [ ] Disabled: list area at 40% opacity; input bg `#f2f2f2`, text `#cfcece`, `cursor: not-allowed`; send bg `#e7e6e6`, icon `#cfcece`

**Dark mode (TDK):**
- [ ] Container: `#31313b` background, `#3c3c44` border
- [ ] Received bubbles: `#24242b` (TDK 10), `#d4d4d5` text
- [ ] Sent bubbles: `#ffd14a` (Brand 100 TDK), `#3f3e3d` text (forced, does not cascade to TDK 80)
- [ ] Avatar: `#3c3c44` (TDK 40) — not TDK 30 which matches surface-default
- [ ] Username, timestamp: `#a9a9ac` (TDK 60)
- [ ] Day header: `#a9a9ac` text, `#3c3c44` lines
- [ ] Message input: `#31313b` background, `#3c3c44` border (explicit †)
- [ ] Input placeholder: `#a9a9ac` (TDK 60)
- [ ] Send button: `#ffd14a` background, `#3f3e3d` icon (explicit †)
- [ ] Focus ring: 2px dashed `#7c79ff` (explicit †)
- [ ] Page background: `#202026`; container: `#31313b`

### Functional (Front End · Agent)

- [ ] Message input textarea focusable via Tab key
- [ ] Shift+Enter creates a newline; Enter (alone) submits the message (DevExtreme default)
- [ ] Send button triggers `onMessageEntered` event
- [ ] `.dx-state-disabled` on root blocks all keyboard and pointer events via JS guard
- [ ] `cursor: not-allowed` visible on hover over any disabled element; no `pointer-events: none` on child elements
- [ ] Message list scrolls independently when content overflows container height
- [ ] Received messages render left-aligned; sent messages render right-aligned
- [ ] Day headers are full-width separators with centered date text

**Spacing verification:**
- [ ] Message list: 16px padding all sides
- [ ] Gap between message groups: 16px
- [ ] Bubble padding: 8px vertical, 12px horizontal
- [ ] Message box: 12px vertical, 16px horizontal padding
- [ ] Avatar-to-sender-name gap: 8px
- [ ] Message box to send button gap: 8px

### Figma Binding (Designer · Agent)

- [ ] All `Unknown — requires Figma inspection` entries resolved with confirmed Figma variable paths from `get_variable_defs(yck1tcUXgdQ5aYX6iUAwrO, 22619:2)`
- [ ] All color fills in Figma frames bound to Figma variables — no unbound hex
- [ ] COMPONENTS collection variables exist for bubble backgrounds, avatar, and message box border
- [ ] SHARED SEMANTIC used for `Text/Default`, `Text/Subtle`, `Text/Disabled`, and `Border/Focus`
- [ ] Both ADK and TDK mode values set on every COMPONENTS variable
- [ ] Sent bubble text (`#3f3e3d`) and send icon (`#3f3e3d`) confirmed intentional in both modes
- [ ] `Border/Focus` confirmed as `#1a88b7` ADK / `#7c79ff` TDK

---

## Open Questions

| # | Question | Owner | Status |
|---|---|---|---|
| 1 | Sent bubble color — brand yellow assumed (`#fcd515` / `#ffd14a`); confirm this matches Figma node 22619-2 | Design | Open |
| 2 | All Figma variable paths — 18 of 24 color tokens are `Unknown`. Requires `get_variable_defs(yck1tcUXgdQ5aYX6iUAwrO, 22619:2)` call when Figma MCP is authenticated | Design / Agent | Open |
| 3 | Sub-element class names — `.dx-chat-avatar`, `.dx-chat-messagegroup-sender`, `.dx-chat-messagebubble-time`, `.dx-chat-dayheader`, `.dx-chat-dayheader-text` are inferred; verify against rendered DevExtreme DOM | Front End | Open |
| 4 | Chat height — 480px used in prototype; production likely fluid or fill-container. Confirm expected sizing behavior | Product / Front End | Open |
| 5 | Avatar size — 28px estimated; confirm from Figma frame metadata (`get_metadata`) | Design | Open |
| 6 | Bubble border radius — 4px assumed (matches cards/boardlets in as-built audit); confirm from Figma node | Design | Open |
| 7 | Group gap (16px) — no confirmed SPACING semantic alias for 16px gap; using primitive. Does `Gap/Gap-16` exist in the SPACING collection? | Design | Open |
| 8 | Message box vertical padding (12px) — no confirmed `Padding/Padding-12` semantic alias; using primitive | Design | Open |
| 9 | Bubble horizontal padding (12px) — no confirmed semantic alias; using primitive | Design | Open |
| 10 | Hover state on message action buttons (copy, regenerate) — in scope for this version or deferred to separate spec? | Product | Open |
| 11 | Typing indicator — currently out of scope. When needed, define as a variant with dot animation tokens and separate sub-element spec | Design | Deferred |
| 12 | `--color-text-subtle` TDK value — inspire-core says `#a9a9ac` (TDK 60); slider.html sets `#bcbcbe` (TDK 70). This spec uses `#a9a9ac` per inspire-core. Confirm correct TDK value | Design | Open |
