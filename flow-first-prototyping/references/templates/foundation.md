# Foundation Commands

Detailed templates and behavior for foundation artifacts. Load this file only for the command being run.

---

### proto.brief

**Output:** `./docs/ux-ui/brief.md`
**Reads:** user input

**Required fields:**
- Product name or working title
- Problem statement — what problem exists, for whom, and why it matters
- Product purpose — what the product does and for whom (two sentences max)
- Target users and actors — high level, not yet detailed actor files
- Business goal
- Success criteria
- Scope — in scope and explicitly out of scope
- Known constraints — technical, regulatory, timeline, budget, team
- Key assumptions — treated as true but not yet validated
- Open questions — unknown and could affect direction

**Template:**
```markdown
# Product Brief

## Product name
[Name or working title]

## Problem statement
[What problem, for whom, why it matters now]

## Product purpose
[What it does and for whom. Two sentences max.]

## Target users
[High level. Detailed actors come later.]

## Business goal
[What the business needs this to achieve]

## Success criteria
[How success is measured]

## Scope

### In scope

### Out of scope

## Known constraints

## Key assumptions

## Open questions
```

---

---

### proto.value

**Output:** `./docs/ux-ui/value-proposition.md`
**Reads:** `docs/ux-ui/brief.md`

**Required fields:**
- Value proposition — structured: for / who needs / the product is / that / unlike / our product
- Design principles — 3 to 6, each product-specific with a name and one-sentence meaning
- Non-goals

**Important:** Principles must be specific to this product. If a principle is generic ("be simple", "delight users"), reframe it as a specific commitment. For example, "be simple" on a finance product becomes "never show a number without context."

**Template:**
```markdown
# Value Proposition and Design Principles

## Value proposition

**For** [target user]
**Who needs** [need or job-to-be-done]
**The product is** [product name and category]
**That** [primary benefit]
**Unlike** [current alternative]
**Our product** [key differentiator]

## Design principles

### 1. [Principle name]
[What this means specifically for this product]

### 2. [Principle name]
[What this means specifically for this product]

### 3. [Principle name]
[What this means specifically for this product]

[Up to 6 total]

## Non-goals
[What this product should deliberately not try to do]
```

---

---

### proto.design

**Output:** `./docs/ux-ui/design.md`
**Reads:** `docs/ux-ui/app-outline.md`, `docs/ux-ui/stories/`, `docs/ux-ui/flows/`, `docs/ux-ui/brief.md`, user input (existing design file, tokens, style guide)

**When to run:** After proto.outline and proto.flows, not before. The app outline reveals the likely product shape; stories reveal what the prototype must prove; flows reveal what the screens need to do — whether this is a mobile-first field tool, a desktop dashboard, or a multi-step form — which should inform design decisions before committing to tokens and patterns.

**Two paths:**
- **Existing file provided:** validate against required fields, complete gaps only, preserve everything supplied
- **Nothing provided:** draft defaults based on product type and flow context. Present as a block for confirmation — do not ask field by field.

**Required fields (core — needed for screen generation):**
- Framework and target environment (React / Next.js / Vue / mobile / other)
- Component library name, version, and styling approach (CSS variables vs Tailwind)
- Dark mode support
- Optional machine-readable token summary — include only confirmed colors, typography, spacing, radius, and component tokens; do not invent values
- Visual tone — one sentence describing the intended feel (e.g. "clean and utilitarian for field use", "warm and approachable for consumers")
- Cross-screen UI decisions — reusable product rules for navigation, action hierarchy, contextual in-flow actions, state treatment, source/status language, data freshness, layout constraints, and copy conventions
- Navigation pattern and mobile behaviour
- Primary color, background, and surface tokens — enough for a generation tool to apply consistent colour
- Border radius and elevation style
- Interaction patterns — loading states, empty states, error states, success feedback, confirmation for destructive actions
- Tone and voice — label casing, button copy convention, error message tone
- Icon set and size scale
- Accessibility baseline — WCAG level and minimum contrast

**Extended fields (add when moving toward engineering handoff):**
- Full color token set with foreground variants
- Complete typography scale
- Full spacing system
- Complete breakpoint and layout definitions

**Do not include:** photography style, illustration style, or other brand-only fields not used by code generation tools.

