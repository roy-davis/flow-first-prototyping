# Screen, Prepare, and UI-Agent Commands

Detailed templates and behavior for screen inventory, screen specs, prototype briefs, and UI-agent handoff files.

---

### proto.map

**Output:** `./docs/ux-ui/screens/inventory.md` and `./docs/ux-ui/screens/sitemap.md`
**Reads:** `docs/ux-ui/app-outline.md`, `docs/ux-ui/journeys/`, `docs/ux-ui/stories/`, `docs/ux-ui/flows/`, `docs/ux-ui/actors/`

Collect all screens from the app outline, each flow's exit states and steps, each story's acceptance criteria where they imply a screen, and each journey's screens-implied table. Deduplicate.

Use `app-outline.md` as the sanity-check baseline, not as a binding inventory. If the final inventory adds, removes, merges, or splits candidates from the outline, call that out in Notes so the user can review the structural change.

**Screen types:** List / Detail / Form / Dashboard / Empty / Error / Confirmation / Settings / Auth

**Priority:** Must-have / Should-have / Nice-to-have

**Canonical screen naming:**
- Name pages as stable app surfaces or Figma frame names, not as purpose/action hybrids.
- Do not combine a page with its primary action using slash names. For example, use `Home`, not `Home / Resume`; make resume a state such as `Resume available`.
- Avoid state, task, or mode words in top-level page names when a simpler noun names the surface. Examples: `Library`, not `Library Browsing`; `Sources`, not `Sources Overview`; `SMB Setup`, not `SMB Source Setup`; `Sync Progress`, not `Source Sync Progress`; `Remove Source`, not `Remove Source Confirmation`.
- Keep nouns that genuinely identify a task-specific surface. Examples: `Provider Authorization`, `Folder Picker`, `Book Detail`, `Now Playing`, `Playback Recovery`, `Source Repair`.
- Put variants such as empty, loading, blocked, warning, resume-ready, confirmation, and restricted views in the screen state's name rather than the page name.

Ask the user to confirm prototype scope before finalising.

After producing `inventory.md`, also produce `sitemap.md` showing the navigation structure — how screens connect to each other. The sitemap shows canonical screens only, not state variants. Each screen appears once regardless of how many states it has.

**Template:**
```markdown
# Screen Inventory

> File: docs/ux-ui/screens/inventory.md

Total: [N] | In scope: [N] | Out of scope: [N]

## Screen list

| ID | Name | Type | Priority | Scope | File | Story | Flow | Actor | State |
|---|---|---|---|---|---|---|---|---|---|
| PG01 | | | Must-have | In | — | | | | |

> The File column starts empty. proto.screens fills it in as each screen file is written.
> Route column comes from proto.screens too — leave blank initially.

---

## [Screen name] — PG01

**Type:** | **Priority:** | **Scope:** In / Out
**Story:** [Story file] | **Flow:** [Flow file] | **Journey stage:** | **Actor:** [Actor name] | **State shown:**

**Purpose:** [One sentence]
**Entry points:**
**Exit points:**
**Notes:**
```

**Template (sitemap.md):**
```markdown
# Sitemap

> File: docs/ux-ui/screens/sitemap.md
> Canonical screens only. State variants are not separate nodes.

## Entry points

- [Screen name] — [how users arrive: app launch, direct URL, invitation link, etc.]

## Screen connections

Use a table so each transition has a clear trigger, destination, resulting state, and return behaviour. Do not list vague connections such as "continues" without naming the trigger.

| From | Trigger | To | Resulting state | Return / back behaviour | Notes |
|---|---|---|---|---|---|
| [screen-name] | [action, row tap, system event, deep link] | [screen-name] | [state shown on destination] | [where back/cancel returns] | |

## Flow continuity notes

- [Known loops, resume paths, interrupted flows, modal/sheet exits, or transitions that need special care]

## Orphaned screens

[Screens with no inbound path — may need an entry point or are deep-link only.]

- [Screen name]: [note]
```

---

---

### proto.screens

**Output:** one file per screen at `./docs/ux-ui/screens/[screen-name].md`, plus `./docs/ux-ui/screens/page-state-design-links.csv`
**File naming:** slugify the screen name from the inventory. Examples: `map-workspace.md`, `mob-movement.md`, `login.md`, `dashboard.md`
**Reads:** `docs/ux-ui/design.md`, `docs/ux-ui/screens/inventory.md`, `docs/ux-ui/data/states.md`, `docs/ux-ui/journeys/`, `docs/ux-ui/stories/`, `docs/ux-ui/flows/`
**Also reads if present:** `docs/ux-ui/screens/contracts.md`, `docs/ux-ui/data/requirements.md`, `docs/ux-ui/actions.md`

Generate one file per in-scope screen from the inventory. Do not produce a combined file. After writing all screen files, update `docs/ux-ui/screens/inventory.md` to fill in the File column for each screen.

