> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Start selected book

> File: docs/ux-ui/stories/leo-starts-selected-book.md
> Primary actor: Leo the Living Room Listener
> Journey: leo-browses-and-starts-book.md
> Journey stage: Starting selected playback
> Priority: Must-have

- Task slice: Start or resume the selected book from Book Detail.
- Real-world trigger: Leo presses Resume, Start, or a chapter row.
- Problem: Playback can fail after cached metadata looked ready.
- Story statement: As Leo the Living Room Listener, I want to start or resume the selected book from Book Detail, so I can make progress without losing audiobook or source context.
- Value: The start transition proves cache-backed browsing still leads to reliable streaming.
- Outcome: Now Playing opens in buffering, then playing, or Source Repair explains the blocker.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Starting state is visible.
  - Duplicate starts are blocked.
  - Now Playing receives book and position context.
  - Source failure routes to Source Repair with origin preserved.
- Data needed: Selected book, selected chapter, playable asset reference, saved position, source status.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: leo-starts-selected-book.md
