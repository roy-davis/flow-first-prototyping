# Shortcut Workflows

Detailed behavior for the condensed sprint and one-shot prototype flows.

---

### proto.sprint

**Output:** All files from the 5-step condensed prototype flow
**Runs:** proto.brief + proto.actors → proto.journeys + proto.stories + proto.outline → proto.flows + proto.states → proto.design → proto.map + proto.screens + proto.prepare + proto.ui + proto.continuity

proto.sprint groups the 12 prototype commands into 5 steps. Each step asks for input once, runs its grouped commands, outputs all files for that step, then pauses for review before continuing. The standard checkpoint pattern applies within each step — validate, draft or complete, list assumptions, ask about gaps — but runs across all commands in the group before pausing.

When running grouped commands within a step:
- Ask for input once at the start of the step, not once per command
- If the input clearly covers one command but not another, draft the uncovered command from context and mark it provisional
- Output all files for the step, then list all assumptions across the group together
- Ask only the most important gap questions across the group — not one round per command
- End each step (except the last) with the standard stop phrase plus the next step preview

**Step 1 — Foundation**
Runs: proto.brief + proto.actors (full depth for human actors; non-human template for systems/agents)
Input question: Do you have a product brief, PRD, or idea to share? Paste it, give a file path, or say "nothing."
Outputs: `docs/ux-ui/brief.md`, `docs/ux-ui/actors/[name].md`, `docs/ux-ui/actors/permissions.md`
Stop phrase: "Step 1 complete. Reply with corrections or 'accept' to continue to Step 2 — journeys, stories, and app outline."

**Step 2 — User understanding**
Runs: proto.journeys + proto.stories + proto.outline
Input question: Do you have existing journey maps, user stories, scenario notes, rough app structure, navigation, or screen-shape notes? Share a file path, paste content, or say "nothing."
Outputs: `docs/ux-ui/journeys/overview.md`, `docs/ux-ui/journeys/[actor]-[scenario].md` (one per journey), `docs/ux-ui/journeys/journey-map.xlsx`, `docs/ux-ui/stories/overview.md`, `docs/ux-ui/stories/[actor]-[story].md` (one per story), `docs/ux-ui/app-outline.md`
Note: After writing story files, update journeys/overview.md with story references. Generate app-outline.md as the early structure sanity check before flow and screen inventory work.
Stop phrase: "Step 2 complete. Review the app outline carefully, then reply with corrections or 'accept' to continue to Step 3 — flows and states."

**Step 3 — Structure**
Runs: proto.flows + proto.states
Input question: Do you have existing flow documentation, state model, workflow documentation, or changes from the app-outline review? Share a file path, paste content, or say "nothing."
Outputs: `docs/ux-ui/flows/[actor]-[scenario].md` (one per flow), `docs/ux-ui/data/states.md`
Note: After writing flow files, update stories/overview.md with flow references as per the standard proto.flows rule.
Stop phrase: "Step 3 complete. Reply with corrections or 'accept' to continue to Step 4 — design system."

**Step 4 — Design**
Runs: proto.design
Input question: Do you have an existing design system, design.md, or component library to reference? Share a file path, paste content, or say "nothing."
Outputs: `docs/ux-ui/design.md`
Stop phrase: "Step 4 complete. Reply with corrections or 'accept' to continue to Step 5 — screens, prepare brief, and UI-agent handoff."

**Step 5 — Screens, handoff, and continuity**
Runs: proto.map + proto.screens + proto.prepare + proto.ui + proto.continuity
Input question: Do you have an existing screen list, screen specs, or prototype brief? Share a file path, paste content, or say "nothing." Also: which tool are you generating for — v0, Lovable, Bolt, Claude Design, Google Stitch, or other?
Outputs: `docs/ux-ui/screens/inventory.md`, `docs/ux-ui/screens/sitemap.md`, `docs/ux-ui/screens/[screen-name].md` (one per screen), `docs/ux-ui/screens/page-state-design-links.csv`, `docs/ux-ui/prepare-brief.md`, `docs/ux-ui/ui-agent/README.md`, `docs/ux-ui/ui-agent/[screen-id]-[screen-name].md`, and `docs/ux-ui/flow-continuity-review.md`
Stop phrase: "Sprint complete. Your prototype spec is ready in ./docs/ux-ui/. Use ./docs/ux-ui/ui-agent/ for UI generation. If generated screens feel disconnected, rerun proto.continuity with the feedback, then use proto.change to apply fixes."

