---
name: flow-first-prototyping
description: Build flow-first rapid prototype artifacts with proto.* commands into ./docs/ux-ui, including actors, journeys, stories, app outline, flows, states, design system context, screen specs, prototype handoff briefs, UI-agent rendering contracts, flow-continuity checks, and readiness reviews. Use when the user asks to create, update, review, or run behavior-driven UX/UI prototyping workflows.
---

# Flow-First Prototyping

A command-driven skill for building rapid prototype artifacts from actors, journeys, stories, app shape, flows, states, and screen behavior. All outputs are written under `./docs/ux-ui/` in the current working directory.

This file is the routing guide. Detailed templates live in `references/` and should be loaded only for the command being run.

## Core Rules

- Use `./docs/ux-ui/` as the canonical output root unless the user explicitly overrides it for the run.
- Use the `proto.*` command namespace only. Do not emit or revive older `spec.*` command names.
- For standard artifact commands, ask the input question first, validate existing context, write the requested output, list assumptions, ask about gaps, then stop.
- If the user provides input inline with the command, treat it as the answer and proceed directly to validation.
- `nothing` is valid input. Draft from existing `docs/ux-ui/` artifacts and mark inferences as assumptions.
- Do not continue to the next command automatically unless the invoked command is explicitly a shortcut workflow.

## Command Behavior

| Behavior | Commands | Rule |
|---|---|---|
| Standard artifact command | `brief`, `value`, `actors`, `journeys`, `stories`, `outline`, `flows`, `states`, `design`, `map`, `screens`, `prepare`, `contracts`, `data`, `actions`, `patterns`, `review` | Ask for input first, output, then stop. |
| Immediate inspection | `status` | Do not ask for input; scan `docs/ux-ui/` and report progress. |
| Compiled handoff | `ui` | Do not ask for input; rebuild `docs/ux-ui/ui-agent/` from canonical artifacts. |
| Focused review | `continuity` | Do not ask for input; check generated flow and transition continuity, write the review, then stop. |
| Prompt-only output | `generate` | Print one screen-generation prompt; write no files. |
| Change workflow | `change` | Use the change process in `references/workflows/change-patterns.md`. |
| Shortcut workflow | `sprint`, `oneshot` | Follow `references/workflows/shortcuts.md`; these intentionally group commands. |

## Screen Quality Rules

Use these rules especially for `proto.screens`, `proto.ui`, and `proto.review`:

- Product-specific direction wins. Do not override explicit palette, typography, platform, CTA, or tone rules with generic preferences.
- Capture the physical context of use when it affects the screen: who is using it, where, under what constraints, and in what state of mind.
- Specify realistic data ranges: zero, typical, maximum, long text, missing data, and permission-restricted data.
- Every consequential action needs defined states: default, focus, pressed/active, disabled, loading, success feedback, error feedback, and recovery.
- Every action that moves the user between screens or states needs a source, trigger, destination, resulting state, back/exit behavior, and blocked/error path.
- If a secondary intent naturally arises from the object the user is currently touching, reading, writing, selecting, or editing, consider an in-flow contextual action before sending the user to a separate post-task screen.
- Copy must be exact where it affects UI generation: primary actions, empty states, errors, confirmations, destructive actions, offline messages, labels, and hints.
- Prefer fewer visible decisions. If a screen presents more than four simultaneous choices at one decision point, group them, sequence them, or mark it as a cognitive-load gap.
- Harden for production-shaped reality: long names, text expansion, offline/degraded states, duplicate taps, slow loading, partial data, unavailable permissions, touch targets, focus visibility, and responsive safe areas.

## Artifact Detail Boundaries

| Level | Right detail | Avoid |
|---|---|---|
| Journeys | Real-world context, mood shift, stakes, before/after app use | Button sequences, exact UI mechanics |
| Stories | One prototype-sized task slice: one actor, one trigger, one primary user-visible outcome, usually one screen or one adjacent screen transition, acceptance criteria, edge cases | Epic-sized chains, multi-intent titles with "and/then/through", full flow steps, rewriting the whole journey |
| App outline | Rough surfaces, navigation hypothesis, what should not become screens | Final screen inventory, components |
| Flows | Exact product sequence, branches, errors, exit states | Re-explaining actor motivation |
| States | Object lifecycle, allowed/blocked/hidden actions | Copywriting, layout, visual design |

## In-Flow Intent Rule

Some important product actions emerge inside another task, not after it. If a user sees, selects, edits, writes, hears, drags, reviews, or otherwise focuses on an object and may want to act on that object, test whether the action belongs in-flow.

