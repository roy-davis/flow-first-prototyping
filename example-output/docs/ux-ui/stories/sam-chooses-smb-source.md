> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Choose SMB source

> File: docs/ux-ui/stories/sam-chooses-smb-source.md
> Primary actor: Sam the Server Steward
> Journey: sam-connects-smb-library.md
> Journey stage: Preparing source details
> Priority: Must-have

- Task slice: Choose SMB as the source type.
- Real-world trigger: Sam starts Add source for a NAS or Windows/Samba share.
- Problem: Cloud, SMB, and WebDAV choices can be confused if grouped generically.
- Story statement: As Sam the Server Steward, I want to choose SMB as the source type, so I can make progress without losing audiobook or source context.
- Value: The setup path starts with the right source-specific branch.
- Outcome: SMB Setup opens with local-share fields.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Sources presents SMB separately from cloud providers.
  - WebDAV remains advanced/custom.
  - Back returns to the origin screen.
  - SMB selection does not ask for provider auth.
- Data needed: Static source type list, existing connected status.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: sam-chooses-smb-source.md
