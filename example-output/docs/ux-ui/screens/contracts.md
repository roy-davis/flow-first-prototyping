> Provisional: updated after story-splitting pass. Review before treating as authoritative.

# Page Contracts

> File: docs/ux-ui/screens/contracts.md

---

## Home - PG01

**Story:** leo-resumes-current-book.md | **Flow:** leo-resumes-current-book.md | **Actor:** Leo the Living Room Listener | **State:** Resume available

### Purpose
Give the listener the fastest path back into the current audiobook.

### Current state displayed
- Object shown: Current book and source status
- Status: Resume available
- What happened: App launch, Android TV dashboard return, Back from Now Playing.
- What is pending: resume_available, no_source, source_unavailable
- What needs attention: Source unavailable

### Primary decision
- Decision: Resume current book
- Options: Resume; Browse library; Add source; Repair source
- Information required: Current book title/author; chapter and position; source health
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Browse library | Open curated listening library | Local metadata cache readable |
| Add source | Start source setup | Always |
| Repair source | Open repair flow | Source degraded or unavailable |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Resume | Primary | Current book exists and source is playable | Start current book at saved position | buffering | Now Playing |
| Browse library | Secondary | Local metadata cache readable | Open curated listening library | loaded_grid / empty_library | Library |
| Add source | Secondary | Always | Start source setup | default_providers | Sources |
| Repair source | Secondary | Source degraded or unavailable | Open repair flow | source_unavailable | Source Repair |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | Show no-source state with Add source CTA |
| Permission denied | Repair source if token/permission blocked |
| Conflicting state | Prefer cached context plus source/status warning |
| Action fails | Keep the current book visible and offer Repair source or Retry |
| Session expired | Route to Provider Authorization or Source Repair when relevant |
---

## Sources - PG02

**Story:** sam-chooses-smb-source.md; clara-chooses-cloud-provider.md | **Flow:** sam-chooses-smb-source.md; clara-chooses-cloud-provider.md | **Actor:** Sam the Server Steward; Clara the Cloud Collector | **State:** Default providers

### Purpose
Let the source owner choose the correct storage type.

### Current state displayed
- Object shown: Source/provider options
- Status: Default providers
- What happened: Home Add source, Library empty state, or Source Repair add/replace source.
- What is pending: default_providers, advanced_webdav
- What needs attention: Unavailable provider or existing source warning

### Primary decision
- Decision: Choose source type
- Options: Select SMB; Select cloud provider; Show advanced; Back
- Information required: Source type list; existing source status
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Select cloud provider | Open provider authorization | Provider available |
| Show advanced | Reveal WebDAV | Always |
| Back | Return to previous screen | Always |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Select SMB | Primary | Always | Open local share setup | credentials_form | SMB Setup |
| Select cloud provider | Secondary | Provider available | Open provider authorization | provider_selected | Provider Authorization |
| Show advanced | Secondary | Always | Reveal WebDAV | default_providers | Sources |
| Back | Secondary | Always | Return to previous screen | default_providers | Origin |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | Static provider list still renders |
| Permission denied | Unavailable provider appears disabled with reason |
| Conflicting state | Show current source status without blocking new setup |
| Action fails | Show source-specific recovery path |
| Session expired | Route to Provider Authorization or Source Repair when relevant |
---

## SMB Setup - PG03

**Story:** sam-validates-smb-connection.md | **Flow:** sam-validates-smb-connection.md | **Actor:** Sam the Server Steward | **State:** Credentials form

### Purpose
Collect and validate SMB source details before folder selection.

### Current state displayed
- Object shown: SMB connection details
- Status: Credentials form
- What happened: Sources Select SMB or Source Repair Edit SMB credentials.
- What is pending: credentials_form, testing_connection, connection_error, anonymous_login
- What needs attention: Connection failed

