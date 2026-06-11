> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Flow: Choose SMB source

> File: docs/ux-ui/flows/sam-chooses-smb-source.md
> Primary actor: Sam the Server Steward
> Story: sam-chooses-smb-source.md
> Journey: sam-connects-smb-library.md
> Implements: Preparing source details

- Trigger: Sam starts Add source for a NAS or Windows/Samba share.
- Entry point: Screen/state implied by Preparing source details.
- Preconditions: Relevant source, cache, or selection state exists; user has reached the source screen for this story.
- Steps:
  1. Actor enters the relevant screen for Preparing source details.
  2. The app renders the current state and required data for this single task slice.
  3. Actor takes the primary action for "Choose SMB source".
  4. The app shows loading, success, blocked, or error feedback.
  5. The flow exits to the adjacent screen/state or preserves context for retry/back.
- Decision points: One primary decision only for this story.
- In-flow opportunities: Contextual actions preserve selected source/book/chapter/playback/discovered item and return to the same state.
- Interruption risks: Back, cancel, retry, and repair must preserve origin context.
- Branches:
  - Required data missing: show empty/blocked state and recovery.
  - Source unavailable: route to Source Repair when the task depends on source access.
  - Duplicate action: keep focus and disable repeated trigger while loading.
- Error paths: Permission denied, offline/degraded source, local cache unavailable, provider/SMB failure, unsupported book, duplicate add.
- Exit states: SMB Setup opens with local-share fields.
- Completion criteria: SMB Setup opens with local-share fields.