After all screen files are written, generate `docs/ux-ui/screens/page-state-design-links.csv`. This CSV is a lightweight Figma linking tracker for designers. It lists each canonical page row and each sub-state row, with stable IDs that can be pasted into or matched to Figma frame names.

**CSV naming rules:**
- Use the canonical screen names from `docs/ux-ui/screens/inventory.md`; do not reintroduce purpose/action hybrid names.
- Top-level page rows use the screen ID only: `PG01`, `PG02`, etc.
- Sub-state rows append sequential uppercase letters in the order the states appear in the screen spec: `PG01.A`, `PG01.B`, `PG01.C`.
- For every in-scope screen, include one sub-state row for every state in that screen spec's `### States` table. Do not emit page-only rows for in-scope screens, and do not limit sub-state rows to newly added or recently changed screens.
- The `Page / State Name` column merges the page and state name in this format: `[Page name] - [State name]`.
- Page rows use `[Page name] - Page overview`.
- State names should be human-readable labels, not raw code slugs. Example: `resume-available` becomes `Resume available`.
- Keep the `Figma Link` cells blank for the user to fill.
- Include out-of-scope screens as page rows only, with `Item Type` = `Page` and `State Type` = `Out of scope`.

**State Type classification:**
Use concise labels that help designers filter the CSV. Prefer these labels when applicable: `Default`, `Ready`, `Dashboard`, `List`, `Detail`, `Form`, `Settings`, `Auth`, `Confirmation`, `Empty`, `Loading`, `Error`, `Warning`, `Success`, `Dialog`, `Warning dialog`, `Loading dialog`, `Error dialog`, `Permission`, `Auth pending`, `Auth required`, `Auth error`, `Auth success`, `Progress`, `Progress queued`, `Progress partial`, `Playback`, `Playback paused`, `Repair`, `Completed`, `Out of scope`.

**CSV template:**
```csv
Design ID,Page / State Name,Item Type,State Type,Figma Link
PG01,Home - Page overview,Page,Dashboard,
PG01.A,Home - Resume available,Sub-state,Ready,
PG01.B,Home - No sources,Sub-state,Empty,
PG01.C,Home - Source unavailable,Sub-state,Error,
```

Each screen spec describes what the screen must do and how it must behave — not which components to use or how to implement it. The implementing agent makes those choices. Specifications that name specific libraries or prescribe exact implementations reduce the agent's ability to make good decisions.

Each screen ends with a **screen generation prompt** — one dense paragraph that gives the implementing agent everything it needs: who uses the screen, what they are trying to do, what must be visible, how it must behave, and what constraints apply. The prompt describes intent and behaviour, not implementation choices.

**Literal copy boundary:** Directional fields are not on-screen copy. Do not render text from Design intent, User state of mind, Usage context, Content priority, Anti-goals, Screen robustness, Layout regions, Acceptance criteria, or Heuristic check as visible UI text. Quotation marks inside directional fields do not make text literal copy. Only text listed under `### Content`, `### Copy requirements`, explicit labels/messages in `### Actions` or `### Interaction states`, and copy labelled as title/body/button/label/message inside a critical variant should be treated as visible copy. If a sentence from a directional field should appear in the UI, duplicate it under `### Content` and name the element it belongs to.

If the user has specified a target tool inline with the command, note it in the prompt header. Otherwise ask: "Which tool are you generating for — v0, Lovable, Bolt, Claude Design, Google Stitch, or other?"

