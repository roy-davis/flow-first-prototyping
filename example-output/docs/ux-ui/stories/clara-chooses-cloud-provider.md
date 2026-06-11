> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Choose cloud provider

> File: docs/ux-ui/stories/clara-chooses-cloud-provider.md
> Primary actor: Clara the Cloud Collector
> Journey: clara-connects-cloud-library.md
> Journey stage: Choosing provider
> Priority: Must-have

- Task slice: Choose a first-class cloud provider.
- Real-world trigger: Clara starts Add source for cloud audiobooks.
- Problem: Named providers should not be hidden behind generic WebDAV.
- Story statement: As Clara the Cloud Collector, I want to choose a first-class cloud provider, so I can make progress without losing audiobook or source context.
- Value: Clara can choose the provider she recognizes.
- Outcome: Provider Authorization opens for the selected provider.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Dropbox, Google Drive, iCloud Drive, and OneDrive are first-class choices.
  - WebDAV is advanced/custom.
  - Provider choice preserves origin.
  - Offline state explains auth requires internet.
- Data needed: Provider list, connected status, provider availability.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: clara-chooses-cloud-provider.md
