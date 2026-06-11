> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Resume current book

> File: docs/ux-ui/stories/leo-resumes-current-book.md
> Primary actor: Leo the Living Room Listener
> Journey: leo-resumes-current-book.md
> Journey stage: Checking resume context
> Priority: Must-have

- Task slice: Resume the cached current audiobook from the saved millisecond.
- Real-world trigger: Leo opens the app after a prior session.
- Problem: Long-form progress is hard to recover if the app loses context or blocks on source health.
- Story statement: As Leo the Living Room Listener, I want to resume the cached current audiobook from the saved millisecond, so I can make progress without losing audiobook or source context.
- Value: The fastest path proves the app is built for audiobooks.
- Outcome: Playback begins at the saved position or Leo sees a clear repair entry.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Home shows the cached current book and saved position.
  - Resume is the default focused action.
  - Starting feedback blocks duplicate activation.
  - Source failure preserves progress and routes to repair.
- Data needed: Current book, chapter, saved millisecond, source health, playable asset reference.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: leo-resumes-current-book.md
