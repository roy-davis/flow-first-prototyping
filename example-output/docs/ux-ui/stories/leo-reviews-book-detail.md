> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Review book detail

> File: docs/ux-ui/stories/leo-reviews-book-detail.md
> Primary actor: Leo the Living Room Listener
> Journey: leo-browses-and-starts-book.md
> Journey stage: Confirming a book
> Priority: Must-have

- Task slice: Open one focused book and review title, progress, source status, and chapters.
- Real-world trigger: Leo selects a focused book from Library.
- Problem: A card alone does not show enough context to choose a chapter or trust source availability.
- Story statement: As Leo the Living Room Listener, I want to open one focused book and review title, progress, source status, and chapters, so I can make progress without losing audiobook or source context.
- Value: Book Detail lets Leo confirm the book before playback starts.
- Outcome: Leo sees enough context to start, resume, choose a chapter, or repair source.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Book Detail shows metadata and progress from cache.
  - Chapter list scrolls without hiding primary action.
  - Source unavailable state keeps cached book context visible.
  - Back returns to the same focused Library card.
- Data needed: Book metadata, chapter list, progress, source health.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: leo-reviews-book-detail.md
