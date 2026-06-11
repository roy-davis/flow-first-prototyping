# Flow-First Prototyping

Flow-First Prototyping is a Codex skill for rapid product prototyping. Its goal is to quickly move from an idea, PRD, rough notes, or existing UX artifacts to a visualized product concept that can be reviewed, generated, and iterated on.

Instead of starting with a static screen list, the skill starts with people, goals, and behavior. It builds actors, journeys, small user stories, flows, state models, screen inventories, screen specifications, and UI-generation prompts from the way users actually move through a product.

All generated artifacts are written to:

```text
./docs/ux-ui/
```

You can start from almost nothing, from a polished PRD, or from artifacts that already exist. Paste notes into the conversation, point to files, upload source material, or ask the skill to infer from what is already in `docs/ux-ui/`.

## Why This Exists

Most early prototypes jump too quickly to screens. That can make a product look plausible before the core behavior is understood. This skill is designed to create just enough structure before screen generation so visual prototypes have a coherent reason to exist.

The workflow helps answer:

- Who is using the product?
- What are they trying to accomplish?
- What journey are they in before, during, and after app use?
- What small stories make up that journey?
- What exact flows, states, failures, and recovery paths exist?
- Which screens are actually needed?
- What should a UI generation agent render?
- Where are the continuity gaps before design or engineering spend more time?

The result is a prototype artifact set that can feed visual generation tools, design review, product iteration, or engineering handoff.

## How It Evolves an Idea

The skill turns an idea into UI-generation material through a flow-first chain:

```text
idea / PRD / existing artifacts
  -> brief
  -> actors
  -> journeys
  -> small stories
  -> app outline
  -> flows
  -> object states
  -> design context
  -> screen inventory and sitemap
  -> screen specifications
  -> prototype build brief
  -> UI-agent prompts
  -> continuity and readiness reviews
```

### Actors

Actors are the people, systems, integrations, workers, or services that initiate actions, make decisions, or materially affect the product. Human actors get realistic context. Non-human actors, such as sync workers, provider APIs, agents, or devices, are represented operationally.

### Journeys

Journeys capture the real-world arc: the situation, motivation, before-and-after context, risks, and stages. A journey can remain broad, such as "connect a library" or "recover from playback failure."

### Stories

Stories are intentionally smaller than journeys. A good story has one actor, one trigger, one primary outcome, and usually one screen or one adjacent screen transition. The skill splits large chains such as "browse and start", "connect and index", or "discover and add" into separate prototype-sized stories.

### Flows

Flows define the exact product sequence for each story: entry point, decisions, branches, errors, exit states, and screen transitions. This is where vague intent becomes behavior a prototype can render.

### States

States describe object lifecycles and what actions are allowed, blocked, or hidden in each state. This prevents screens from only showing the happy path.

### Screens

Screens are derived from the flows and states. The skill creates a screen inventory, sitemap, individual screen specs, and a `page-state-design-links.csv` tracker that includes one row for every page and every state.

### UI-Generation Prompts

The skill compiles screen specs into `docs/ux-ui/ui-agent/`. These files are written for UI-generation agents and visual prototyping tools. They describe what each screen must render, which states need distinct frames, what copy is literal, and which transitions must stay coherent.

## Starting Points

You can use the skill in several ways.

### Start From A Rough Idea

Use this when you only have a product concept or a few notes.

```text
proto.oneshot
```

Then paste the idea when asked. The skill will infer the artifact chain and mark assumptions as provisional.

### Start From A PRD Or Existing File

Use this when you already have a source document.

```text
proto.oneshot use prd.md
```

You can point to any available local file or uploaded artifact. The skill reads it as source material and builds the artifact set from it.

### Start From Existing UX/UI Artifacts

Use this when `docs/ux-ui/` already exists or you have prior journeys, stories, flows, screen lists, or design notes.

```text
proto.oneshot use prd.md and existing docs/ux-ui artifacts
```

The skill can reuse existing artifacts as source, regenerate them, or update them depending on the command you run.

### Work Step By Step

Use this when you want review checkpoints after each stage.

```text
proto.brief
proto.actors
proto.journeys
proto.stories
proto.outline
proto.flows
proto.states
proto.design
proto.map
proto.screens
proto.prepare
proto.ui
proto.continuity
```

This is slower than `proto.oneshot`, but it gives the most control.

### Work In Sprint Mode

Use this when you want grouped checkpoints rather than command-by-command control.

```text
proto.sprint
```

Sprint mode runs the prototype chain in five grouped steps:

1. Foundation
2. User understanding
3. Structure
4. Design
5. Screens, handoff, and continuity

Each step pauses for review before the next step.

### Change An Existing Prototype

Use this when the artifact set already exists and a requirement changes.

```text
proto.change add QR-code authorization for cloud providers
```

The skill performs impact analysis first, shows which files need to change, waits for confirmation, and then updates only the affected artifacts.

### Generate One Screen Prompt

Use this when you want a focused prompt for one screen after the screen specs exist.

```text
proto.generate PG08
```

This prints a single generation prompt and writes no files.

