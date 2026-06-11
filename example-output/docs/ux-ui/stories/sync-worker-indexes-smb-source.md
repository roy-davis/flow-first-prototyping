> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Index SMB source

> File: docs/ux-ui/stories/sync-worker-indexes-smb-source.md
> Primary actor: Sync Worker
> Journey: sam-connects-smb-library.md
> Journey stage: Indexing and handoff
> Priority: Must-have

- Task slice: Index the selected SMB folder into discovered audiobook records.
- Real-world trigger: Sam selects the SMB library folder.
- Problem: Large SMB folders need progress and partial-result handling.
- Story statement: As Sync Worker, I want to index the selected SMB folder into discovered audiobook records, so I can make progress without losing audiobook or source context.
- Value: The app discovers books without blocking the TV UI.
- Outcome: Discovered books are available for review, or sync explains skipped items.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Sync Progress shows queued/indexing/partial/complete states.
  - Counts distinguish books, tracks, and skipped items.
  - Partial success still exposes discovered books.
  - Source failures route to Source Repair.
- Data needed: Source, selected folder, books/tracks scanned, skipped items, sync status.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: sync-worker-indexes-smb-source.md