**Template:**
```markdown
# [Screen name]

> File: docs/ux-ui/screens/[screen-name].md
> Screen ID: PG01

| Attribute | Value |
|---|---|
| Route | `/[path]` |
| Access | [ROLE, ROLE] |
| Mobile | Critical / Supported / Not required |
| Scope | In scope / Out of scope |

### Design intent

- Primary purpose: [What this screen exists to do — one sentence]
- Primary actors: [Which human or non-human actors use, affect, or are represented on this screen]
- Primary job: [The core task the user is trying to complete]
- Principle served: [Which design principle from docs/ux-ui/value-proposition.md this screen most directly expresses]
- Entry points: [How users arrive here]
- Success outcome: [What a completed interaction looks like]
- Content priority: Primary: [what must be immediately visible]. Secondary: [what supports but is not critical]
- Critical variants: [Named rendering modes this screen must support, e.g. offline mode, empty state, permission-restricted view]
- User state of mind: [Rushed, exploring, anxious, focused, distracted, etc. — only include if it affects design]
- Usage context: [Device posture, environment, connectivity, interruption level, lighting, accessibility constraints]
- Data range: [Zero / typical / maximum records and long-text examples this screen must tolerate]
- Anti-goals: [What this screen must not become or must avoid visually/structurally]
- Fidelity target: [Sketch / Lo-fi / Mid-fi / Hi-fi / Production-ready]
- Exit paths: [Where users go after completing or abandoning the task]

### Related flows

- [Flow file name]: [One-line description of the relationship]

### Related stories

- [Story file name]: [What user task slice this screen supports]

### Decisions on this screen

Document decisions with meaningful consequences — approve, submit, delete, assign, configure, move. Not navigation choices. Write "None" if there are no consequential decisions.

| ID | Decision | Stakes | Reversible |
|---|---|---|---|
| D1 | | High/Med/Low | Yes / No |

For each Medium or High stakes decision:

**[Decision name] — D1**
- What the user is deciding: [Plain language]
- Options: [Choices available and what each means]
- Information required: [What must be visible to decide confidently]
- Risk if wrong: [Consequence]
- Reversible: Yes / No — Recovery: [How to undo or correct]
- Recommended default: [Safe option if one exists]
- Conditions that change this: [State or permission that changes options]

### States

| State | Description | Transitions |
|---|---|---|
| `loading` | | |
| `ready` | | |
| `error` | | |

### Actions

| Action | Description | Precondition |
|---|---|---|
| [Action name] | | Always |
| [Action name] | | [Condition] |

### In-flow contextual actions

List optional secondary actions that arise while the user is focused on a specific object on this screen. These should preserve the user's place in the primary task unless there is a strong reason to navigate away. Write None if no contextual action belongs on this screen.

| Moment / object | User intent | Trigger / affordance | Result | Preserve / return behaviour | When not available |
|---|---|---|---|---|---|
| [selected text / focused item / media position / row / field] | [capture / annotate / save / tag / attach / reuse] | [selection menu / inline action / sheet / row action] | [what is created or changed] | [cursor, scroll, selection, draft, playback, or route restored] | [blocked condition] |

### Transition contract

List every transition into or out of this screen, including state changes that keep the user on the same screen. Each row must line up with a flow step or sitemap connection.

| From | Trigger | To | Resulting state | Back / exit behaviour | Blocked / error behaviour |
|---|---|---|---|---|---|
| [source screen/state] | [action/event] | [destination screen/state] | [what the destination shows] | [return path] | [what happens if unavailable] |

### Interaction states

Define states for every consequential button, row action, input, menu, drag action, or destructive control. Use N/A only when the interaction does not exist on the target platform.

| Element or action | Default | Focus | Pressed / active | Disabled | Loading | Success feedback | Error feedback / recovery |
|---|---|---|---|---|---|---|---|
| [Element/action] | | | | | | | |

### Data required

| Data | Source | Offline | Notes |
|---|---|---|---|
| [Data] | Server | Cached | |
| [Data] | Device | Real-time | |
| [Data] | Local | Local | |
| [Data] | Input | N/A | |

**Offline key:** Cached = available offline / Local = device only / Real-time = requires connection / N/A = derived or user input

### Screen robustness

Document realistic edge cases that change rendering or interaction. Mark N/A only after deciding the concern truly does not apply.

| Concern | Requirement |
|---|---|
| Empty / zero data | |
| Typical data | |
| Maximum / dense data | |
| Long text / overflow | |
| Text expansion / localization | |
| Loading / slow response | |
| Offline / degraded connection | |
| Permission / restricted access | |
| Duplicate or concurrent action | |
| Responsive / safe area | |
| Keyboard / focus | |

### Visual indicators

| Indicator | Meaning |
|---|---|
| [Symbol or colour] | [What it communicates] |

### Critical variants

**[Variant name]**
[What triggers this variant, what changes, and what the user can do in this mode]

### Layout regions

Describe the functional regions of this screen without specifying components or implementation. What must be present and what purpose does each region serve.

| Region | Purpose | Required content |
|---|---|---|
| [Region name] | [What it does for the user] | [What it must show] |

### Content

Only this section and explicitly quoted labels/messages elsewhere define literal on-screen copy. Directional guidance from earlier sections must not be rendered as visible text unless repeated here. Do not populate this table by lifting phrases from Content priority, Design intent, Anti-goals, Layout regions, or Acceptance criteria. If exact visible copy is missing, write `None specified` or add a gap note instead of inventing body or hint copy.

| Element | Copy |
|---|---|
| Page title | |
| Primary action label | |
| Empty state heading | |
| Empty state body | |
| Empty state CTA | |
| Error heading | |
| Error body | |
| Offline message | |
| Success message | |
| Confirmation heading | |
| Destructive action label | |
| Field labels / hints | |

### Screen generation prompt

> Target tool: [v0 / Lovable / Bolt / Claude Design / Google Stitch / other]

[One dense paragraph. Describe which actor is involved and what they are trying to do or affect. Describe what must be visible and how the screen must behave — not which components to use. Cover the primary action, critical variants, and how the screen handles offline, empty, and error states. Ground every requirement in the actor's context and constraints. No bullet points. No component or library names.]

### Acceptance criteria

Generate from the design intent, critical variants, and actor constraints above. Keep to 5–8 criteria. The actor-job criterion is always first. All criteria must be verifiable by looking at the generated screen — nothing that requires running code.

- [ ] [Actor name] can [primary job] without scrolling on a standard phone screen
- [ ] Primary action is the most visually prominent interactive element
- [ ] [Each critical variant] renders as a visually distinct state
- [ ] Empty state is shown when [condition] and includes [CTA label]
- [ ] Error state is shown when [condition] and explains what went wrong
- [ ] Long content and maximum realistic data still fit without overlap or clipped primary actions
- [ ] Focus, disabled, loading, success, and error feedback are visually defined for consequential actions
- [ ] [Offline indicator] is visible when connectivity is unavailable (if applicable)
- [ ] All content uses realistic mock data — no placeholder text

### Heuristic check

For each item mark ✓ (defined), ✗ (missing — flag as gap), or N/A (not applicable).

**1. Visibility of system status** — does every action and state transition have defined feedback?
- [ ] Every action has defined success feedback
- [ ] Every action has defined error feedback and recovery path
- [ ] All loading and saving states are described

**2. Match between system and real world** — does the content use the actor's domain vocabulary, not internal terms?
- [ ] Labels, actions, and copy use the actor's domain language
- [ ] No unexplained internal terminology

**3. User control and freedom** — can the user exit or undo anything consequential?
- [ ] Every destructive action has a cancel or confirmation path
- [ ] The user can return from every exit point listed

**4. Error prevention** — does the spec prevent errors, not just handle them?
- [ ] High-stakes actions have preconditions or confirmation before executing
- [ ] The spec does not rely solely on error states to handle foreseeable bad inputs

**5. Error recovery** — are error states specific enough to produce useful feedback?
- [ ] Every error state names the condition, the message, and the recovery path
- [ ] No error state is described only as "show error"

**6. Flexibility and efficiency** — given the actor's timing, session length, and constraints, is the path efficient?
- [ ] The primary path fits within the actor's typical session duration or operational timing
- [ ] No mandatory steps that don't serve the primary job

**7. Cognitive load** — can the actor make the main decision without excess memory or comparison work?
- [ ] The screen has one clear primary focus
- [ ] No decision point presents more than four ungrouped visible choices
- [ ] Required context is visible on the same screen; the actor does not need to remember it from a previous screen

**8. Responsive and accessibility resilience** — can the screen survive real device and input conditions?
- [ ] Touch targets meet the platform minimum
- [ ] Focus states are visible where keyboard or remote navigation is possible
- [ ] The layout accounts for safe areas, text expansion, and narrow viewports

**Heuristic gaps:**
[List failing items with what is missing. Write "None" if all pass.]
```

