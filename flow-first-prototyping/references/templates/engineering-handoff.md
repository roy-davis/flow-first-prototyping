# Engineering Handoff Commands

Detailed templates and behavior for page contracts, data requirements, action specifications, and readiness review.

---

### proto.contracts

**Output:** `./docs/ux-ui/screens/contracts.md`
**Reads:** `docs/ux-ui/data/states.md`, `docs/ux-ui/screens/inventory.md`, `docs/ux-ui/actors/`

Produce contracts only for in-scope screens. Actions must be consistent with allowed/blocked/hidden rules in the state model.

**Template:**
```markdown
# Page Contracts

> File: docs/ux-ui/screens/contracts.md

---

## [Screen name] — PG01

**Story:** [Story file] | **Flow:** [Flow file] | **Actor:** [Actor name] | **State:** [Name]

### Purpose
[One sentence]

### Current state displayed
- Object shown:
- Status:
- What happened:
- What is pending:
- What needs attention:

### Primary decision
- Decision:
- Options:
- Information required:
- Risk if wrong:
- Reversible: Yes / No

### Secondary decisions

| Decision | Options | Info required |
|---|---|---|

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
|---|---|---|---|---|---|
| | Primary | | | | |
| | Disabled | [condition] | — | — | — |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

### Edge cases

| Scenario | Behaviour |
|---|---|
| Missing data | |
| Permission denied | |
| Conflicting state | |
| Action fails | |
| Session expired | |
```

---

---

### proto.data

**Output:** `./docs/ux-ui/data/requirements.md`
**Reads:** `docs/ux-ui/screens/contracts.md`, `docs/ux-ui/screens/inventory.md`, `docs/ux-ui/data/states.md`

For missing-data behaviour, be specific. "Show error" is insufficient — state whether the action is blocked, the field is hidden, a placeholder is shown, or the section degrades.

**Template:**
```markdown
# Data Requirements

> File: docs/ux-ui/data/requirements.md

## Data-to-decision matrix

| Decision | Data required | Display | Source | If missing |
|---|---|---|---|---|

---

## Per-screen data

### [Screen] — PG01

| Field | Type | Source | Required | Display | If missing |
|---|---|---|---|---|---|

---

## Shared objects

### [Object]

| Field | Type | Nullable | Description |
|---|---|---|---|
| id | string | No | |
| status | enum | No | See states.md |

---

## Loading states

| Screen | Loading | Empty | Error | Partial |
|---|---|---|---|---|
| PG01 | Skeleton | Empty state | Error banner | |
```

---

---

### proto.actions

**Output:** `./docs/ux-ui/actions.md`
**Reads:** `docs/ux-ui/data/states.md`, `docs/ux-ui/screens/contracts.md`, `docs/ux-ui/actors/`

Produce one full spec per action. Do not collapse similar actions across pages.

**Action types:** Progression / Modification / Investigation / Recovery / Delegation / Exit

**Template:**
```markdown
# Action Specifications

> File: docs/ux-ui/actions.md

## Index

| ID | Action | Type | Page | Actor | Priority |
|---|---|---|---|---|---|
| A01 | | | | | |

---

## [Action] — A01

**Type:** | **Page:** [ID] | **Story:** [Story file] | **Flow:** [Flow file] | **Actor:** [Actor name] | **Priority:**

### Intent
[One sentence]

### Preconditions
-

### Permission rules
- Allowed for:
- Blocked for:
- Conditions:

### Validation

| Rule | Message | Behaviour |
|---|---|---|

### Confirmation
- Required: Yes / No
- Style: Modal / Popover / None
- Heading:
- Body:
- Confirm label:
- Cancel label:
- Destructive: Yes / No

### Result

### State transition
[Object] from [State] → [State]

### Destination

### Success feedback
- Style:
- Copy:

### Error feedback
- Style:
- Copy:
- Recovery:

### Undo
- Available: Yes / No
- Window:
- Trigger:

### Analytics
- Event:
- Properties:
```

---

---

### proto.review

**Output:** `./docs/ux-ui/readiness-review.md`
**Reads:** all files in `./docs/ux-ui/`

No external input needed. Read all files and run the checks below.