**Template:**
```markdown
---
name:
description:
colors:
  primary:
  background:
  foreground:
  surface:
  muted:
  border:
  error:
typography:
  heading:
    fontFamily:
    fontSize:
    fontWeight:
    lineHeight:
  body:
    fontFamily:
    fontSize:
    fontWeight:
    lineHeight:
rounded:
  default:
spacing:
  base:
components:
  button-primary:
    backgroundColor:
    textColor:
    rounded:
    padding:
---

# Design System Context

> Referenced by all screen artifacts. Every component in screen specs must be named here.

If confirmed token values are unavailable, omit the frontmatter rather than filling it with guesses. The markdown body remains required.

## Framework
- Framework:
- Component library:
- Library version:
- Documentation URL:
- Styling: (CSS variables / Tailwind / other)
- Dark mode: (yes / no / system)
- Custom component overrides:

## Visual tone
[One sentence. What this product should feel like — e.g. "Clean and utilitarian for field workers who need fast, glanceable information" or "Warm and approachable, built for people who distrust software".]

## Cross-screen UI decisions

These are product-specific decisions every screen inherits unless a screen spec explicitly overrides them. Keep them concrete enough for a UI agent to apply consistently.

| Area | Decision | Applies to |
|---|---|---|
| Navigation model | [How users move between top-level and detail screens; back behaviour; no-go navigation patterns] | All screens |
| Primary action hierarchy | [How primary, secondary, tertiary, destructive, and disabled actions look and where they appear] | All actions |
| Contextual in-flow actions | [When secondary actions appear at the object of attention; how they preserve selection, cursor, scroll, draft, playback, or focused state; when they must remain separate] | Writing, reading, editing, review, media, map, list, and detail surfaces |
| Focus and input | [Keyboard/remote/touch/focus model, default focus, visible focus treatment, touch target minimums] | All interactive elements |
| Data freshness | [What is cached vs real-time; whether stale/cached content remains visible; how freshness is labelled] | Data-backed screens |
| Loading states | [Skeleton/spinner/progress approach; when loading blocks vs preserves content] | Async screens/actions |
| Empty states | [Structure, tone, CTA pattern, and what not to show] | Empty variants |
| Error and recovery | [How errors are named, where recovery actions appear, and how much detail is exposed] | Error variants |
| Offline/degraded states | [How offline, degraded, partial, or unavailable conditions appear] | Source/network-dependent screens |
| Status indicators | [Meaning of badges, pills, colors, icons, progress, warnings, and success states] | Status-heavy screens |
| Provider/source identity | [How external sources, integrations, systems, or agents are named and visually represented] | Setup, sync, repair, playback |
| Data density | [Typical and maximum list/grid density, truncation/wrapping, progressive disclosure] | Lists, grids, details |
| Responsive/layout constraints | [Safe areas, breakpoints, viewport-specific layout rules, no-go layouts] | All screens |
| Copy conventions | [Casing, button label pattern, error tone, destructive copy, forbidden generic copy] | All copy |
| Accessibility baseline | [Contrast, focus, reduced motion, keyboard/remote expectations, screen reader expectations] | All screens |

## Color tokens

| Token | Light | Dark | Usage |
|---|---|---|---|
| primary | | | Main actions, links |
| primary-foreground | | | Text on primary |
| secondary | | | Secondary actions |
| secondary-foreground | | | |
| background | | | Page background |
| foreground | | | Default text |
| card | | | Card backgrounds |
| card-foreground | | | |
| muted | | | Subtle backgrounds |
| muted-foreground | | | Placeholder text |
| border | | | Default borders |
| error | | | Error states |
| error-foreground | | | |
| success | | | |
| success-foreground | | | |
| warning | | | |
| warning-foreground | | | |
| info | | | |
| info-foreground | | | |

## Typography

| Role | Family | Size | Weight | Line height |
|---|---|---|---|---|
| Heading 1 | | | | |
| Heading 2 | | | | |
| Heading 3 | | | | |
| Body | | | | |
| Body small | | | | |
| Label | | | | |
| Caption | | | | |
| Code | | | | |

## Spacing
- Base unit:
- Scale:
- Component padding:
- Section gap:

## Layout
- Grid:
- Breakpoints:
- Container max width:
- Page padding mobile:
- Page padding desktop:

## Shape
- Border radius default:
- Border radius scale:
- Elevation style:

## Navigation
- Pattern:
- Sidebar width:
- Mobile navigation:
- Active state style:

## Interaction patterns

### Loading
- Approach: (skeleton / spinner / both)
- Button loading:

### Empty states
- Structure:
- Tone:

### Error states
- Inline field:
- Form level:
- Page level:

### Success feedback
- Style:
- Toast duration:

### Modals
- Sizes:
- Overlay:
- Dismiss on overlay click:

### Toasts
- Position:
- Duration:

### Confirmation (destructive)
- Style:
- Require typing:

## Tone and voice
- Label casing:
- Button copy:
- Error tone:
- Help text:

## Icons
- Set:
- Sizes:
- Stroke weight:

## Accessibility
- WCAG level:
- Text contrast:
- UI contrast:
- Focus style:
- Reduced motion:

## Notes
```

---
