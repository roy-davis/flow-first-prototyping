> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Flow: Select SMB library folder

> File: docs/ux-ui/flows/sam-selects-smb-library-folder.md
> Primary actor: Sam the Server Steward
> Story: sam-selects-smb-library-folder.md
> Journey: sam-connects-smb-library.md
> Implements: Choosing library folder

- Trigger: SMB connection validates successfully.
- Entry point: Screen/state implied by Choosing library folder.
- Preconditions: Relevant source, cache, or selection state exists; user has reached the source screen for this story.
- Steps:
  1. Actor enters the relevant screen for Choosing library folder.
  2. The app renders the current state and required data for this single task slice.
  3. Actor takes the primary action for "Select SMB library folder".
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
- Exit states: Sync starts for the selected SMB folder.
- Completion criteria: Sync starts for the selected SMB folder.