### Prepare Engineering Handoff

After the prototype has stabilized, generate implementation-facing artifacts.

```text
proto.contracts
proto.data
proto.actions
proto.review
```

These add page contracts, data requirements, action specifications, and a readiness review.

## Setup

Install the skill folder under your Codex skills directory:

```text
~/.codex/skills/flow-first-prototyping/
```

For a project, add an `AGENTS.md` note like this:

```md
# Agents

Use the skill at ~/.codex/skills/flow-first-prototyping/SKILL.md

All proto.* commands are available. Read from and write to ./docs/ux-ui/
```

Then run commands in Codex using the `proto.*` namespace.

## Output Structure

The main generated tree is:

```text
docs/ux-ui/
  brief.md
  value-proposition.md
  design.md
  app-outline.md
  actions.md
  prepare-brief.md
  flow-continuity-review.md
  readiness-review.md
  patterns.md

  actors/
    [actor-name].md
    permissions.md

  journeys/
    overview.md
    journey-map.xlsx
    [actor]-[scenario].md

  stories/
    overview.md
    [actor]-[story].md

  flows/
    [actor]-[scenario].md

  screens/
    inventory.md
    sitemap.md
    contracts.md
    page-state-design-links.csv
    [screen-name].md

  data/
    requirements.md
    states.md

  ui-agent/
    README.md
    [screen-id]-[screen-name].md
```

## Ways To Progress Through The Flow

### 1. One-Shot Prototype

Best when you want speed and can tolerate provisional assumptions.

Use:

```text
proto.oneshot use prd.md
```

This runs the full artifact chain in one pass. It is the fastest way to get from idea to visual-generation-ready prompts.

### 2. Sprint Prototype

Best when you want momentum but still need review gates.

Use:

```text
proto.sprint
```

This groups the workflow into five checkpoints. It is useful for workshops, early product shaping, or collaborative review.

### 3. Command-By-Command Prototype

Best when the problem is complex, high risk, or still being discovered.

Use the recommended command sequence:

```text
proto.brief -> proto.actors -> proto.journeys -> proto.stories -> proto.outline -> proto.flows -> proto.states -> proto.design -> proto.map -> proto.screens -> proto.prepare -> proto.ui -> proto.continuity
```

This gives you maximum control and lets you correct the direction after each artifact.

### 4. Existing Artifact Refresh

Best when you already have prior UX work, generated artifacts, or a `docs/ux-ui/` folder.

Use:

```text
proto.oneshot use prd.md and existing docs/ux-ui artifacts
```

or make targeted updates with:

```text
proto.change [what changed]
```

This lets the skill use existing artifacts as context instead of starting over from a blank page.

### 5. UI Generation Handoff

Best when the prototype behavior is clear and you want visual output.

Use:

```text
proto.ui
```

The skill compiles canonical artifacts into `docs/ux-ui/ui-agent/`, including one file per screen with states, transitions, copy boundaries, mock data, and acceptance criteria.

## Commands

### `proto.help`

Prints the command table, recommended flows, behavior matrix, and output root. It writes no files.

### `proto.status`

Scans `docs/ux-ui/` and reports which artifact groups are present or missing. Use this before continuing work in an existing project.

Produces:

```text
stdout status report
```

### `proto.brief`

Creates the foundation product brief. It captures the product idea, target users, scope, goals, assumptions, and prototype direction.

Produces:

```text
docs/ux-ui/brief.md
```

### `proto.value`

Creates a stakeholder-facing value proposition. Use this when the product framing, promise, or differentiation needs to be explicit before prototyping.

Produces:

```text
docs/ux-ui/value-proposition.md
```

### `proto.design`

Creates the cross-screen design context: platform, visual language, navigation model, state treatment, copy rules, accessibility posture, and constraints for generation.

Produces:

```text
docs/ux-ui/design.md
```

### `proto.actors`

Creates actor profiles and permissions. Actors can be human users, non-human workers, provider APIs, devices, services, or agents.

Produces:

```text
docs/ux-ui/actors/[actor-name].md
docs/ux-ui/actors/permissions.md
```

### `proto.journeys`

Creates real-world journey arcs for the actors. Journeys describe the user situation, stages, stakes, before/after context, and emotional or operational shifts.

Produces:

```text
docs/ux-ui/journeys/overview.md
docs/ux-ui/journeys/[actor]-[scenario].md
docs/ux-ui/journeys/journey-map.xlsx
```

### `proto.stories`

Creates small prototype-sized stories from the journeys. Stories are deliberately split so each one has one actor, one trigger, one primary outcome, and a focused flow/screen concern.

Produces:

```text
docs/ux-ui/stories/overview.md
docs/ux-ui/stories/[actor]-[story].md
```

### `proto.outline`

Creates the early app shape. It identifies likely surfaces, navigation hypotheses, feature boundaries, and things that should not become screens.

Produces:

```text
docs/ux-ui/app-outline.md
```

### `proto.flows`

Creates exact product flows for the stories. Flows define steps, branches, error paths, exits, and screen transitions.

Produces:

