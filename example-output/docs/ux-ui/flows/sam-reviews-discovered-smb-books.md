> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Flow: Review discovered SMB books

> File: docs/ux-ui/flows/sam-reviews-discovered-smb-books.md
> Primary actor: Sam the Server Steward
> Story: sam-reviews-discovered-smb-books.md
> Journey: sam-connects-smb-library.md
> Implements: Indexing and handoff

- Trigger: SMB indexing completes or has usable partial results.
- Entry point: Screen/state implied by Indexing and handoff.
- Preconditions: Relevant source, cache, or selection state exists; user has reached the source screen for this story.
- Steps:
  1. Actor enters the relevant screen for Indexing and handoff.
  2. The app renders the current state and required data for this single task slice.
  3. Actor takes the primary action for "Review discovered SMB books".
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
- Exit states: Sam can hand off discovered books to listening-library curation.
- Completion criteria: Sam can hand off discovered books to listening-library curation.
