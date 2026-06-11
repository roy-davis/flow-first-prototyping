# Journey, Story, Outline, Flow, and State Commands

Detailed templates and behavior for journey maps, prototype-driving stories, rough app outline, flows, and workflow state models.

---

### proto.journeys

**Output:**
- `./docs/ux-ui/journeys/overview.md`
- `./docs/ux-ui/journeys/[actor]-[scenario].md` — one file per journey
- `./docs/ux-ui/journeys/journey-map.xlsx` — review-friendly companion workbook generated from the Markdown journeys

**Reads:** `docs/ux-ui/actors/`

**File naming:** slugify actor name + scenario description.
- `andy-discovers-the-app.md`
- `rachel-approves-a-request.md`
- `sync-worker-indexes-content.md`
- `felix-logs-a-field-issue.md`

**Journey boundary:** A journey starts before the actor uses the app. It begins in the actor's environment where the problem exists, the trigger appears, and the actor decides whether the app is needed. It ends after the actor has completed the task, the original problem is resolved, and any follow-up, confirmation, or real-world handoff has happened.

**Relationship to stories and flows:** A journey is the "why and what" — the actor's environment, experience, questions, stakes, and where friction exists. Stories are prototype-sized task slices pulled from journey stages. A flow is the "how" — the precise sequence of product steps, branches, and system responses that implements one story. The chain is `Journey → Story → Flow`.

**Required fields per journey:**
- Name, real-world trigger, primary actor, starting context, resolved end state
- Stages (4–8): each as prose (3–5 sentences) covering what the actor is doing, what question is in their head, what they need to know, and what could go wrong
- First stage: before app use, in the actor's real-world environment where the problem exists
- Middle stages: app-supported work and transitions between app and real-world activity
- Final stage: after app use, where the task has been completed and the original problem is resolved
- Data needed and friction risk per stage
- Moments that matter — highest-stakes transitions where trust is built or broken
- Story opportunities — multiple prototype-sized tasks or scenarios implied by the journey; do not collapse all stages into one story
- Screens implied
- Stories and flows that implement this journey (filled in by later commands)

**Format:** Write stages as prose paragraphs, not table rows. No emotion column. Do not include button sequences or exact UI mechanics; those belong in flows and screen specs.

**Canonical source rule:** Markdown journey files are the source of truth for the `proto.*` workflow. The workbook is a companion output for stakeholder review, intranet storage, workshop discussion, and stage-by-stage comparison. Do not make downstream commands depend on reading the workbook when the Markdown files exist.

**Workbook rule:** Generate `docs/ux-ui/journeys/journey-map.xlsx` every time `proto.journeys` runs. The workbook should be readable as a formatted customer journey map, not a raw export of Markdown and not a list/data dump. Use one `Overview` sheet plus one worksheet per journey. If there is only one journey, still include `Overview` and one journey worksheet.

Use spreadsheet tooling to create the `.xlsx`; do not handwrite spreadsheet XML or rename CSV files.

**Workbook structure:**
- `Overview` sheet: Journey file, Journey name, Primary actor, Real-world trigger, Starting context, Resolved end state, Story candidates, Notes.
- One formatted sheet per journey, with stages as columns and journey dimensions as rows, following the matrix layout from the provided customer journey map example.
- Use short, workbook-safe sheet names, e.g. `Andy discovers`, `Rachel approves`.
- Keep stage names as column headers. Keep long prose wrapped in cells.
- Include a simple satisfaction row only when source material or user input supports it. Do not invent scores.

**Per-journey worksheet layout contract:**
- Do not output the journey worksheet as a plain table of records, a list of fields, or a dump of Markdown sections.
- Use the visual matrix format:
  - Row 1: merged title across the stage columns, e.g. `Customer Journey Map: [Journey name]`.
  - Row 2: merged scenario/context line across the stage columns.
  - Left column: journey dimension labels.
  - Columns B onward: journey stages in chronological order.
  - Row 3: `Journey Stage` with stage names across columns.
  - Row 4: `Timeframe` or `Context`.
  - Rows 5 onward: journey dimensions, with each stage's content in the corresponding stage column.
- If stages are grouped into broader phases, merge the phase headers across the relevant stage columns only when that improves readability. Otherwise keep one stage per column.
- Apply wrapped text, readable column widths, visible borders, and light header styling so the workbook feels like a customer journey map template.
- Preserve the supplied workbook's style and merged-cell pattern when the user provides a journey-map template. Populate the template rather than replacing it with a generic data table.