### Primary decision
- Decision: Validate SMB connection
- Options: Test connection; Use anonymous login; Continue; Cancel
- Information required: Host/share; credential mode; validation result
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Use anonymous login | Toggle credential mode | Always |
| Continue | Go to Folder Picker after validation | Connection valid |
| Cancel | Return to Sources or Source Repair | Always |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Test connection | Primary | Required fields present or anonymous mode selected | Validate SMB source | testing_connection / connection_valid | SMB Setup |
| Use anonymous login | Secondary | Always | Toggle credential mode | credentials_form | SMB Setup |
| Continue | Secondary | Connection valid | Go to folder picker | folder_browsing | Folder Picker |
| Cancel | Secondary | Always | Return to prior screen | default_providers | Sources / Source Repair |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | Disable Test connection until required fields exist |
| Permission denied | Bad credentials and permission denied have separate messages |
| Conflicting state | Preserve typed values while showing validation warning |
| Action fails | Check the host, share, and credentials, then try again |
| Session expired | N/A for SMB unless credentials expire in source repair |
---

## Provider Authorization - PG04

**Story:** clara-authorizes-cloud-provider.md | **Flow:** clara-authorizes-cloud-provider.md | **Actor:** Clara the Cloud Collector | **State:** Provider selected

### Purpose
Guide provider-specific cloud authorization.

### Current state displayed
- Object shown: Selected cloud provider account
- Status: Provider selected
- What happened: Sources selected cloud provider or Source Repair Reauthorize provider.
- What is pending: provider_selected, auth_pending, auth_success, auth_error
- What needs attention: Authorization failed

### Primary decision
- Decision: Authorize provider account
- Options: Start authorization; Retry authorization; Continue; Cancel
- Information required: Provider identity; auth state; account metadata
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Retry authorization | Restart failed auth | Auth failed or timed out |
| Continue | Open Folder Picker | Auth success |
| Cancel | Return to Sources or Source Repair | Always |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Start authorization | Primary | Provider selected and internet available | Begin provider auth | auth_pending | Provider Authorization |
| Retry authorization | Secondary | Auth failed or timed out | Restart failed auth | auth_pending | Provider Authorization |
| Continue | Secondary | Auth success | Open Folder Picker | folder_browsing | Folder Picker |
| Cancel | Secondary | Always | Return to prior screen | default_providers | Sources / Source Repair |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | Provider selected is required before this screen |
| Permission denied | Auth error states distinguish denied vs timeout |
| Conflicting state | Show authorized account and allow replacement |
| Action fails | The provider did not authorize this source; check the account and try again |
| Session expired | Route back here with reauthorization_required |
---

## Folder Picker - PG05

**Story:** sam-selects-smb-library-folder.md; clara-selects-cloud-library-folder.md | **Flow:** sam-selects-smb-library-folder.md; clara-selects-cloud-library-folder.md | **Actor:** Sam the Server Steward; Clara the Cloud Collector | **State:** Folder browsing

### Purpose
Let the source owner choose the audiobook root folder.

### Current state displayed
- Object shown: Source folder tree
- Status: Folder browsing
- What happened: SMB validation success or Provider Authorization success.
- What is pending: folder_browsing, permission_blocked, empty_folder
- What needs attention: Folder cannot be opened

### Primary decision
- Decision: Select library folder
- Options: Open folder; Select this folder; Go up; Retry listing; Choose another folder
- Information required: Source identity; folder list; selected path; capability warning
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Open folder | Navigate into focused folder | Folder readable |
| Go up | Move to parent folder | Parent exists |
| Retry listing | Reload current folder | Permission or network issue |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Open folder | Primary | Folder readable | Navigate into focused folder | folder_browsing | Folder Picker |
| Select this folder | Secondary | Folder readable | Use current folder as library root | queued / indexing | Sync Progress |
| Go up | Secondary | Parent exists | Move to parent folder | folder_browsing | Folder Picker |
| Choose another folder | Secondary | Always | Return to readable folder | folder_browsing | Folder Picker |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | Show empty folder state with Choose another folder |
| Permission denied | Blocked folder state with recovery |
| Conflicting state | Keep selected source visible while browsing |
| Action fails | This source did not allow access to the selected folder |
| Session expired | Route to Provider Authorization or Source Repair when relevant |
---

