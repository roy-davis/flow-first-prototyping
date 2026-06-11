> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Validate SMB connection

> File: docs/ux-ui/stories/sam-validates-smb-connection.md
> Primary actor: Sam the Server Steward
> Journey: sam-connects-smb-library.md
> Journey stage: Validating SMB connection
> Priority: Must-have

- Task slice: Enter and test SMB host, share, and credential details.
- Real-world trigger: SMB Setup opens from Sources or Source Repair.
- Problem: SMB failures are costly to diagnose on a TV remote.
- Story statement: As Sam the Server Steward, I want to enter and test SMB host, share, and credential details, so I can make progress without losing audiobook or source context.
- Value: Specific validation prevents indexing the wrong or unreachable source.
- Outcome: The connection validates or Sam sees host/share/credential-specific recovery.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Required fields gate Test connection.
  - Anonymous mode hides credential fields.
  - Testing blocks duplicate submission.
  - Host, share, credential, and permission errors are distinct.
- Data needed: Host, share, username/password or anonymous mode, validation result.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: sam-validates-smb-connection.md