**Per-journey worksheet rows:**
1. Journey stage
2. Timeframe / context
3. Actor goal
4. Key touchpoints
5. Actor actions
6. Thoughts / questions
7. Mood / pain points
8. Data needed
9. Friction risk
10. Opportunities
11. Story opportunities
12. Screens implied
13. Internal owner / source / confidence
14. Success metrics
15. Satisfaction score (1-5), only if researched or supplied

If workbook generation is technically blocked, still write the Markdown journey outputs and report `journey-map.xlsx` as a generation blocker in the final command response.

**Template (overview.md):**

> The Story file(s) and Flow file(s) columns start empty when journeys are generated. proto.stories fills Story file(s). proto.flows fills Flow file(s) only if it updates this overview directly. Do not invent downstream file names when generating journeys.

```markdown
# Journey Overview

> File: docs/ux-ui/journeys/overview.md

| Journey file | Journey name | Primary actor | Story file(s) | Flow file(s) | Real-world trigger | Resolved end state |
|---|---|---|---|---|---|---|
| andy-discovers-the-app.md | | Andy the App User | — | — | | |
| rachel-approves-a-request.md | | Rachel the Receptionist | — | — | | |
```

**Template (per journey file):**
```markdown
# Journey: [Name]

> File: docs/ux-ui/journeys/[actor]-[scenario].md
> Primary actor: [Actor name]
> Real-world trigger: [What causes this journey to start before app use]
> Starting context: [Where the actor is, what is happening, and why the problem matters]
> Resolved end state: [What success looks like after the task is complete and the problem is resolved]

## Stages

### Stage 1: [Name]
[Pre-app prose: where the actor is, what problem exists, what question is in their head, why they may need the app, and what could go wrong. 3–5 sentences.]

**Data needed:** [What information must be available at this stage]
**Friction risk:** [What could cause the actor to stall or fail]

### Stage 2: [Name]
[Same structure. Include app-supported work and real-world transitions. 4–8 stages total.]

## Moments that matter
- **[Stage or transition]:** [Why it matters and what is at stake]

## Story opportunities

| Stage | Story candidate | Why it matters |
|---|---|---|
| [Stage name] | [Prototype-sized task or scenario] | [Why this should become a story] |

## Screens implied

| Stage | Screen needed |
|---|---|
| [Stage name] | [Screen name] |
```

---

---

### proto.stories

**Output:**
- `./docs/ux-ui/stories/overview.md`
- `./docs/ux-ui/stories/[actor]-[story].md` — one file per prototype-driving story

**Reads:** `docs/ux-ui/actors/`, `docs/ux-ui/journeys/`

**File naming:** slugify actor name + story goal.
- `andy-starts-a-planned-session.md`
- `rachel-approves-a-request.md`
- `sync-worker-recovers-a-failed-sync.md`

**Relationship to journeys and flows:** A story is the bridge between broad journey context and precise product flow. It turns one journey stage or story opportunity into a buildable task slice with clear value, acceptance criteria, data, and edge cases. Flows implement stories; screen specs come from flows.

Use "story" in the product/prototype sense, not a verbose Agile backlog item. Keep it concrete enough that a designer or UI agent can understand what must exist on screen and why.

**Granularity rule:** A story is one prototype-sized task slice from one journey opportunity. It is not a full rewrite of the journey and should not include the full step-by-step flow. One journey may produce one story in a very small prototype, but larger journeys commonly produce multiple stories.

**Story sizing rule:** Write the smallest story that still produces a meaningful screen/flow. A story should have one actor, one trigger, one primary user-visible outcome, and usually one primary screen or one adjacent screen transition. Split the story if the task uses "and", "then", or "through" to chain multiple intents; if it includes more than one primary decision; if it spans more than two screens; or if acceptance criteria mix discovery, browsing, selection, confirmation, playback, setup, sync, and repair outcomes.

**Required splits:**
- Split "browse and start book" into library scan, book detail review, and start/resume selected book.
- Split "connect source" into source choice, credential/auth validation, folder selection, sync/indexing, and review/import outcomes.
- Split "discover and add book" into discovery/indexing, review discovered book, and add to listening library unless every indexed book is automatically in the library.
- Keep source repair branches separate when the recovery action changes screen or actor authority.

**Required fields per story:**
- Story name, primary actor, journey reference, journey stage reference
- One task slice this story covers
- Real-world trigger and problem
- User story statement or job story statement
- Value and outcome
- Preconditions
- Acceptance criteria
- Data needed
- In-flow intent opportunities
- Edge cases and failure conditions
- Flow files that implement this story

**After writing story files:** update `docs/ux-ui/journeys/overview.md` to add story filenames to the Story file(s) column for each matching journey. If the journey overview does not have a Story file(s) column, add it. Do not update Flow file(s) here.

