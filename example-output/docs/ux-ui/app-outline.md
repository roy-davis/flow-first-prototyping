> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# App Outline

> File: docs/ux-ui/app-outline.md
> Purpose: early app-shape sanity check before flows and screen inventory
> Status: rough, non-final; screen inventory is the committed source later

## App shape summary

The product now separates three concepts that were previously blurred: discovered catalog items, curated listening-library items, and playable book sessions. Source setup discovers audiobooks from SMB/cloud folders; Discovered Books lets a human review what was found; Library shows books that have been added to the listening library.

## Likely top-level areas

| Area / surface | Purpose | Primary actors | Stories supported | Notes |
| --- | --- | --- | --- | --- |
| Home | Fast resume and entry into Library/Sources | Leo | leo-resumes-current-book.md | Resume-first |
| Library | Browse curated listening-library books | Leo | leo-scans-cached-library.md | Not all discovered books appear here |
| Discovered Books | Review indexed books and add selected items | Leo, Sam, Clara | sam-reviews-discovered-smb-books.md; clara-reviews-discovered-cloud-books.md; leo-reviews-discovered-book.md; leo-adds-book-to-listening-library.md | New surface added by story split |
| Book Detail | Review a selected library or discovered book | Leo | leo-reviews-book-detail.md; leo-reviews-discovered-book.md | Has added/not-added states |
| Now Playing | Playback and progress | Leo | leo-starts-selected-book.md; leo-resumes-current-book.md | Playback source failures route to repair |
| Source setup | Choose, validate/auth, select folder, sync | Sam, Clara, Sync Worker | setup split stories | Linear branch |
| Source Repair | Retry or route to source-specific repair | Leo, Sam, Clara | leo-sees-playback-source-failure.md; leo-retries-failed-source.md | Preserves origin |

## Rough screen candidates

| Candidate screen | Why it might exist | Supporting stories | Confidence | Notes |
| --- | --- | --- | --- | --- |
| Home | Resume current book | leo-resumes-current-book.md | High | Existing |
| Sources | Choose source type | sam-chooses-smb-source.md; clara-chooses-cloud-provider.md | High | Existing |
| SMB Setup | Validate SMB credentials | sam-validates-smb-connection.md | High | Existing |
| Provider Authorization | Authorize cloud account | clara-authorizes-cloud-provider.md | High | Existing |
| Folder Picker | Select source folder | sam-selects-smb-library-folder.md; clara-selects-cloud-library-folder.md | High | Existing |
| Sync Progress | Index selected folder | sync-worker-indexes-smb-source.md; sync-worker-indexes-cloud-source.md | High | Existing |
| Discovered Books | Review indexed books and add to listening library | review/add discovered stories | High | New |
| Library | Browse curated listening library | leo-scans-cached-library.md | High | Existing meaning refined |
| Book Detail | Review library/discovered book | leo-reviews-book-detail.md; leo-reviews-discovered-book.md | High | Existing state expanded |
| Now Playing | Playback | leo-starts-selected-book.md | High | Existing |
| Source Repair | Recover source failure | leo-retries-failed-source.md | High | Existing |

## Story coverage by surface

| Story | Likely area / surface | Needs new surface? | Notes |
| --- | --- | --- | --- |
| leo-resumes-current-book.md | Home / Library / Book Detail / Now Playing | No | Resume current book |
| leo-scans-cached-library.md | Home / Library / Book Detail / Now Playing | No | Scan cached library |
| leo-reviews-book-detail.md | Home / Library / Book Detail / Now Playing | No | Review book detail |
| leo-starts-selected-book.md | Home / Library / Book Detail / Now Playing | No | Start selected book |
| leo-sees-playback-source-failure.md | Now Playing / Source Repair | No | See playback source failure |
| leo-retries-failed-source.md | Now Playing / Source Repair | No | Retry failed source |
| sam-chooses-smb-source.md | Sources / SMB Setup / Folder Picker / Sync Progress | No | Choose SMB source |
| sam-validates-smb-connection.md | Sources / SMB Setup / Folder Picker / Sync Progress | No | Validate SMB connection |
| sam-selects-smb-library-folder.md | Sources / SMB Setup / Folder Picker / Sync Progress | No | Select SMB library folder |
| sync-worker-indexes-smb-source.md | Sources / SMB Setup / Folder Picker / Sync Progress | No | Index SMB source |
| sam-reviews-discovered-smb-books.md | Discovered Books / Book Detail / Library | Yes | Review discovered SMB books |
| clara-chooses-cloud-provider.md | Sources / Provider Authorization / Folder Picker / Sync Progress | No | Choose cloud provider |
| clara-authorizes-cloud-provider.md | Sources / Provider Authorization / Folder Picker / Sync Progress | No | Authorize cloud provider |
| clara-selects-cloud-library-folder.md | Sources / Provider Authorization / Folder Picker / Sync Progress | No | Select cloud library folder |
| sync-worker-indexes-cloud-source.md | Sources / Provider Authorization / Folder Picker / Sync Progress | No | Index cloud source |
| clara-reviews-discovered-cloud-books.md | Discovered Books / Book Detail / Library | Yes | Review discovered cloud books |
| leo-reviews-discovered-book.md | Discovered Books / Book Detail / Library | Yes | Review discovered book |
| leo-adds-book-to-listening-library.md | Discovered Books / Book Detail / Library | Yes | Add book to listening library |

## Should not become screens

| Candidate / idea | Why not | Better treatment |
| --- | --- | --- |
| All indexed files automatically in Library | The user asked how to discover and add a book; auto-add hides that task | Separate Discovered Books from Library |
| Live remote file browser for normal library browsing | Breaks cache-first performance goal | Use Folder Picker only during setup/repair |
| Separate screen for every setup micro-step | Would over-fragment TV flow | Use states within existing setup screens |

## In-flow action candidates

| Moment / object of attention | Secondary intent | Better treatment | Return behaviour |
| --- | --- | --- | --- |
| Focused discovered book | Add to listening library | Contextual row action or Book Detail primary action | Return to same discovered item with Added state |
| Focused library book | Resume focused book | Contextual row/card action | Return to same focused card |
| Playback error | Repair source | Inline repair action | Return to saved playback position |

## Navigation and entry hypothesis

- Primary entry point: Home.
- Discovery entry point: Sync Progress -> Discovered Books, plus Library empty/add-books affordance.
- Listening entry point: Home -> Library -> Book Detail -> Now Playing.
- Setup entry point: Home/Library -> Sources -> source-specific setup.
- Back/exit behavior: Preserve focused book, discovered item, folder, source, and playback position.

## Structural risks

- Discovered Books creates a new curation concept that must be confirmed: not every indexed book appears in Library until added.
- Bulk add/select all is not specified and may be needed for large libraries.

## Questions before flows and inventory

1. Should every indexed book auto-add to Library, or is Discovered Books the intended curation step? - default if accepted: separate discovered catalog from listening library.
2. Should Discovered Books support bulk add? - default if accepted: single-book add for prototype.
