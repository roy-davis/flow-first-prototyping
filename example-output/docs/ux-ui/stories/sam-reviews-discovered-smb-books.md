> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Review discovered SMB books

> File: docs/ux-ui/stories/sam-reviews-discovered-smb-books.md
> Primary actor: Sam the Server Steward
> Journey: sam-connects-smb-library.md
> Journey stage: Indexing and handoff
> Priority: Should-have

- Task slice: Review books discovered from the SMB source before they enter the listening library.
- Real-world trigger: SMB indexing completes or has usable partial results.
- Problem: Auto-adding every indexed folder may clutter the listening library.
- Story statement: As Sam the Server Steward, I want to review books discovered from the SMB source before they enter the listening library, so I can make progress without losing audiobook or source context.
- Value: Source owners can confirm what the app discovered.
- Outcome: Sam can hand off discovered books to listening-library curation.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Discovered Books shows source and sync result.
  - Unsupported/skipped items are visible as warnings.
  - Add to listening library is available per discovered book.
  - Already-added books are marked.
- Data needed: Discovered book list, source, sync status, support status, added status.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: sam-reviews-discovered-smb-books.md