**Template (overview.md):**
```markdown
# Story Overview

> File: docs/ux-ui/stories/overview.md

| Story file | Story name | Primary actor | Journey file | Journey stage | Flow file(s) | Priority |
|---|---|---|---|---|---|---|
| andy-starts-a-planned-session.md | | Andy the App User | andy-trains-a-session.md | | — | Must-have |
```

**Template (per story file):**
```markdown
# Story: [Name]

> File: docs/ux-ui/stories/[actor]-[story].md
> Primary actor: [Actor name]
> Journey: [Journey file name]
> Journey stage: [Stage name]
> Priority: Must-have / Should-have / Nice-to-have

- Task slice: [The one prototype-sized task this story covers]
- Real-world trigger: [What happens in the actor's environment]
- Problem: [The unresolved problem that creates the need for the app]
- Story statement: As [actor], I want to [do the task], so I can [resolve the problem or make progress].
- Value: [Why this matters to the actor and product]
- Outcome: [What is true after the story is complete]
- Preconditions: [What must already be true; separate with semicolons]
- Acceptance criteria:
  - [Observable product or behavior criterion]
  - [Observable product or behavior criterion]
- Data needed: [Data, source, and freshness if relevant]
- In-flow intent opportunities: [Optional secondary actions that may arise while the actor is focused on an object; write None if not applicable]
- Edge cases: [Zero data, permission issue, offline/degraded, duplicate action, long text, failed validation, or other likely issue]
- Flow files: [Filled by proto.flows]
```

---

---

### proto.outline

**Output:** `./docs/ux-ui/app-outline.md`
**Reads:** `docs/ux-ui/actors/`, `docs/ux-ui/journeys/`, `docs/ux-ui/stories/`

proto.outline is an early app-shape sanity check. It consolidates journey "screens implied" hints and story tasks into a rough product structure before flows, state models, screen inventory, and complete screen specs make the design harder to change.

This is not the committed screen inventory and not a component plan. Keep it high level. Use it to catch missing surfaces, overcomplicated structure, unclear navigation, and product-shape assumptions while they are still cheap to change.

**Input question:**
> Do you have existing app structure, information architecture, navigation, rough screens, or product-shape notes to include? Share a file path, paste content, or say "nothing."

**Required fields:**
- App shape summary — one short paragraph
- Likely top-level areas or surfaces
- Rough screen candidates
- Story coverage by surface
- What should not become a screen
- In-flow actions that should remain contextual instead of becoming standalone screens
- Navigation / entry model hypothesis
- Structural risks and missing surfaces
- Questions to resolve before flows and screen inventory

**Template:**
```markdown
# App Outline

> File: docs/ux-ui/app-outline.md
> Purpose: early app-shape sanity check before flows and screen inventory
> Status: rough, non-final; screen inventory is the committed source later

## App shape summary

[One short paragraph describing the likely product structure implied by actors, journeys, and stories.]

## Likely top-level areas

| Area / surface | Purpose | Primary actors | Stories supported | Notes |
|---|---|---|---|---|
| [Area name] | | | | |

## Rough screen candidates

| Candidate screen | Why it might exist | Supporting stories | Confidence | Notes |
|---|---|---|---|---|
| [Screen candidate] | | | High / Medium / Low | |

## Story coverage by surface

| Story | Likely area / surface | Needs new surface? | Notes |
|---|---|---|---|
| [story file] | | Yes / No / Unsure | |

## Should not become screens

| Candidate / idea | Why not | Better treatment |
|---|---|---|
| [Thing] | [Reason] | [State, inline control, modal, copy, system behavior, or out of scope] |

## In-flow action candidates

Use this to catch secondary intents that arise while the actor is focused on a specific object. These may become contextual actions, inline affordances, sheets, or lightweight branches rather than separate navigation surfaces.

| Moment / object of attention | Secondary intent | Better treatment | Return behaviour |
|---|---|---|---|
| [e.g. selected text, reviewed item, map point, media segment] | [save, capture, annotate, tag, attach, reuse] | [contextual action / inline control / sheet / state] | [preserve cursor, scroll, selection, playback, or task state] |

## Navigation and entry hypothesis

- Primary entry point:
- Secondary entry points:
- Likely navigation model:
- Deep links or system-triggered entry:
- Back/exit behavior:

## Structural risks

- [Risk] — [why it could cause rework later]

## Questions before flows and inventory

1. [Question] — default if accepted: [default]
```

---

---

### proto.flows