## Sync Progress - PG06

**Story:** sync-worker-indexes-smb-source.md; sync-worker-indexes-cloud-source.md | **Flow:** sync-worker-indexes-smb-source.md; sync-worker-indexes-cloud-source.md | **Actor:** Sync Worker; Sam the Server Steward; Clara the Cloud Collector | **State:** Indexing

### Purpose
Show background indexing progress and route discovered results into review.

### Current state displayed
- Object shown: Source indexing job
- Status: Indexing
- What happened: Folder Picker Select this folder.
- What is pending: queued, indexing, complete, partial_error
- What needs attention: Some items were skipped

### Primary decision
- Decision: Review discovered books after indexing
- Options: Review discovered books; Run in background; Retry sync; Review source
- Information required: Source name/type; progress counts; current item; error summary
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Run in background | Leave while worker continues | Sync active |
| Retry sync | Restart failed/partial sync | Partial or failed state |
| Review source | Open Source Repair | Partial or blocked state |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Review discovered books | Primary | Sync has produced a result | Open discovered catalog | discovered_list / partial_results / empty_discovered | Discovered Books |
| Run in background | Secondary | Sync active | Leave while worker continues | indexing | Origin |
| Retry sync | Secondary | Partial or failed state | Restart failed/partial sync | queued | Sync Progress |
| Review source | Secondary | Partial or blocked state | Open Source Repair | source_unavailable | Source Repair |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | Show queued/indexing before counts arrive |
| Permission denied | Partial/error links to Source Repair |
| Conflicting state | Prefer current job state and avoid duplicate indexing |
| Action fails | The source is connected, but some folders or files could not be indexed |
| Session expired | Route to Provider Authorization or Source Repair when relevant |
---

## Discovered Books - PG11

**Story:** sam-reviews-discovered-smb-books.md; clara-reviews-discovered-cloud-books.md; leo-reviews-discovered-book.md; leo-adds-book-to-listening-library.md | **Flow:** sam-reviews-discovered-smb-books.md; clara-reviews-discovered-cloud-books.md; leo-reviews-discovered-book.md; leo-adds-book-to-listening-library.md | **Actor:** Leo the Living Room Listener; Sam the Server Steward; Clara the Cloud Collector | **State:** Discovered list

### Purpose
Let a listener or source owner review indexed books before adding them to the listening library.

### Current state displayed
- Object shown: Discovered audiobook catalog
- Status: Discovered list
- What happened: Sync Progress completed or Library empty state opened discovered books.
- What is pending: discovered_list, partial_results, empty_discovered, added_state, unsupported_blocked
- What needs attention: Unsupported, duplicate, or partially indexed books

### Primary decision
- Decision: Add a discovered book to the listening library
- Options: Add to library; Open details; View library; Review source issue; Choose another folder
- Information required: Book title/author; source; support status; added status
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Open details | Review a discovered book | Discovered book exists |
| View library | Open listening library | At least one added book |
| Review source issue | Open Source Repair or sync warning | Partial or blocked result |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Add to library | Primary | Supported and not already added | Create listening-library item | added_state | Discovered Books |
| Open details | Secondary | Discovered book exists | Open discovered book detail | discovered_not_added / added | Book Detail |
| View library | Secondary | At least one added book | Open curated listening library | loaded_grid | Library |
| Choose another folder | Secondary | No discovered books or wrong folder | Return to folder selection | folder_browsing | Folder Picker |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | Empty discovered state with Choose another folder / Add source |
| Permission denied | Blocked items show reason and repair |
| Conflicting state | Already-added state disables duplicate add |
| Action fails | Keep focus on row and show row-level error |
| Session expired | Route to Provider Authorization or Source Repair when relevant |
---