```text
docs/ux-ui/flows/[actor]-[scenario].md
```

### `proto.states`

Creates object and system state models. It defines lifecycle states, allowed actions, blocked actions, hidden actions, and recovery conditions.

Produces:

```text
docs/ux-ui/data/states.md
```

### `proto.map`

Creates the screen inventory and sitemap from the flows and states. This is where the prototype becomes a set of canonical screens.

Produces:

```text
docs/ux-ui/screens/inventory.md
docs/ux-ui/screens/sitemap.md
```

### `proto.screens`

Creates one screen specification per in-scope screen. Each spec defines purpose, actors, decisions, states, actions, transitions, interaction states, robustness requirements, copy, and a generation prompt.

Also creates a Figma/design tracker with one row per page and one row per sub-state.

Produces:

```text
docs/ux-ui/screens/[screen-name].md
docs/ux-ui/screens/page-state-design-links.csv
```

### `proto.prepare`

Creates a self-contained prototype build brief for visual generation tools. It summarizes the product, screens, flows, mock data, states, edge cases, and implementation boundaries.

Produces:

```text
docs/ux-ui/prepare-brief.md
```

### `proto.ui`

Compiles the canonical artifacts into UI-agent handoff files. These are designed to be handed to a UI generation agent or visual prototyping tool.

Produces:

```text
docs/ux-ui/ui-agent/README.md
docs/ux-ui/ui-agent/[screen-id]-[screen-name].md
```

### `proto.continuity`

Checks whether journeys, stories, flows, sitemap, screens, and UI-agent handoff agree with one another. Use it before generating visuals or after generation feedback.

Produces:

```text
docs/ux-ui/flow-continuity-review.md
```

### `proto.generate`

Prints one focused screen-generation prompt. It does not write files.

Produces:

```text
stdout prompt only
```

### `proto.change`

Ingests a change request and updates affected artifacts. It first performs impact analysis, lists the files to update, and waits for confirmation before writing.

Produces:

```text
targeted updates to affected docs/ux-ui files
```

### `proto.patterns`

Creates or updates a behavioral pattern library after screen generation or feedback. Use it to capture recurring interaction decisions and anti-patterns.

Produces:

```text
docs/ux-ui/patterns.md
```

### `proto.contracts`

Creates implementation-facing page contracts from the screen inventory and state model.

Produces:

```text
docs/ux-ui/screens/contracts.md
```

### `proto.data`

Creates data requirements for decisions, screens, shared objects, loading states, missing data behavior, and offline/degraded behavior.

Produces:

```text
docs/ux-ui/data/requirements.md
```

### `proto.actions`

Creates detailed action specifications. Each action gets intent, preconditions, permissions, validation, result, state transition, destination, feedback, undo, and analytics guidance.

Produces:

```text
docs/ux-ui/actions.md
```

### `proto.review`

Creates a readiness review across the prototype and engineering handoff artifacts. Use it before committing to implementation or a heavier visual design pass.

Produces:

```text
docs/ux-ui/readiness-review.md
```

### `proto.sprint`

Runs the prototype flow in five reviewable groups:

1. Foundation
2. User understanding
3. Structure
4. Design
5. Screens, handoff, and continuity

Produces the same core prototype artifacts as the command-by-command path, but with fewer pauses.

### `proto.oneshot`

Runs the full prototype artifact chain in one pass from a single input. Use it for the fastest route from idea or PRD to UI-generation-ready artifacts.

Produces:

```text
docs/ux-ui/brief.md
docs/ux-ui/actors/*
docs/ux-ui/journeys/*
docs/ux-ui/stories/*
docs/ux-ui/app-outline.md
docs/ux-ui/flows/*
docs/ux-ui/data/states.md
docs/ux-ui/design.md
docs/ux-ui/screens/*
docs/ux-ui/prepare-brief.md
docs/ux-ui/ui-agent/*
docs/ux-ui/flow-continuity-review.md
```

## Recommended Command Sequences

### Fastest

```text
proto.oneshot use prd.md
proto.continuity
proto.ui
```

### Workshop

```text
proto.sprint
proto.continuity
proto.generate [screen]
```

### Controlled

```text
proto.brief
proto.actors
proto.journeys
proto.stories
proto.outline
proto.flows
proto.states
proto.design
proto.map
proto.screens
proto.prepare
proto.ui
proto.continuity
```

### After Visual Feedback

```text
proto.change [feedback or requirement change]
proto.ui
proto.continuity
proto.review
```

### Engineering Handoff

```text
proto.contracts
proto.data
proto.actions
proto.review
```

## Practical Notes

- Existing artifacts are useful. The skill can read `docs/ux-ui/` and use it as context.
- `nothing` is valid input. The skill will infer from existing artifacts and mark assumptions.
- One-shot output is intentionally provisional. Review before treating it as authoritative.
- Keep journeys broad, but keep stories small.
- Run `proto.continuity` whenever screen flow, sitemap, or UI-generation output feels disconnected.
- Run `proto.change` for targeted updates instead of regenerating everything when the product direction changes.