---

---

### proto.prepare

**Output:** `./docs/ux-ui/prepare-brief.md`
**Reads:** `docs/ux-ui/design.md`, `docs/ux-ui/app-outline.md`, `docs/ux-ui/screens/inventory.md`, `docs/ux-ui/screens/sitemap.md`, `docs/ux-ui/screens/[screen-name].md` (all in-scope screen files), `docs/ux-ui/stories/`, `docs/ux-ui/flows/`
**Also reads if present:** `docs/ux-ui/screens/contracts.md`

Self-contained alongside `docs/ux-ui/design.md`. A generation tool with only these two files should be able to generate the prototype without reading anything else.

For mock data: use realistic specific values. "Jane Okafor, Meridian Publishing, 14 titles, Active" not "[Name], [Company], [Count], [Status]".

**Template:**
```markdown
# Prototype Build Brief

> File: docs/ux-ui/prepare-brief.md
> Self-contained generation brief for v0, Lovable, Bolt, Claude Design, Google Stitch. Use alongside docs/ux-ui/design.md.

## Overview

**Product:**
**Goal:** [What someone should be able to do]
**Fidelity:** Lo-fi / Mid-fi / Hi-fi
**Target tool:** v0 / Lovable / Bolt / Claude Design / Google Stitch / other
**Primary story:** [Story file name]
**Primary flow:** [Flow file name]
**Screens:** [Page IDs]

## Design system summary

- Framework:
- Component library + version:
- Styling:
- Dark mode:
- Navigation:
- Primary color:
- Border radius:
- Font:

## Global UI decisions

Summarise the cross-screen decisions from docs/ux-ui/design.md that the generator must follow.

- Navigation model:
- Primary action hierarchy:
- Focus/input model:
- Data freshness:
- Loading/empty/error treatment:
- Offline/degraded treatment:
- Provider/source identity:
- Layout constraints:
- Copy conventions:

(Full detail in docs/ux-ui/design.md)

## Screens to build

| Order | ID | Name | Spec file | Entry? | Notes |
|---|---|---|---|---|---|
| 1 | PG01 | | docs/ux-ui/screens/[screen-name].md | Yes | |

## Core flow

1. User at [PG01] — [what they see]
2. [Action] → [PG02]
3. [Continue]

## Mock data

### [Object]

| Field | Value |
|---|---|

## States to show

| Screen | State | How |
|---|---|---|
| PG01 | Loaded | Default |
| PG02 | Empty | Zero records |

## Implement

| From | Trigger | To |
|---|---|---|

## Stub (appear but not function)
- [Action] on [PG03]: toast only
- [Action] on [PG04]: disabled

## Edge cases

| Case | Screen | How |
|---|---|---|

## Do not
- Generate screens not in the inventory
- Use components not in docs/ux-ui/design.md
- Use lorem ipsum
- Add navigation not in the design context

## Acceptance
- [ ] All screens render
- [ ] Primary flow completes end to end
- [ ] Visual style is consistent with docs/ux-ui/design.md requirements
- [ ] Empty, loading, and error states present on each screen
- [ ] Mobile layout correct at sm breakpoint
- [ ] Realistic mock data throughout
```