## Library - PG07

**Story:** leo-scans-cached-library.md; leo-adds-book-to-listening-library.md | **Flow:** leo-scans-cached-library.md; leo-adds-book-to-listening-library.md | **Actor:** Leo the Living Room Listener | **State:** Loaded grid

### Purpose
Browse curated listening-library audiobook metadata quickly from the couch.

### Current state displayed
- Object shown: Listening-library book collection
- Status: Loaded grid
- What happened: Home Browse library, Discovered Books View library, empty current book, cached library from repair.
- What is pending: loading_cache, loaded_grid, empty_library, stale_source
- What needs attention: Library unavailable or discovered books pending review

### Primary decision
- Decision: Choose book
- Options: Select book; Resume focused book; Review discovered books; Add source; Repair source
- Information required: Book list; source status; library state
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Resume focused book | Start/resume focused book | Focused book has progress and source playable |
| Review discovered books | Open discovered catalog | Discovered books exist |
| Add source | Open source setup | Always |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Select book | Primary | Book exists | Open Book Detail | ready | Book Detail |
| Resume focused book | Secondary | Focused book has progress and source playable | Start/resume focused book | buffering | Now Playing |
| Review discovered books | Secondary | Discovered books exist | Open discovered catalog | discovered_list | Discovered Books |
| Repair source | Secondary | Focused/source degraded | Open repair flow | source_unavailable | Source Repair |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | Show empty library state with Add source or Review discovered books |
| Permission denied | Blocked sources show repair action |
| Conflicting state | Prefer added listening-library items over raw discovered items |
| Action fails | The local library cache could not be read |
| Session expired | Route to Provider Authorization or Source Repair when relevant |
---

## Book Detail - PG08

**Story:** leo-reviews-book-detail.md; leo-reviews-discovered-book.md; leo-starts-selected-book.md | **Flow:** leo-reviews-book-detail.md; leo-reviews-discovered-book.md; leo-starts-selected-book.md | **Actor:** Leo the Living Room Listener | **State:** Ready

### Purpose
Show audiobook context and let the listener start/resume or add a discovered book to the listening library.

### Current state displayed
- Object shown: Selected or discovered book
- Status: Ready
- What happened: Library select book or Discovered Books open details.
- What is pending: ready, discovered_not_added, source_unavailable, no_chapters
- What needs attention: Source unavailable or book not yet added

### Primary decision
- Decision: Confirm selected book action
- Options: Add to library; Resume; Start from beginning; Select chapter; Repair source
- Information required: Book metadata; chapters/tracks; added status; playback progress; source health
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Add to library | Add discovered book | Discovered and supported but not added |
| Start from beginning | Start first chapter | Source playable |
| Select chapter | Start a specific chapter | Chapter available and source playable |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Add to library | Primary | Discovered and supported but not added | Create listening-library item | added | Book Detail |
| Resume | Primary | Progress exists and source playable | Start from saved progress | buffering | Now Playing |
| Start from beginning | Secondary | Source playable | Start first chapter | buffering | Now Playing |
| Repair source | Secondary | Source degraded | Open repair flow | source_unavailable | Source Repair |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | If no chapters, show cannot play and retry/resync action |
| Permission denied | Source unavailable variant |
| Conflicting state | If discovered and not added, prioritize Add to library over playback |
| Action fails | This book is in your library, but its source cannot stream right now |
| Session expired | Route to Provider Authorization or Source Repair when relevant |
---

## Now Playing - PG09

**Story:** leo-resumes-current-book.md; leo-starts-selected-book.md; leo-sees-playback-source-failure.md | **Flow:** leo-resumes-current-book.md; leo-starts-selected-book.md; leo-sees-playback-source-failure.md | **Actor:** Leo the Living Room Listener; Playback Engine | **State:** Playing

### Purpose
Control audiobook playback and preserve progress.