Prefer an in-flow contextual action when:
- the user already has the target object in focus
- delaying the action would make the user remember or re-find the object
- the secondary action is lightweight, optional, and reversible
- the user should return to the same flow, cursor position, scroll position, or selected object afterward

Prefer a separate screen or post-flow step when:
- the secondary action needs extended decision-making, review, permissions, or structured data
- the action changes the primary task's outcome
- the action is rare, destructive, or should not be available during focused work

For writing, reading, review, media, maps, lists, and editing surfaces, always scan for contextual capture, annotate, save, bookmark, tag, quote, clip, attach, or reuse actions that may be better handled inline.

## Story Sizing Rules

Stories must be small enough to become one primary flow and one focused screen-generation concern. A good story has one human or non-human actor, one trigger, one primary user-visible outcome, and usually one primary screen or one adjacent screen transition. Split a candidate when the title or task slice contains "and", "then", "through", or a chain such as "browse and start", "connect and index", "authorize and choose folder", or "discover and add".

Use this split test before writing stories:
- If the task requires more than one primary decision, split it.
- If the task naturally crosses more than two screens, split it unless the second screen is only confirmation or feedback.
- If acceptance criteria cover browsing, selecting, confirming, and starting playback, split those into separate stories.
- If setup covers choosing a source, validating/authorizing, selecting a folder, indexing, and reviewing results, split those into separate stories.
- Keep discovery/import separate from listening-library curation: "discover indexed audiobooks", "review discovered books", and "add a discovered book to the listening library" are separate stories unless the product explicitly treats every indexed book as already added.

Journeys may remain broad end-to-end arcs. Stories should be the smaller task slices extracted from journey stages; do not collapse all stages of a journey into one story.

## Output Structure

`prepare-brief.md` is the canonical prototype build brief. `build-brief.md` may be read as an optional legacy or alternate input when present, but it is not the normal output of this skill.

```
./docs/ux-ui/
  brief.md
  value-proposition.md
  design.md
  app-outline.md
  actions.md
  prepare-brief.md
  flow-continuity-review.md
  readiness-review.md
  patterns.md                  optional, after first screens or generation feedback

  /ui-agent/                   compiled UI generation handoff
    README.md
    [screen-id]-[screen-name].md

  /actors/
    [actor-name].md
    permissions.md

  /journeys/
    overview.md
    journey-map.xlsx             Review-friendly companion workbook generated from journeys
    [actor]-[scenario].md

  /stories/
    overview.md
    [actor]-[story].md

  /flows/
    [actor]-[scenario].md

  /screens/
    inventory.md
    sitemap.md
    contracts.md
    page-state-design-links.csv
    [screen-name].md

  /data/
    requirements.md
    states.md
```

## Actor Naming

Actors are any participant that can initiate actions, receive information, make decisions, or materially affect a flow. Human actors use human-centred names and context. Non-human actors, such as systems, services, agents, scheduled jobs, external providers, devices, or automation, use operational names and a separate template.

Human actors use alliterative names: a first name and role descriptor sharing the same starting letter, such as `Andy the App User`, `Rachel the Receptionist`, or `Sam the Supervisor`. The file name is the slugified actor name.

Non-human actors use clear operational names, such as `Sync Worker`, `Provider API`, `Recommendation Agent`, `Payment Gateway`, or `Device Sensor`. Do not anthropomorphise non-human actors unless the product explicitly presents them as an assistant or agent in the UI.

## Commands

