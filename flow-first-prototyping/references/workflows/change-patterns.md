# Change and Pattern Workflows

Detailed behavior for ingesting changes and maintaining the reusable pattern library.

---

### proto.change

**Output:** updates affected files in place — no new files created
**Usage:** `proto.change [description of change or new feature]`
**Reads:** all existing files in `./docs/ux-ui/`

Ingests a change description or new feature request, analyses which existing artifacts are affected, confirms the impact list with the user, then updates only the affected files in dependency order.

This command does not follow the standard step pattern. It has its own four-step process.

---

#### Step 1 — Accept the change description

The change description comes inline with the command:

```
proto.change add offline support for the mob movement screen
proto.change new actor: farm owner who reviews weekly reports
proto.change new non-human actor: sync worker that indexes files overnight
proto.change the source connection flow needs a QR code scan option
proto.change rename "paddock" to "block" throughout
```

If the user runs `proto.change` with no description, ask:
> What is changing? Describe the feature, fix, or addition — or paste a requirements document, ticket, or notes.

Wait for a response before proceeding.

---

#### Step 2 — Impact analysis

Read all files in `./docs/ux-ui/` and determine which artifacts are affected by the change. Reason through the dependency chain — a change to an actor may affect journeys, flows, and screens. A new flow may affect the sitemap, inventory, and screen files.

For each affected file, identify specifically what needs to change and why.

Print the impact analysis in this format — do not update any files yet:

```
─────────────────────────────────────────────
  proto.change impact analysis
─────────────────────────────────────────────
  Change: [description]

  Files to update:
  ✎ docs/ux-ui/[file]        [what changes and why]
  ✎ docs/ux-ui/[file]        [what changes and why]

  Files not affected:
  ✓ docs/ux-ui/[file]
  ✓ docs/ux-ui/[file]

  New files to create:
  + docs/ux-ui/[file]        [what it is]

─────────────────────────────────────────────
  [N] files to update, [N] to create

  Reply "yes" to proceed, adjust the list, or "cancel".
─────────────────────────────────────────────
```

Stop and wait for the user's response before writing anything.

---

#### Step 3 — Apply updates

If the user replies "yes" or "proceed", update files in dependency order:

1. Brief and value proposition (if affected)
2. Design (if affected)
3. Actors (if affected)
4. Journeys (if affected)
5. Flows (if affected)
6. States (if affected)
7. Screens — inventory, sitemap, then individual screen files (if affected)
8. Prepare brief (if affected)
9. UI-agent handoff package (only if it already exists, or if the user explicitly asks to update it)

If the user adjusts the list (removes or adds files), honour their changes before proceeding.

For each file updated, add a change log entry as the first line of the file, immediately after any existing provisional notice:

```
> 📝 Changed: [brief description of what changed] — proto.change "[original input]"
```

If a file already has change log entries, prepend the new one so the most recent is always first.

Do not regenerate files from scratch. Make targeted edits — preserve all existing content that is not affected by the change.

Print progress as each file is updated:

```
✎ docs/ux-ui/flows/aroha-moves-mob.md       updated — offline branch added
✎ docs/ux-ui/screens/mob-movement.md        updated — offline variant and queued state added
+ docs/ux-ui/screens/mob-movement-offline.md created
✓ docs/ux-ui/screens/sitemap.md             updated — new screen connection added
```

---

#### Step 4 — Summary and stop

After all updates are complete, print:

```
─────────────────────────────────────────────
  proto.change complete
─────────────────────────────────────────────
  [N] files updated, [N] files created

  Changed files:
  - docs/ux-ui/[file]
  - docs/ux-ui/[file]

  Run proto.generate [screen-name] to produce a
  generation prompt for any updated screens.
  Run proto.ui to rebuild the UI-agent handoff package.
  Run proto.review to check overall readiness.
─────────────────────────────────────────────
```

---

#### Edge cases

**Rename or terminology change** — if the change is a rename (e.g. "paddock" → "block"), perform a targeted find-and-replace across all affected files. List every file touched in the impact analysis. Confirm before executing — renames touch many files.