---

---

### proto.ui

**Output:**
- `./docs/ux-ui/ui-agent/README.md`
- `./docs/ux-ui/ui-agent/[screen-id]-[screen-name].md` — one file per in-scope screen

**Reads:** `docs/ux-ui/brief.md`, `docs/ux-ui/value-proposition.md`, `docs/ux-ui/design.md`, `docs/ux-ui/screens/inventory.md`, `docs/ux-ui/screens/sitemap.md`, `docs/ux-ui/screens/page-state-design-links.csv`, `docs/ux-ui/screens/[screen-name].md`, `docs/ux-ui/prepare-brief.md`
**Also reads if present:** `docs/ux-ui/build-brief.md`, `docs/ux-ui/patterns.md`

Use `./docs/ux-ui/` as the canonical project-relative output root. Do not write this package to any other folder unless the user explicitly overrides the root for that run.

This command compiles the canonical product specs into a UI-generation handoff package. It does not replace `docs/ux-ui/screens/*.md`. The canonical screen files remain the source of truth for product reasoning, flow traceability, actions, data, and states. The `ui-agent/` files are optimized for visual generation tools that perform better with a prescriptive screen rendering contract.

**Behaviour:**
- Does not follow the standard step pattern — no input question, no assumptions prompt, and no stop phrase.
- Read existing artifacts and write the compiled package immediately.
- Use `prepare-brief.md` as the canonical prototype brief. If `build-brief.md` exists, treat it as a legacy or alternate prototype brief and merge useful details, but prefer `prepare-brief.md` when the two conflict unless the user explicitly says otherwise. If neither exists, continue from design and screen files but include a gap note in `ui-agent/README.md` that global mock data is missing.
- Include only in-scope screens unless the user explicitly requests out-of-scope screens.
- Each screen contract must be self-contained enough to paste into a UI agent by itself.
- Preserve the source screen IDs and canonical screen names. Do not renumber screens.
- Do not copy `screens/page-state-design-links.csv` into `ui-agent/`. It remains canonical in `screens/`; use it to decide which states each UI-agent screen contract must render and link to it from `ui-agent/README.md`.

**Purpose of this package:**
- Make UI generation more consistent by front-loading visual language, exact states to render, layout regions, mock data, content, negative constraints, interaction states, robustness requirements, and acceptance criteria.
- Convert broad product-spec sections into a screen-by-screen rendering contract.
- Avoid changing the canonical screen specs into a format that is noisier for product and engineering handoff.

**README.md structure:**
```markdown
# UI Agent Handoff

> File: docs/ux-ui/ui-agent/README.md
> Generated from docs/ux-ui/design.md, docs/ux-ui/screens/*.md, and docs/ux-ui/prepare-brief.md or docs/ux-ui/build-brief.md.

## Product and Design Context
[Condensed product purpose, target platform, target users, visual tone, interaction model, accessibility constraints, global visual rules, and the cross-screen UI decisions from docs/ux-ui/design.md.]

## Generation Rules
- [Global do and do-not rules from design.md, patterns.md, and the prototype brief.]
- [Cross-screen UI decisions from design.md that every screen contract must follow unless explicitly overridden.]
- Do not render instruction fields as visible UI text. `User and usage context`, `Content priority`, `ANTI-GOALS`, data ranges, hardening notes, layout regions, and acceptance criteria are guidance. Quotation marks inside guidance do not make text visible copy. Literal visible text comes only from `CONTENT`, `COPY REQUIREMENTS`, explicit button/label/message entries, or copy labelled as title/body/button/label/message inside a state description.

## Screens

| ID | Screen | UI-agent file | States to render | Notes |
|---|---|---|---|---|
| PG01 | | docs/ux-ui/ui-agent/pg01-screen-name.md | | |

## Shared Mock Data
[Global mock data extracted from prepare-brief.md and, if present, build-brief.md.]

## Shared Navigation
[Core flow and route/transition summary from sitemap.md and the prototype brief. Include transition rules for back/cancel, resume, modal/sheet dismissal, interrupted flows, and destructive confirmations.]

## Acceptance
[Global acceptance criteria for the generated prototype.]

## Source Files
- docs/ux-ui/design.md
- docs/ux-ui/screens/inventory.md
- docs/ux-ui/screens/page-state-design-links.csv
- docs/ux-ui/prepare-brief.md or docs/ux-ui/build-brief.md
```