| Command | Output | Load details from |
|---|---|---|
| `proto.help` | stdout | this file |
| `proto.status` | stdout | this file |
| `proto.brief` | `docs/ux-ui/brief.md` | `references/templates/foundation.md` |
| `proto.value` | `docs/ux-ui/value-proposition.md` | `references/templates/foundation.md` |
| `proto.design` | `docs/ux-ui/design.md` | `references/templates/foundation.md` |
| `proto.actors` | `docs/ux-ui/actors/*.md`, `permissions.md` | `references/templates/actors.md` |
| `proto.journeys` | `docs/ux-ui/journeys/*.md`, `journey-map.xlsx` | `references/templates/journeys-flows-states.md` |
| `proto.stories` | `docs/ux-ui/stories/*.md` | `references/templates/journeys-flows-states.md` |
| `proto.outline` | `docs/ux-ui/app-outline.md` | `references/templates/journeys-flows-states.md` |
| `proto.flows` | `docs/ux-ui/flows/*.md` | `references/templates/journeys-flows-states.md` |
| `proto.states` | `docs/ux-ui/data/states.md` | `references/templates/journeys-flows-states.md` |
| `proto.map` | `docs/ux-ui/screens/inventory.md`, `sitemap.md` | `references/templates/screens-ui.md` |
| `proto.screens` | `docs/ux-ui/screens/*.md`, `page-state-design-links.csv` | `references/templates/screens-ui.md` |
| `proto.prepare` | `docs/ux-ui/prepare-brief.md` | `references/templates/screens-ui.md` |
| `proto.ui` | `docs/ux-ui/ui-agent/*` | `references/templates/screens-ui.md` |
| `proto.continuity` | `docs/ux-ui/flow-continuity-review.md` | `references/templates/screens-ui.md` |
| `proto.generate` | stdout only | `references/templates/screens-ui.md` |
| `proto.change` | updates affected files | `references/workflows/change-patterns.md` |
| `proto.patterns` | `docs/ux-ui/patterns.md` | `references/workflows/change-patterns.md` |
| `proto.contracts` | `docs/ux-ui/screens/contracts.md` | `references/templates/engineering-handoff.md` |
| `proto.data` | `docs/ux-ui/data/requirements.md` | `references/templates/engineering-handoff.md` |
| `proto.actions` | `docs/ux-ui/actions.md` | `references/templates/engineering-handoff.md` |
| `proto.review` | `docs/ux-ui/readiness-review.md` | `references/templates/engineering-handoff.md` |
| `proto.sprint` | grouped prototype files | `references/workflows/shortcuts.md` |
| `proto.oneshot` | full prototype artifact chain | `references/workflows/shortcuts.md` |

When loading a reference file, use the heading for the invoked command, for example `### proto.screens`. Do not load unrelated reference files unless the command's reference explicitly requires it.

## Recommended Flows

Prototype path:
`proto.brief -> proto.actors -> proto.journeys -> proto.stories -> proto.outline -> proto.flows -> proto.states -> proto.design -> proto.map -> proto.screens -> proto.prepare -> proto.ui -> proto.continuity`

Engineering handoff after prototype validation:
`proto.contracts -> proto.data -> proto.actions -> proto.review`

Optional additions:
- `proto.value` can be added after `brief` for stakeholder alignment.
- `proto.patterns` should be added after first screens or UI generation feedback, not speculatively.
- `proto.generate` can be used after `screens` for a single screen prompt.
- `proto.continuity` can be rerun after `proto.ui`, after a UI generation pass, or after `proto.change` to catch broken transitions before broader readiness review.

## Standard Step Pattern

For standard artifact commands:

1. Ask the command's input question and wait unless inline input was provided.
2. Validate relevant existing files and note missing inputs.
3. Draft or update the artifact using the command template.
4. Add an assumptions section when inference was required.
5. Ask concise questions about meaningful gaps.
6. Write the output, then stop with: `Step complete. Review the output, then reply with corrections or the next proto.* command.`

## Help Command

For `proto.help`, print the command table, recommended flows, behavior matrix, and output root from this file. No file reading is required.

## Status Command

For `proto.status`, scan `./docs/ux-ui/` immediately and report grouped progress:

- Foundation: `brief.md`, `value-proposition.md`, `design.md`
- Actors: files under `actors/`, plus `permissions.md`
- Journeys: `journeys/overview.md`, `journeys/journey-map.xlsx`, plus journey files
- Stories: `stories/overview.md`, plus story files
- App outline: `app-outline.md`
- Flows: flow files
- States: `data/states.md`
- Screens: `screens/inventory.md`, `screens/sitemap.md`, screen files, `page-state-design-links.csv`
- Prototype handoff: `prepare-brief.md`, `ui-agent/README.md`, UI-agent screen files
- Quality reviews: `flow-continuity-review.md`, `readiness-review.md`
- Engineering handoff: `screens/contracts.md`, `data/requirements.md`, `actions.md`
- Optional: `patterns.md`

Show done/missing status, a done count, and the next recommended command. If `./docs/ux-ui/` does not exist, print: `No docs/ux-ui folder found. Run proto.brief to start.`

## Design and Pattern Ownership

`design.md` owns upfront cross-screen UI decisions: platform, visual language, action hierarchy, navigation, state treatment, copy rules, accessibility, and global constraints.

`patterns.md` owns reusable decisions learned after screens or generation feedback. It captures recurring interaction patterns and anti-patterns. It is not a component catalogue and should not duplicate the base design system.

## AGENTS.md Snippet

```md
# Agents

Use the skill at ~/.codex/skills/flow-first-prototyping/SKILL.md

All proto.* commands are available. Read from and write to ./docs/ux-ui/
```
