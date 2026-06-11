> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: See playback source failure

> File: docs/ux-ui/stories/leo-sees-playback-source-failure.md
> Primary actor: Leo the Living Room Listener
> Journey: leo-recovers-from-source-dropout.md
> Journey stage: Playback interruption
> Priority: Must-have

- Task slice: See why playback stopped while preserving the saved position.
- Real-world trigger: Playback stalls, buffers too long, or fails to resolve the playable asset.
- Problem: Source failures can look like player bugs and can threaten audiobook progress.
- Story statement: As Leo the Living Room Listener, I want to see why playback stopped while preserving the saved position, so I can make progress without losing audiobook or source context.
- Value: A specific playback error keeps trust in progress persistence.
- Outcome: Leo sees saved position, source identity, Retry playback, and Repair source.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Latest known position is visible.
  - Failure category is source-specific.
  - Retry and Repair actions are distinct.
  - No raw URL, token, file ID, or stack trace appears.
- Data needed: Playback state, saved position, source identity, failure category.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: leo-sees-playback-source-failure.md