**Per-screen file structure:**
```markdown
# [Screen ID] [Screen Name]

PRODUCT AND DESIGN CONTEXT

[Repeat the concise product and design context needed for this screen. Include platform, visual tone, color rules, typography, navigation/input model, and any global negative constraints. Keep this practical, not brand-marketing copy.]

---

SCREEN CONTEXT

[Where this screen sits in the product: entry points, exit points, upstream/downstream screens, and why it matters in the primary flow.]

---

SCREEN SPECIFICATION — [SCREEN ID] [SCREEN NAME]

Screen ID: [PGxx] | [Platform priority, e.g. Mobile: Critical / TV: Critical] | Scope: [In scope]

Primary purpose: [One sentence]

Primary job: [The user job this screen must satisfy]

User and usage context:
- Primary actor: [Who is using or affected by the screen]
- State of mind: [Only what matters for UI decisions]
- Physical/device context: [Device, posture, connectivity, interruptions, accessibility constraints]

Content priority:
- PRIMARY: [must be immediately visible]
- SECONDARY: [supporting information/actions]
- TERTIARY: [low-priority controls/status]

Do not render the Content priority wording itself. Treat this section as hierarchy guidance unless exact copy is repeated under CONTENT or COPY REQUIREMENTS. Do not promote PRIMARY, SECONDARY, or TERTIARY phrases into CONTENT.

ANTI-GOALS:
- [Visual, structural, copy, or interaction direction the UI agent must avoid]

STATES TO RENDER — produce all listed states as distinct artboards or frames:

STATE 1 — [STATE NAME]
[Concrete rendering instructions: layout, content, controls, visual treatment, state-specific data, disabled/hidden actions, and what changes from the default.]

STATE 2 — [STATE NAME]
[Repeat for every critical variant/sub-state.]

ACTIONS:
- [Trigger] -> [result / destination / state transition]

IN-FLOW CONTEXTUAL ACTIONS:
- [Moment/object] -> [user-initiated affordance] -> [result] -> [return to preserved screen/state]
- Distinguish user-initiated contextual capture from system suggestions. An anti-goal against suggestions or interruptions does not automatically forbid a quiet action that appears only after the user selects, focuses, or explicitly opens controls.

TRANSITION CONTRACT:
- Entry from: [upstream screen/state and trigger]
- Primary forward path: [trigger -> destination screen/state]
- Back / exit path: [where the user returns and what state remains]
- Resume / re-entry path: [if applicable]
- Blocked / error path: [where the user stays or recovers]
- Forbidden transitions: [screens/actions the UI agent must not create]

DATA:
[Screen-specific data and whether it is local, cached, real-time, or user input.]

DATA RANGE AND EDGE CASES:
- Empty / zero data:
- Typical data:
- Maximum / dense data:
- Long text / overflow:
- Permission or partial data:

INTERACTION STATES:
- [Element/action]: default, focus, pressed/active, disabled, loading, success feedback, error feedback/recovery

RESPONSIVE AND HARDENING NOTES:
- Touch target / focus expectations:
- Mobile / tablet / desktop or platform-specific layout constraints:
- Safe-area, keyboard, remote, or viewport constraints:
- Offline, slow, duplicate-action, or concurrent-action handling:

VISUAL INDICATORS:
- [Indicator]: [meaning]

LAYOUT REGIONS:
- [Region]: [required content and purpose]

CONTENT:
- [Element]: [exact copy only, from a source Content/Copy section or explicit label/message]

Do not include optional body, hint, or caption copy unless exact visible copy is specified by the source artifacts. Use `None specified` or mark a gap when the source only gives intent or hierarchy guidance.

COPY REQUIREMENTS:
- Button labels:
- Error messages:
- Empty state:
- Confirmation / destructive copy:
- Offline / degraded copy:

MOCK DATA:
[Only the mock data needed for this screen, extracted from the prototype brief and screen file.]

FIDELITY:
[Lo-fi / Mid-fi / Hi-fi] — [visual completeness expectation and target tool if known.]

ACCEPTANCE CRITERIA:
- [Verifiable visual/product criterion]
```