### Current state displayed
- Object shown: Current playback session
- Status: Playing
- What happened: Resume from Home, Start from Book Detail, or media session return.
- What is pending: buffering, playing, paused, playback_error
- What needs attention: Playback interrupted

### Primary decision
- Decision: Control or recover playback
- Options: Play/Pause; Skip back 15 seconds; Skip forward 30 seconds; Change speed; Retry playback; Repair source
- Information required: Current book/chapter; playback position; playback state; source health
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Skip back 15 seconds | Seek backward | Playback ready or paused |
| Skip forward 30 seconds | Seek forward | Playback ready or paused |
| Repair source | Open Source Repair | Playback source failure |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Play/Pause | Primary | Playable book loaded | Toggle playback | playing / paused | Now Playing |
| Change speed | Secondary | Playback loaded | Adjust speed | playing | Now Playing |
| Retry playback | Secondary | Playback error | Resolve asset again | buffering | Now Playing |
| Repair source | Secondary | Playback source failure | Open Source Repair | source_unavailable | Source Repair |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | Do not show player without selected book; route Home/Library |
| Permission denied | Auth/credential errors route repair |
| Conflicting state | Persist saved position before showing error |
| Action fails | The app saved your position, but this source cannot stream right now |
| Session expired | Route to Provider Authorization or Source Repair when relevant |
---

## Source Repair - PG10

**Story:** leo-retries-failed-source.md; sam-validates-smb-connection.md; clara-authorizes-cloud-provider.md | **Flow:** leo-retries-failed-source.md; sam-validates-smb-connection.md; clara-authorizes-cloud-provider.md | **Actor:** Leo the Living Room Listener; Sam the Server Steward; Clara the Cloud Collector | **State:** Source unavailable

### Purpose
Explain source failures and route to the right recovery action.

### Current state displayed
- Object shown: Failed source
- Status: Source unavailable
- What happened: Home source unavailable, Now Playing playback error, Sync Progress partial/error, Book Detail source unavailable, Library stale source.
- What is pending: source_unavailable, reauthorization_required, credentials_required, repair_complete
- What needs attention: Source unavailable

### Primary decision
- Decision: Choose repair action
- Options: Retry source; Edit SMB credentials; Reauthorize provider; View cached library; Return to playback
- Information required: Source identity; failure category; cached availability; origin route
- Risk if wrong: User loses time, context, or source confidence.
- Reversible: Yes

### Secondary decisions

| Decision | Options | Info required |
| --- | --- | --- |
| Edit SMB credentials | Open SMB Setup repair mode | SMB credentials failed |
| Reauthorize provider | Open Provider Authorization repair mode | Cloud auth failed |
| View cached library | Open Library with cached data | Local metadata readable |

### Available actions

| Action | Priority | Preconditions | Result | Next state | Next screen |
| --- | --- | --- | --- | --- | --- |
| Retry source | Primary | Source unavailable | Check source again | repair_complete / source_unavailable | Origin / Source Repair |
| Edit SMB credentials | Secondary | SMB credentials failed | Open SMB Setup repair mode | credentials_form | SMB Setup |
| Reauthorize provider | Secondary | Cloud auth failed | Open Provider Authorization repair mode | provider_selected | Provider Authorization |
| View cached library | Secondary | Local metadata readable | Open Library with cached data | loaded_grid | Library |

Priority key: Primary / Secondary / Destructive / Disabled / Hidden

### If the user does nothing

The current state remains visible. Loading/active states continue only if a worker, authorization, or playback operation is already running.

### Edge cases

| Scenario | Behaviour |
| --- | --- |
| Missing data | If source missing, return to Sources/Add source |
| Permission denied | Auth/credential repair route specific to source type |
| Conflicting state | Preserve origin route and failed book context |
| Action fails | The app can still show cached books, but this source cannot be reached right now |
| Session expired | Route to Provider Authorization or Source Repair when relevant |
