> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Add book to listening library

> File: docs/ux-ui/stories/leo-adds-book-to-listening-library.md
> Primary actor: Leo the Living Room Listener
> Journey: leo-discovers-and-adds-book.md
> Journey stage: Adding to listening library
> Priority: Must-have

- Task slice: Add one discovered audiobook to the listening library.
- Real-world trigger: Leo chooses Add to library on a discovered book.
- Problem: Discovery alone does not explain how a book becomes part of Leo's listening library.
- Story statement: As Leo the Living Room Listener, I want to add one discovered audiobook to the listening library, so I can make progress without losing audiobook or source context.
- Value: The product gains an explicit curation step between indexed catalog and listening library.
- Outcome: The book appears in Library as an added listening-library item.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Add to library has loading/success/error states.
  - Already-added books cannot be added twice.
  - Success keeps return path to discovered list or Library.
  - Library shows the newly added book.
- Data needed: Discovered book, listening library item, added status, source health.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: leo-adds-book-to-listening-library.md
