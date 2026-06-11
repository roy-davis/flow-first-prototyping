> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Select SMB library folder

> File: docs/ux-ui/stories/sam-selects-smb-library-folder.md
> Primary actor: Sam the Server Steward
> Journey: sam-connects-smb-library.md
> Journey stage: Choosing library folder
> Priority: Must-have

- Task slice: Choose the readable SMB folder that should be indexed.
- Real-world trigger: SMB connection validates successfully.
- Problem: Choosing a blocked or overly broad folder creates confusing sync results.
- Story statement: As Sam the Server Steward, I want to choose the readable SMB folder that should be indexed, so I can make progress without losing audiobook or source context.
- Value: The app indexes the intended audiobook root.
- Outcome: Sync starts for the selected SMB folder.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Folder Picker shows current source and path.
  - Unreadable folders block selection.
  - Long paths remain readable.
  - Back returns to SMB Setup with context preserved.
- Data needed: SMB source, folder listing, selected path, permission status.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: sam-selects-smb-library-folder.md