**Conflicting changes** — if the requested change contradicts something in an existing artifact, flag the conflict in the impact analysis rather than silently overwriting. Example: "This change adds an offline queue state to mob-movement, but docs/ux-ui/data/states.md currently defines mob-movement as having no offline states. Updating states.md will change the allowed actions table — confirm this is intended."

**New actor** — if the change adds a human actor, run the full human actor generation flow unless the user asks for light actors. If the change adds a system, service, integration, model, scheduled worker, or automation, use the non-human actor template. Then identify which existing flows and screens the new actor participates in or affects and update those.

**New screen** — if the change requires a new screen, add it to the inventory, update the sitemap, and generate the new screen file. Do not generate a screen spec for screens that are out of scope unless the change explicitly brings them into scope.

**Change affects the prepare brief** — always check whether mock data, the core flow, or the screen list in prepare-brief.md needs updating. This is easy to miss but important for generation quality.

**Change affects the UI-agent handoff** — if `docs/ux-ui/ui-agent/` exists, flag that it must be regenerated or updated after changes to design, screens, page-state links, sitemap, mock data, build brief, or prepare brief. Prefer rerunning `proto.ui` over hand-editing UI-agent files, because they are compiled from canonical artifacts.

**Change introduces a new interaction pattern** — if the change adds a new interaction type, flag in the impact analysis whether patterns.md exists and whether it needs a new entry. Do not create patterns.md if it doesn't exist — suggest the user run proto.patterns instead.

---

---

### proto.patterns

**Output:** `./docs/ux-ui/patterns.md`
**Reads:** `docs/ux-ui/design.md`, `docs/ux-ui/screens/*.md`, user input
**Optional:** yes — skippable. Run after generating screens when you have real feedback, not speculatively upfront.

`docs/ux-ui/patterns.md` is a behavioural pattern library — named, reusable design decisions and constraints that apply across the product. It is not a component catalogue. It describes intent and constraints, not implementation. Generation tools use it to make consistent decisions across screens.

**When to run:**
- After generating the first few screens, when you can see what worked and what did not
- When a recurring interaction has been decided and should be applied consistently
- When proto.change flags a new interaction type that needs a pattern defining
- Not before generating screens — patterns written speculatively before seeing real output tend to be generic

**Three modes:**

**Mode 1 — Start from scratch** (default when no patterns.md exists)
Ask: Do you have generation feedback, screen outputs, or interaction decisions to capture? Paste them, or say "nothing" to create an empty patterns file with instructions for when to return.
If feedback provided: extract patterns from it.
If "nothing": create a minimal patterns.md with structure in place and a note to return after first screens.

**Mode 2 — Add a pattern**
Usage: `proto.patterns add [description]`
Adds one new entry to patterns.md. Prompts for: name, when to use, when not to use, what it must achieve, anti-pattern statement.

**Mode 3 — Review and refine**
Usage: `proto.patterns review`
Reads patterns.md and all screen specs. Checks for: patterns no longer reflected in screen specs, recurring screen spec decisions not yet captured as patterns, contextual in-flow actions that should be standardized, contradictions between patterns. Produces a short review with suggestions.

**Required fields per pattern:**
- Pattern name
- What it is — one sentence
- When to use — specific conditions
- When not to use — explicit exclusions
- What it must achieve — the behavioural outcome
- Anti-pattern — what to avoid and why

For contextual-action patterns, always define what context must be preserved when the action completes: selection, cursor, scroll position, draft text, focused item, route, playback position, or object state.

**Template:**
```markdown
# Pattern Library

> File: docs/ux-ui/patterns.md
> Behavioural patterns — intent and constraints, not implementation.
> Grows from real generation feedback. Add patterns when you see recurring decisions, not speculatively.

## Patterns

### [Pattern name]
**What it is:** [One sentence]
**When to use:** [Specific conditions]
**When not to use:** [Explicit exclusions]
**Must achieve:** [Behavioural outcome — what the user must be able to do or understand]
**Anti-pattern:** [What to avoid and why]

---

[Repeat for each pattern]

## Anti-patterns

Things this product must never do, regardless of context.

- [Anti-pattern]: [Why]

## Open questions

Recurring decisions not yet resolved into a pattern.

- [Decision]: [What is unresolved and why it matters]
```

---