---

### proto.oneshot

**Output:** All prototype artifact files in one pass
**Reads:** Single input provided inline or at the start

proto.oneshot takes one input — a product idea, PRD, notes, or file — and generates the complete prototype artifact chain without pausing. It makes all assumptions, marks every output as provisional, and collects all clarification questions at the end.

**Behaviour rules:**
- Ask for input once at the very start. Do not pause again until all artifacts are written.
- Use full human actors (not light mode) and non-human actor templates where relevant — a one-shot run needs maximum context for screen generation.
- Mark every output file with the provisional notice (the standard Step 6 rule applies to all files).
- Generate artifacts in the correct dependency order: brief → actors → journeys → stories → app outline → flows → states → design → map → screens → prepare → UI-agent handoff → flow-continuity review.
- Apply the Story Sizing Rules when generating stories and flows. Prefer multiple small story files per journey over one epic-sized story. Do not collapse journey stages into a single story when stages imply separate decisions, screens, or outcomes.
- After all files are written, print a consolidated list of all assumptions grouped by artifact, followed by all clarification questions grouped by artifact.
- The clarification questions section should be actionable — each question names the artifact and field, explains why it matters, and suggests a default if the user wants to accept without answering.

**Input question (asked once):**
> Share your product idea, PRD, or notes — paste content directly, give a file path, or give me a URL. Also tell me which tool you're generating for (v0, Lovable, Bolt, Claude Design, Google Stitch, or other) and whether you have an existing design system to reference. If you have nothing on design, I'll draft defaults.

**Output order:**
1. `docs/ux-ui/brief.md`
2. `docs/ux-ui/actors/[name].md` (one per actor) + `docs/ux-ui/actors/permissions.md`
3. `docs/ux-ui/journeys/overview.md` + `docs/ux-ui/journeys/[actor]-[scenario].md` (one per journey) + `docs/ux-ui/journeys/journey-map.xlsx`
4. `docs/ux-ui/stories/overview.md` + `docs/ux-ui/stories/[actor]-[story].md` (one per story) — update journeys/overview.md with story references
5. `docs/ux-ui/app-outline.md`
6. `docs/ux-ui/flows/[actor]-[scenario].md` (one per flow) — update stories/overview.md with flow references
7. `docs/ux-ui/data/states.md`
8. `docs/ux-ui/design.md`
9. `docs/ux-ui/screens/inventory.md` + `docs/ux-ui/screens/sitemap.md`
10. `docs/ux-ui/screens/[screen-name].md` (one per screen)
11. `docs/ux-ui/screens/page-state-design-links.csv`
12. `docs/ux-ui/prepare-brief.md`
13. `docs/ux-ui/ui-agent/README.md` + `docs/ux-ui/ui-agent/[screen-id]-[screen-name].md`
14. `docs/ux-ui/flow-continuity-review.md`

**End of output:**
Print a summary in this format:

```
─────────────────────────────────────────────
  proto.oneshot complete — prototype artifact chain written
─────────────────────────────────────────────

All outputs are provisional. Review before treating as authoritative.

Assumptions by artifact:
  brief.md — [list]
  actors/ — [list]
  app-outline.md — [list]
  stories/ — [list]
  ...

Clarification questions:
  1. [Artifact: field] — [question] — default if accepted: [default]
  2. ...

Run proto.status to see all files. Rerun proto.continuity after UI-generation feedback, then run proto.review for a readiness check.
─────────────────────────────────────────────
```

---
