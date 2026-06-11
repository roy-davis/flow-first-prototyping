# Actor Commands

Detailed templates and behavior for human and non-human actors. Load for `proto.actors`.

---

### proto.actors

**Output:** one file per actor at `./docs/ux-ui/actors/[actor-name].md` plus `./docs/ux-ui/actors/permissions.md`
**Reads:** `docs/ux-ui/brief.md`, `docs/ux-ui/value-proposition.md`

**Actor types:**
- **Human actor:** A person using, approving, configuring, operating, or affected by the product. Use the human actor template below.
- **Non-human actor:** A system, service, API, device, automation, model, agent, scheduled worker, integration, or external platform that participates in a flow. Use the non-human actor template below.

**Human actor naming:**
Generate an alliterative name automatically from the role. The name combines a first name and a role descriptor that share the same starting letter. The name must feel natural in conversation — "what does Andy need here?" should be easy to say. File name is slugified from the actor name: `andy-the-app-user.md`.

**Non-human actor naming:**
Use a clear operational name, not a human name. Examples: `Sync Worker`, `Provider API`, `Recommendation Agent`, `Payment Gateway`, `Device Sensor`. File name is slugified from the operational name: `sync-worker.md`.

**Required fields per human actor:**
- Composite summary — one short paragraph written as a character sketch
- Identity — actor type, actor group, access level, scope, archetype name, example role titles
- Context of use — primary device, secondary device, connectivity, physical environment, environmental constraints
- Technical profile — technical literacy, software familiarity, data entry comfort, map/spatial comfort, tolerance for complexity
- Time and attention — typical work hours, peak usage times, session duration, interruption frequency, time pressure, attention availability
- Decision authority — strategic, operational, financial, delegation patterns, approval dependencies
- Workday shape — morning, midday, afternoon, evening, seasonal variation
- Goals — primary job goal, secondary goals, success criteria, quality signals
- Frustrations — current pain points, legacy system complaints, workflow friction, information gaps
- Constraints for flow design — each constraint mapped to its design implication
- Jobs this actor performs — job ID, job statement, frequency, notes
- Scenarios involving this actor — scenario ID, name, role

Human actors are operational, not demographic profiles. Every attribute must have a direct implication for design or flow decisions.

**Required fields per non-human actor:**
- Operational summary — what it does and why it matters to the product
- Identity — actor type, owner, boundary, environment, trust level
- Responsibilities — inputs, processing, outputs, timing/frequency
- Capabilities — actions it can perform, decisions it can make, decisions it cannot make
- Data ownership — data read, data written, data retained, data exposed to users
- Triggers — events, schedules, requests, webhooks, or user actions that invoke it
- States — available, degraded, unavailable, pending, blocked, or product-specific states
- Failure modes — what can go wrong and how the product/user experiences it
- Constraints for flow design — latency, reliability, permissions, rate limits, privacy, observability
- Jobs this actor performs — job ID, job statement, frequency, notes
- Scenarios involving this actor — scenario ID, name, role

**Two human actor depths:**

**Light human actor** — use for rapid prototyping or early-stage ideas. Six fields only:
- Archetype name (alliterative)
- Role and access level
- Primary device and connectivity
- Primary job — what they are trying to accomplish
- Key constraint — the single biggest thing that limits how they use the product
- What they distrust — what would make them abandon or ignore the product

Generate a light human actor when the user says "quick", "fast", "draft", or when proto.brief indicates early-stage exploration. Ask: "Do you want light human actors (6 fields, fast), full human actors (all sections), or mixed actors including systems/agents?"

**Full human actor** — use when the product concept is established and the actors will drive flow and screen decisions across multiple sessions.