**Checks to run:**
- Traceability: for each in-scope screen verify `Screen → Component → Action → Decision → Data → Flow → Story → Journey → Actor → Product Goal`
- Flow continuity: if `docs/ux-ui/flow-continuity-review.md` exists, carry unresolved Critical and Important items into this review; if it does not exist and `ui-agent/` exists, flag that `proto.continuity` should be run before final prototype handoff
- In-flow intent fit: secondary capture, save, tag, annotate, bookmark, quote, clip, attach, or reuse actions appear at the moment/object of attention when delaying them would interrupt or degrade the primary flow
- App outline sanity: screen inventory explains any meaningful addition, removal, merge, or split from `docs/ux-ui/app-outline.md`
- Story granularity: each story is one prototype-sized task slice from a journey opportunity, not a full journey rewrite or a procedural flow
- Component coverage: every component in screen files exists in design.md
- Action coverage: every action in contracts.md has a spec in actions.md
- State coverage: every state in contracts.md is defined in data/states.md
- Data coverage: every field in screen files appears in data/requirements.md
- Scope consistency: every screen file in screens/ is marked in-scope in inventory.md
- Actor coverage: every story and flow references an actor file in `actors/`
- Screen robustness: every in-scope screen covers empty, typical, maximum, long text, loading, error, offline/degraded, permission, duplicate-action, responsive, and focus concerns where applicable
- Interaction-state coverage: every consequential action has default, focus, pressed/active, disabled, loading, success, error, and recovery treatment where applicable
- Copy specificity: primary actions, errors, empty states, confirmations, destructive actions, offline messages, labels, and hints use exact product copy rather than generic placeholders
- Copy boundary: directional guidance from context, content priority, anti-goals, robustness notes, layout regions, and acceptance criteria is not treated as visible UI copy, and CONTENT does not contain phrases lifted only from those guidance sections
- Cognitive-load check: each screen has one clear primary focus and no ungrouped decision point with more than four visible choices
- UI-agent readiness: if `docs/ux-ui/ui-agent/` exists, each screen contract includes states to render, anti-goals, data ranges, interaction states, responsive/hardening notes, copy requirements, mock data, and visual acceptance criteria
- Transition readiness: every in-scope screen has matching entry, forward, back/exit, blocked/error, and re-entry paths where relevant
- Context preservation: contextual actions preserve selection, cursor, scroll, draft, playback, focused item, route, or object state where relevant
- Cross-screen design decisions: `design.md` contains concrete reusable UI decisions for navigation, action hierarchy, focus/input, data freshness, loading, empty, error, offline/degraded states, status indicators, provider/source identity, data density, layout constraints, copy, and accessibility

**Score 1–5:** 1 = not started / 2 = major gaps / 3 = adequate / 4 = strong / 5 = complete / N/A = intentionally skipped

**Before scoring:** check which optional artifacts exist. Mark proto.states, proto.data, and proto.actions as N/A if they were intentionally skipped for rapid prototyping — do not score them as gaps. Only flag them as missing if the prototype cannot function without them.

**Dimensions:** product clarity, user clarity, actor usefulness, journey completeness, story completeness, app outline sanity, flow completeness, transition continuity, design system completeness, screen completeness, screen robustness, UI-agent readiness, prototype readiness.

**Engineering handoff dimensions (only score if those artifacts exist):** state coverage, decision clarity, data completeness, action completeness.

**Categorise issues:** Critical (blocks prototype build) / Important (affects quality or correctness) / Minor (polish or completeness).

**Template:**
```markdown
# Readiness Review

> File: docs/ux-ui/readiness-review.md

## Scores

| Dimension | Score | Notes |
|---|---|---|
| Product clarity | /5 | |
| User clarity | /5 | |
| Actor usefulness | /5 | |
| Journey completeness | /5 | |
| Story completeness | /5 | |
| App outline sanity | /5 | |
| Flow completeness | /5 | |
| Transition continuity | /5 | |
| Design system completeness | /5 | |
| Screen completeness | /5 | |
| Screen robustness | /5 | |
| UI-agent readiness | /5 or N/A | |
| **Prototype readiness** | /5 | |

**Engineering handoff dimensions (score N/A if artifacts were intentionally skipped)**

| Dimension | Score | Notes |
|---|---|---|
| State coverage | /5 or N/A | |
| Decision clarity | /5 or N/A | |
| Data completeness | /5 or N/A | |
| Action completeness | /5 or N/A | |

**Verdict:** Ready / Needs fixes / Not ready

## Traceability

| Screen | Complete | Break point |
|---|---|---|
| PG01 | ✓ | |

## Critical gaps
- [ ] [Gap] — [file] — fix: [action]

## Important issues
- [ ] [Issue] — [file]

## Robustness and generation risks
- [ ] [Risk] — [screen/file] — impact: [why the generated UI may fail]

## Minor issues
- [ ] [Issue]

## Missing components
- [Component] — used in [Screen] — not in docs/ux-ui/design.md

## Risky assumptions

| Assumption | File | Risk |
|---|---|---|

## Next actions
1.
2.

## Open questions
1.
```

---

---