**Output:** one file per flow at `./docs/ux-ui/flows/[actor]-[scenario].md`
**Reads:** `docs/ux-ui/actors/`, `docs/ux-ui/journeys/`, `docs/ux-ui/stories/`

**File naming:** Match the story file name where possible — one story, one primary flow. Use a suffix for secondary flows on the same story.
- `andy-starts-a-planned-session.md` — primary flow for that story
- `andy-starts-a-planned-session-offline.md` — variant flow covering the offline branch
- `rachel-approves-a-request.md`
- `sync-worker-indexes-content.md`

**Relationship to stories and journeys:** A flow is the precise implementation of a story. Each flow references the story it implements and maps its steps back to the relevant journey stage where helpful. The overlap is intentional — the journey captures context, the story captures the task slice and acceptance criteria, and the flow captures the exact sequence the system must support.

User flows are expected to be large. Each flow should be complete, but should not re-explain actor motivation beyond the story and journey references.

**Required fields per flow:**
- Story reference — which story file this flow implements
- Journey reference — which journey file and stage the story came from
- Trigger
- Entry point
- Preconditions
- Steps — numbered list, each step noting which story acceptance criterion or journey stage it supports where helpful
- Decision points
- In-flow opportunities and interruption risks
- Branches — condition: consequence pairs
- Error paths
- Exit states
- Completion criteria

**After writing each flow file:** update `docs/ux-ui/stories/overview.md` to add this flow's filename to the Flow file(s) column for the matching story row, and update the matching story file's `Flow files` line. If `docs/ux-ui/journeys/overview.md` has a Flow file(s) column, optionally add the flow there too, but treat the story overview as the canonical story-to-flow link.

**Format rules:**
- Flat bullet list per flow, consistent named fields — no tables, no nested headers
- Steps numbered inline, annotated with journey stage reference where helpful
- Branches as condition: consequence on one line
- Keep each field scannable — one line where possible

**Template (per flow file):**
```markdown
# Flow: [Name]

> File: docs/ux-ui/flows/[actor]-[scenario].md
> Primary actor: [Actor name]
> Story: [Story file name]
> Journey: [Journey file name]
> Implements: [Story acceptance criteria or journey stage names this flow covers, comma-separated]

- Trigger: [What causes this flow to start]
- Entry point: [Screen or state where the flow begins]
- Preconditions: [What must be true; separate with semicolons]
- Steps:
  1. [First action] ← [Journey stage name]
  2. [Second action]
  3. [Third action] ← [Journey stage name]
  4. [Continue for all steps]
- Decision points: [Comma-separated list of choices the user makes]
- In-flow opportunities: [Secondary actions that arise while focused on a specific object; preferred contextual treatment; write None if not applicable]
- Interruption risks: [Steps that may pull the actor out of the primary flow; how the flow preserves or restores the original context]
- Branches:
  - [Condition]: [Consequence]
  - [Condition]: [Consequence]
- Error paths: [Comma-separated list of specific failure conditions]
- Exit states: [All possible end states, separated by semicolons]
- Completion criteria: [One sentence defining what a completed flow looks like]
```

---

---

### proto.states

**Output:** `./docs/ux-ui/data/states.md`
**Reads:** `docs/ux-ui/flows/`, `docs/ux-ui/actors/`

**When to run:** After proto.flows, before proto.design and proto.screens. Screen specs reference states directly — the States table, Critical Variants, and the screen generation prompt all depend on knowing what states exist and what the user can do in each one. Running this before screens means the screen spec draws from a defined model rather than guessing.

**Required fields per object:**
- Object name
- All states with entry/exit conditions
- Transitions: from, trigger, to, actor, guard condition
- Actions per state: allowed / blocked (show disabled) / hidden
- Terminal states

Do not expand states into copywriting, layout, or visual design. Keep states focused on object lifecycle and action availability.

**Distinguish precisely:**
- Allowed — available and enabled
- Blocked — exists but cannot be taken in this state (render disabled)
- Hidden — does not appear at all in this state

**Template:**
```markdown
# Workflow State Model

> File: docs/ux-ui/data/states.md

## Objects

| Object | States | Terminal states |
|---|---|---|

---

## Object: [Name]

### States

| ID | Name | Description | Entry | Exit |
|---|---|---|---|---|
| S1 | | | | |

### Transitions

| From | Trigger | To | Actor | Guard |
|---|---|---|---|---|

### Actions per state

| State | Allowed | Blocked | Hidden |
|---|---|---|---|

### Diagram

```
[S1: Name] --(trigger)--> [S2: Name]
[S2: Name] --(trigger)--> [S3: Name]
```

### Terminal states

| State | Description | UI behaviour |
|---|---|---|
```

---
