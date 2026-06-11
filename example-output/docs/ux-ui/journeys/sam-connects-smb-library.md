> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Journey: Sam connects SMB library

> File: docs/ux-ui/journeys/sam-connects-smb-library.md
> Primary actor: Sam the Server Steward
> Real-world trigger: The household wants to add a NAS or Windows/Samba audiobook folder.
> Starting context: The household wants to add a NAS or Windows/Samba audiobook folder.
> Resolved end state: SMB books are discovered and ready for review.

## Stages

### Stage 1: Preparing source details
Cloud, SMB, and WebDAV choices can be confused if grouped generically. The setup path starts with the right source-specific branch.

**Data needed:** Static source type list, existing connected status.
**Friction risk:** SMB selection does not ask for provider auth.

### Stage 2: Validating SMB connection
SMB failures are costly to diagnose on a TV remote. Specific validation prevents indexing the wrong or unreachable source.

**Data needed:** Host, share, username/password or anonymous mode, validation result.
**Friction risk:** Host, share, credential, and permission errors are distinct.

### Stage 3: Choosing library folder
Choosing a blocked or overly broad folder creates confusing sync results. The app indexes the intended audiobook root.

**Data needed:** SMB source, folder listing, selected path, permission status.
**Friction risk:** Back returns to SMB Setup with context preserved.

### Stage 4: Indexing and handoff
Large SMB folders need progress and partial-result handling. The app discovers books without blocking the TV UI.

**Data needed:** Source, selected folder, books/tracks scanned, skipped items, sync status.
**Friction risk:** Source failures route to Source Repair.

### Stage 5: Indexing and handoff
Auto-adding every indexed folder may clutter the listening library. Source owners can confirm what the app discovered.

**Data needed:** Discovered book list, source, sync status, support status, added status.
**Friction risk:** Already-added books are marked.

## Moments that matter

- **Story boundaries:** Each stage maps to a smaller story rather than one epic flow.
- **Context preservation:** Back, repair, and add-to-library actions preserve the selected source, book, focused card, or playback position.
- **Discovery versus library:** Discovered books are not assumed to be in the listening library until an add action succeeds.

## Story opportunities

| Stage | Story candidate | Why it matters |
| --- | --- | --- |
| Preparing source details | sam-chooses-smb-source.md | The setup path starts with the right source-specific branch. |
| Validating SMB connection | sam-validates-smb-connection.md | Specific validation prevents indexing the wrong or unreachable source. |
| Choosing library folder | sam-selects-smb-library-folder.md | The app indexes the intended audiobook root. |
| Indexing and handoff | sync-worker-indexes-smb-source.md | The app discovers books without blocking the TV UI. |
| Indexing and handoff | sam-reviews-discovered-smb-books.md | Source owners can confirm what the app discovered. |

## Screens implied

| Stage | Screen needed |
| --- | --- |
| Preparing source details | Sources, SMB Setup, Folder Picker, Sync Progress, Discovered Books |
| Validating SMB connection | Sources, SMB Setup, Folder Picker, Sync Progress, Discovered Books |
| Choosing library folder | Sources, SMB Setup, Folder Picker, Sync Progress, Discovered Books |
| Indexing and handoff | Sources, SMB Setup, Folder Picker, Sync Progress, Discovered Books |
| Indexing and handoff | Sources, SMB Setup, Folder Picker, Sync Progress, Discovered Books |

## Stories and flows that implement this journey

| Story file | Flow file |
| --- | --- |
| sam-chooses-smb-source.md | sam-chooses-smb-source.md |
| sam-validates-smb-connection.md | sam-validates-smb-connection.md |
| sam-selects-smb-library-folder.md | sam-selects-smb-library-folder.md |
| sync-worker-indexes-smb-source.md | sync-worker-indexes-smb-source.md |
| sam-reviews-discovered-smb-books.md | sam-reviews-discovered-smb-books.md |
