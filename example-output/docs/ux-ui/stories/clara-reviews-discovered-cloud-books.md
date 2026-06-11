> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Review discovered cloud books

> File: docs/ux-ui/stories/clara-reviews-discovered-cloud-books.md
> Primary actor: Clara the Cloud Collector
> Journey: clara-connects-cloud-library.md
> Journey stage: Indexing cloud library
> Priority: Should-have

- Task slice: Review books discovered from a cloud source before they enter the listening library.
- Real-world trigger: Cloud indexing completes or has usable partial results.
- Problem: Cloud folders can include unrelated audio, duplicates, or unsupported files.
- Story statement: As Clara the Cloud Collector, I want to review books discovered from a cloud source before they enter the listening library, so I can make progress without losing audiobook or source context.
- Value: Clara can curate discovered books instead of polluting the listener's library.
- Outcome: Discovered cloud books are ready to add or skip.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Discovered Books shows source/provider and sync result.
  - Unsupported or duplicate items are marked.
  - Add to listening library is available per discovered book.
  - Already-added books are marked.
- Data needed: Discovered book list, provider, support/duplicate status, added status.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: clara-reviews-discovered-cloud-books.md
