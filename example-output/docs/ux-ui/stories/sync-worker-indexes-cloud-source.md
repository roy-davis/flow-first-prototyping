> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Index cloud source

> File: docs/ux-ui/stories/sync-worker-indexes-cloud-source.md
> Primary actor: Sync Worker
> Journey: clara-connects-cloud-library.md
> Journey stage: Indexing cloud library
> Priority: Must-have

- Task slice: Index the selected cloud folder into discovered audiobook records.
- Real-world trigger: Clara selects the provider folder.
- Problem: Cloud providers may rate-limit, skip files, or restrict folder access.
- Story statement: As Sync Worker, I want to index the selected cloud folder into discovered audiobook records, so I can make progress without losing audiobook or source context.
- Value: Cloud metadata becomes locally discoverable without blocking browsing.
- Outcome: Discovered cloud books are available for review, or sync explains blockers.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Sync Progress shows provider source identity.
  - Rate limit/partial sync states are distinct.
  - Usable partial results can be reviewed.
  - Auth failures route to Source Repair.
- Data needed: Provider source, folder, book/track counts, skipped files, auth/rate status.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: sync-worker-indexes-cloud-source.md
