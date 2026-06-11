> Provisional: updated after story-splitting pass. Review before treating as authoritative.

# Sitemap

> File: docs/ux-ui/screens/sitemap.md
> Canonical screens only. State variants are not separate nodes.

## Entry points

- Home - app launch and Android TV dashboard return.
- Sources - Add source from Home or Library.
- Discovered Books - Sync completion/partial results, or Library empty state.
- Library - curated listening-library browsing.
- Now Playing - Resume/start or media session return.
- Source Repair - source or playback failure.

## Screen connections

| From | Trigger | To | Resulting state | Return / back behaviour | Notes |
| --- | --- | --- | --- | --- | --- |
| App launch | Open app | Home | resume_available / no_source / source_unavailable | N/A | Reads cached current book |
| Home | Resume | Now Playing | buffering then playing | Back returns Home; audio may continue | Resume current book |
| Home | Browse library | Library | loaded_grid / empty_library | Back returns Home | Curated listening library |
| Home/Library | Add source | Sources | default_providers | Back returns origin | Source setup entry |
| Sources | Select SMB | SMB Setup | credentials_form | Back returns Sources | Choose SMB source story |
| Sources | Select cloud provider | Provider Authorization | provider_selected | Back returns Sources | Choose provider story |
| SMB Setup | Validation success | Folder Picker | folder_browsing | Back returns SMB Setup | Validate SMB story |
| Provider Authorization | Auth success | Folder Picker | folder_browsing | Back returns Provider Authorization | Authorize provider story |
| Folder Picker | Select this folder | Sync Progress | queued/indexing | Back returns Folder Picker or runs in background | Folder selection stories |
| Sync Progress | Review discovered books | Discovered Books | discovered_list / partial_results / empty_discovered | Back returns Sync Progress | Discovery review after indexing |
| Discovered Books | Open details | Book Detail | discovered_not_added / added | Back returns same discovered item | Review discovered book |
| Discovered Books | Add to library | Discovered Books | added_state | Focus remains on item | Add single book |
| Discovered Books | View library | Library | loaded_grid | Back returns Discovered Books | Curated library |
| Library | Select book | Book Detail | ready/source_unavailable/no_chapters | Back restores Library focus | Review book detail |
| Book Detail | Resume / Start / Select chapter | Now Playing | buffering then playing | Back returns Book Detail; audio may continue | Start selected book |
| Now Playing | Playback failure | Now Playing | playback_error | N/A | See playback source failure |
| Now Playing | Repair source | Source Repair | source_unavailable / reauthorization_required / credentials_required | Back returns Now Playing error | Retry failed source |
| Source Repair | Retry success | Origin | repair_complete then origin | Return to origin | Origin preserved |

## Flow continuity notes

- Setup no longer jumps directly from sync to Library; sync results go to Discovered Books for review/add.
- Library represents the listening library.
- Discovered Books is the curation step between indexing and listening.
