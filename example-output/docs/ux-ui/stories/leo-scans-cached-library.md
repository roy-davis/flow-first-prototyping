> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Scan cached library

> File: docs/ux-ui/stories/leo-scans-cached-library.md
> Primary actor: Leo the Living Room Listener
> Journey: leo-browses-and-starts-book.md
> Journey stage: Scanning the library
> Priority: Must-have

- Task slice: Scan the cached listening library and focus one book.
- Real-world trigger: Leo chooses Browse library or arrives after setup.
- Problem: Remote folder browsing is too slow and hard to control from a TV remote.
- Story statement: As Leo the Living Room Listener, I want to scan the cached listening library and focus one book, so I can make progress without losing audiobook or source context.
- Value: A cache-first library feels local even when files live on SMB or cloud.
- Outcome: Leo can focus a candidate book without losing grid position.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Library renders from local metadata only.
  - Focused book card is visually obvious.
  - Missing artwork has a usable fallback.
  - Large libraries preserve focus and scroll position.
- Data needed: Listening library book list, title, author, progress, source badge, artwork fallback.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: leo-scans-cached-library.md
