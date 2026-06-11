> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Select cloud library folder

> File: docs/ux-ui/stories/clara-selects-cloud-library-folder.md
> Primary actor: Clara the Cloud Collector
> Journey: clara-connects-cloud-library.md
> Journey stage: Selecting provider folder
> Priority: Must-have

- Task slice: Choose the provider folder that contains audiobooks.
- Real-world trigger: Provider authorization succeeds.
- Problem: Provider permissions and capabilities can block folder access or streaming.
- Story statement: As Clara the Cloud Collector, I want to choose the provider folder that contains audiobooks, so I can make progress without losing audiobook or source context.
- Value: Folder choice happens with provider-specific status before indexing.
- Outcome: Sync starts for the selected provider folder.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Folder Picker shows provider identity and path.
  - Permission-blocked folders are not selectable.
  - Capability warnings are visible.
  - Back returns to Provider Authorization with context.
- Data needed: Provider folder list, selected path, capability model, permission state.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: clara-selects-cloud-library-folder.md