**Compilation rules:**
- Convert each screen's `States` and `Critical variants` into explicit `STATES TO RENDER` sections. If `page-state-design-links.csv` lists sub-states that are missing from the screen file, include them and mark the missing detail as a gap.
- Use the prototype brief for shared mock data, global navigation, prototype fidelity, target tool, core flow, setup flow, edge cases, and global "Do not" constraints.
- Use the screen file for purpose, job, content priority, actions, in-flow contextual actions, transition contract, data, interaction states, screen robustness, visual indicators, layout regions, copy, and acceptance criteria.
- Use `screens/sitemap.md` and flow files to verify each screen's transition contract. If a UI-agent transition differs from the sitemap or a flow step, mark the mismatch as a gap instead of inventing a new path.
- Preserve in-flow contextual actions as lightweight branches. They should not become new global navigation, dashboards, tab bars, or required post-task steps unless the source screen explicitly says so.
- Preserve the copy boundary when compiling. Directional text in context, content priority, anti-goals, robustness, layout, and acceptance sections must not become UI copy. Do not promote content-priority phrases into CONTENT or COPY REQUIREMENTS. Move only confirmed visible labels/messages into CONTENT or COPY REQUIREMENTS; if exact source copy is missing, leave optional copy out or mark it as a gap.
- Use `design.md` for platform, visual tone, cross-screen UI decisions, color, typography, spacing, shape, navigation, input, focus, accessibility, and component constraints.
- Use `patterns.md` only for patterns that directly affect the screen type. Do not paste the whole pattern library into every screen.
- Make state instructions visually concrete. Prefer "row background changes to muted surface and Resume is the only enabled row action" over "show running state".
- Turn data ranges and robustness notes into renderable constraints. Prefer "show 12 visible rows plus clipped-safe scrolling; long names wrap to two lines" over "handle lots of data".
- If screen robustness or interaction-state details are missing, infer only from existing artifacts and mark the missing item as a gap rather than hiding it.
- Keep implementation details out unless they are explicit user-facing constraints. For example, a UI-agent screen can say "cached items remain visible" but should not mention Room, WorkManager, database IDs, or provider file IDs in user-facing copy.
- Preserve strong negative constraints from the product context and prototype brief. These are often what keep generated UI on-brief.
- Acceptance criteria must be checkable by looking at the generated screen or prototype. Do not include criteria that require backend code, real APIs, analytics, or persistence.
- Do not include lorem ipsum, placeholder bracket text, or generic examples. Use concrete mock data.

**When to rerun:**
- Rerun `proto.ui` after `proto.screens`, `proto.prepare`, `proto.change`, or any design/prototype-brief update that changes visual direction, state coverage, navigation, mock data, or acceptance criteria.
- Run `proto.continuity` after `proto.ui` and after any generated UI feedback that suggests screens do not connect smoothly.

---

---

### proto.continuity

**Output:** `./docs/ux-ui/flow-continuity-review.md`
**Reads:** `docs/ux-ui/flows/`, `docs/ux-ui/stories/`, `docs/ux-ui/screens/inventory.md`, `docs/ux-ui/screens/sitemap.md`, `docs/ux-ui/screens/page-state-design-links.csv`, `docs/ux-ui/screens/[screen-name].md`, `docs/ux-ui/prepare-brief.md`
**Also reads if present:** `docs/ux-ui/ui-agent/`, `docs/ux-ui/patterns.md`, `docs/ux-ui/data/states.md`, screenshots or notes the user provides from generated UI output

No external input needed. Read the artifacts and write the review immediately. Do not edit specs during this command; produce a repair plan that can be applied with `proto.change` or direct user-requested edits.

**Purpose:**
Catch breaks that make generated screens feel disconnected: missing destinations, mismatched action labels, skipped intermediate states, undefined back/cancel behaviour, dead ends, accidental loops, modal dismissal gaps, resume/re-entry ambiguity, and UI-agent files that drift from canonical flow/screen specs.

**Checks to run:**
- Build a transition ledger from flows, `screens/sitemap.md`, screen `Actions`, screen `Transition contract`, and UI-agent `ACTIONS` / `TRANSITION CONTRACT` sections.
- Verify every flow step that changes screen or state has a matching source screen, trigger, destination, and resulting state.
- Verify every screen action with a destination appears in `screens/sitemap.md` or is explicitly marked as local-only.
- Verify every sitemap transition appears in the source screen's actions and the destination screen's entry context.
- Verify labels and action names are consistent enough that a UI agent will not create separate controls for the same action.
- Verify back, cancel, close, exit, retry, resume, and destructive-confirmation paths are defined where relevant.
- Verify interruptible flows have a re-entry state and do not restart users at the wrong screen.
- Verify loading, empty, offline, error, permission, and concurrent-action branches have a recovery or exit path.
- Verify generated `ui-agent/` files do not invent screens, actions, routes, navigation elements, or tab bars that are absent from canonical artifacts.
- Verify the primary happy path can be walked end to end without relying on unstated transitions.
- Flag any transition where the destination screen's content priority or state does not match the action that led there.
- Scan for in-flow intent problems: capture, save, tag, annotate, bookmark, quote, clip, attach, or reuse actions that are only offered after the primary task, even though the target object exists earlier on a writing, reading, review, media, map, list, or editing surface.
- Verify contextual actions preserve the original context: cursor position, selected text, scroll position, draft content, playback position, focused item, or route state.
- Flag contradictions where an anti-goal correctly blocks system suggestions but accidentally blocks user-initiated contextual capture.

