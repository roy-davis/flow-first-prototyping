> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Retry failed source

> File: docs/ux-ui/stories/leo-retries-failed-source.md
> Primary actor: Leo the Living Room Listener
> Journey: leo-recovers-from-source-dropout.md
> Journey stage: Diagnosing source health
> Priority: Should-have

- Task slice: Retry a failed source before entering deeper repair.
- Real-world trigger: Leo lands on Source Repair from a playback or source failure.
- Problem: Some failures are brief network dropouts and should not force full setup.
- Story statement: As Leo the Living Room Listener, I want to retry a failed source before entering deeper repair, so I can make progress without losing audiobook or source context.
- Value: Retry is the smallest safe recovery action.
- Outcome: The source either recovers and returns to origin or remains in repair with the right next action.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Retry has loading and repeated-error states.
  - Repair complete returns to origin.
  - Cached library remains available when readable.
  - Credential/auth repair is shown only when diagnosis requires it.
- Data needed: Source type, failure category, last sync, cached availability, origin route.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: leo-retries-failed-source.md
