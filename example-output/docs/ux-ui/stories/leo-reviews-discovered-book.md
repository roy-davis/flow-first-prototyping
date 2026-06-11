> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Review discovered book

> File: docs/ux-ui/stories/leo-reviews-discovered-book.md
> Primary actor: Leo the Living Room Listener
> Journey: leo-discovers-and-adds-book.md
> Journey stage: Inspecting a discovered book
> Priority: Should-have

- Task slice: Inspect a discovered audiobook before adding it to the listening library.
- Real-world trigger: Leo opens a discovered book from Discovered Books.
- Problem: A discovered folder may not be a book Leo wants in his listening library.
- Story statement: As Leo the Living Room Listener, I want to inspect a discovered audiobook before adding it to the listening library, so I can make progress without losing audiobook or source context.
- Value: Leo can decide with title, author, chapters, source, and support status visible.
- Outcome: Leo is ready to add the book, skip it, or leave it discovered.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Book Detail has a discovered/not-added state.
  - Add to library is primary when not added.
  - Unsupported or incomplete books explain why Add is blocked.
  - Back returns to the same discovered item.
- Data needed: Discovered book metadata, chapters, source, support status, added status.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: leo-reviews-discovered-book.md