**Template (full human actor):**
```markdown
# [Archetype name] — [Role]

> File: docs/ux-ui/actors/[archetype-name].md
> Actor type: Human

**Composite summary:** [One short paragraph. Who this person is, how they move through their day, and their relationship to the product. Written as a character sketch, not a demographic profile.]

## Identity

| Attribute | Value |
|---|---|
| Actor type | Human |
| Actor group | |
| Access level | |
| Scope | |
| Archetype name | [e.g. Andy the App User] |
| Example role titles | |

## Context of Use

| Attribute | Value |
|---|---|
| Primary device | |
| Secondary device | |
| Typical connectivity | |
| Physical environment | |
| Environmental constraints | |

## Technical Profile

| Attribute | Value |
|---|---|
| Technical literacy | |
| Software familiarity | |
| Data entry comfort | |
| Map / spatial comfort | |
| Tolerance for complexity | |

## Time and Attention

| Attribute | Value |
|---|---|
| Typical work hours | |
| Peak usage times | |
| Session duration | |
| Interruption frequency | |
| Time pressure level | |
| Attention availability | |

## Decision Authority

| Attribute | Value |
|---|---|
| Strategic decisions | |
| Operational decisions | |
| Financial authority | |
| Delegation patterns | |
| Approval dependencies | |

## Workday Shape

| Period | Description |
|---|---|
| Morning | |
| Midday | |
| Afternoon | |
| Evening | |
| Seasonal variation | |

## Goals

| Goal type | Description |
|---|---|
| Primary job goal | |
| Secondary goals | |
| Success criteria | |
| Quality signals | |

## Frustrations

| Frustration type | Description |
|---|---|
| Current pain points | |
| Legacy system complaints | |
| Workflow friction | |
| Information gaps | |

## Constraints for Flow Design

| Constraint | Implication |
|---|---|
| Device constraint | |
| Connectivity constraint | |
| Time constraint | |
| Environment constraint | |
| Authority constraint | |
| Literacy constraint | |

## Jobs This Actor Performs

| Job ID | Job statement | Frequency | Notes |
|---|---|---|---|
| J-001 | | | |

## Scenarios Involving This Actor

| Scenario ID | Scenario name | Role in scenario |
|---|---|---|
| SC-01 | | |
```

**Template (light human actor — rapid prototyping):**
```markdown
# [Archetype name] — [Role]

> File: docs/ux-ui/actors/[archetype-name].md
> Actor type: Human
> Mode: Light human actor

**[Archetype name]** is [one sentence: who they are and what they spend their day doing].

| Attribute | Value |
|---|---|
| Role | |
| Access level | |
| Primary device | |
| Connectivity | |
| Primary job | [What they are trying to accomplish with this product] |
| Key constraint | [The single biggest thing limiting how they use the product] |
| What they distrust | [What would make them abandon or ignore the product] |
```

**Template (non-human actor):**
```markdown
# [Actor name] — [System / service / agent / integration role]

> File: docs/ux-ui/actors/[actor-name].md
> Actor type: Non-human

**Operational summary:** [One short paragraph. What this actor does, what product outcome it affects, and how users experience its behaviour.]

## Identity

| Attribute | Value |
|---|---|
| Actor type | Non-human |
| Actor category | System / service / API / device / automation / agent / model / integration |
| Owner | Product / customer / third party / external platform |
| Boundary | Internal / external / hybrid |
| Environment | Client / server / cloud / device / external |
| Trust level | Trusted / partially trusted / untrusted external |

## Responsibilities

| Responsibility | Detail |
|---|---|
| Inputs | |
| Processing | |
| Outputs | |
| Timing / frequency | |
| User-visible effect | |

## Capabilities

| Capability | Allowed decision/action | Cannot decide/do |
|---|---|---|
| [Capability] | | |

## Data Ownership

| Data | Reads | Writes | Retains | Exposes to user |
|---|---|---|---|---|
| [Data object] | | | | |

## Triggers

| Trigger | Source | Result |
|---|---|---|
| [Event/schedule/request] | | |

## States

| State | Meaning | User-visible behaviour |
|---|---|---|
| Available | | |
| Degraded | | |
| Unavailable | | |

## Failure Modes

| Failure | Cause | User-visible impact | Recovery |
|---|---|---|---|
| [Failure] | | | |

## Constraints for Flow Design

| Constraint | Implication |
|---|---|
| Latency | |
| Reliability | |
| Permissions | |
| Rate limits / quotas | |
| Privacy / security | |
| Observability | |

## Jobs This Actor Performs

| Job ID | Job statement | Frequency | Notes |
|---|---|---|---|
| J-001 | | | |

## Scenarios Involving This Actor

| Scenario ID | Scenario name | Role in scenario |
|---|---|---|
| SC-01 | | |
```

**Template (permissions.md):**
```markdown
# Actor Capability Matrix

> File: docs/ux-ui/actors/permissions.md

| Capability | [Andy the App User] | [Rachel the Receptionist] | [Sync Worker] |
|---|---|---|---|
| [Feature or action] | ✓ | — | — |
| [Feature or action] | ✓ | ✓ | — |
| [Automated/system action] | — | — | ✓ |
```

---