**Issue severity:**
- Critical: the primary path cannot be completed, a destination screen is missing, or the UI-agent handoff invents a conflicting navigation model.
- Important: a branch, return path, re-entry path, or error recovery is ambiguous enough that generated UI may feel broken.
- Minor: naming, label, or notes inconsistency that could confuse generation but does not block the path.

**Template:**
```markdown
# Flow Continuity Review

> File: docs/ux-ui/flow-continuity-review.md
> Reviewed: flows, sitemap, screen specs, prepare brief, and UI-agent handoff if present.

## Verdict

Ready / Needs fixes / Blocked

## Primary path walkthrough

| Flow | Step | Source | Trigger | Expected destination / state | Found | Issue |
|---|---|---|---|---|---|---|
| [flow file] | 1 | [screen/state] | [action] | [screen/state] | Yes/No | |

## Transition ledger

| From | Trigger | To | Resulting state | Back / exit | Sources |
|---|---|---|---|---|---|
| [screen/state] | [action/event] | [screen/state] | [state] | [path] | [flow, sitemap, screen] |

## Critical breaks
- [ ] [Issue] — source: [file] — fix: [specific change]

## Important smoothness issues
- [ ] [Issue] — source: [file] — fix: [specific change]

## UI-agent drift
- [ ] [Generated handoff mismatch, invented action, missing transition, or contradicted navigation rule]

## In-flow intent issues
- [ ] [Secondary intent delayed or separated from the object of attention] — source: [file] — better treatment: [contextual action / inline branch / sheet / keep separate]

## Dead ends and loops
- [Screen or flow] — [why the user can get stuck or loop unexpectedly]

## Missing return / recovery paths
- [Action/state] — [missing back, cancel, retry, resume, or exit behaviour]

## Repair plan
1. [Smallest canonical artifact change needed]
2. [Regenerate with proto.ui if UI-agent files are stale]
3. [Rerun proto.continuity]

## Open questions
1.
```

---

---

### proto.generate

**Output:** stdout only — no file is written to disk
**Usage:** `proto.generate [screen-name]` e.g. `proto.generate map-workspace`
**Reads:** `docs/ux-ui/design.md`, `docs/ux-ui/screens/[screen-name].md`, `docs/ux-ui/prepare-brief.md`
**Also reads if present:** `docs/ux-ui/screens/sitemap.md`, `docs/ux-ui/patterns.md`

Packages the context from three or four files into a single ready-to-paste generation prompt for a named screen. The output is formatted to paste directly into Claude Design, Google Stitch, v0, Lovable, Bolt, or any other UI generation tool.

**Behaviour:**
- Does not follow the standard step pattern — no input question, no assumptions, no stop phrase
- Reads the named screen file and the supporting files, then immediately produces the prompt
- If the screen file does not exist, list the available screens from `docs/ux-ui/screens/inventory.md` and ask which one to generate
- If `docs/ux-ui/prepare-brief.md` does not exist, generate the prompt without it and note that mock data is unavailable
- If `docs/ux-ui/screens/sitemap.md` does not exist, generate the prompt without navigation context

**Output format:**

Print the prompt directly — no preamble, no explanation. Just the prompt, ready to copy.

The prompt has four sections assembled from the source files:

**Section 1 — Product and design context** (from design.md, and patterns.md if present)
A short paragraph covering: what the product is, who uses it, the visual tone, platform and environment, and the key interaction and accessibility requirements. Keep it to 3–5 sentences. If patterns.md exists, append a short "Patterns to follow" paragraph with the relevant patterns and anti-patterns for this screen type — omit patterns that don't apply.

**Section 2 — Screen context** (from sitemap.md if present)
One or two sentences covering where this screen sits: what leads to it and where it goes. Derived from the Screen connections list in sitemap.md. Omit if sitemap.md is not present.

**Section 3 — Screen specification** (from [screen-name].md)
The full design intent, states, actions, data, variants, layout regions, and content table from the screen file. Paste these sections in full — do not summarise. The generation prompt section from the screen file becomes the closing instruction paragraph.

**Section 4 — Mock data** (from prepare-brief.md)
The relevant mock data object(s) for this screen. Extract only the data that applies to this screen — do not include the full brief. One or two sentences on fidelity target and target tool if specified.

**Separator between sections:** `---`

**After the prompt**, on a new line, print:
```
--- copied prompt ends here ---
Generating: [screen-name] | Tool: [target tool or "not specified"] | Files used: design.md, [screen-name].md[, prepare-brief.md][, sitemap.md]
```

This trailer is for the user's reference and should not be included when pasting into the generation tool.

---
