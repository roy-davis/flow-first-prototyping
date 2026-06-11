> Provisional: updated after story-splitting pass. Review before treating as authoritative.

# Screen Inventory

> File: docs/ux-ui/screens/inventory.md

Total: 11 | In scope: 11 | Out of scope: 0

## Screen list

| ID | Name | Type | Priority | Scope | File | Story | Flow | Actor | State |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PG01 | Home | Dashboard | Must-have | In | docs/ux-ui/screens/home.md | leo-resumes-current-book.md | leo-resumes-current-book.md | Leo the Living Room Listener | Resume available |
| PG02 | Sources | Settings | Must-have | In | docs/ux-ui/screens/sources.md | sam-chooses-smb-source.md; clara-chooses-cloud-provider.md | sam-chooses-smb-source.md; clara-chooses-cloud-provider.md | Sam the Server Steward; Clara the Cloud Collector | Default providers |
| PG03 | SMB Setup | Form | Must-have | In | docs/ux-ui/screens/smb-setup.md | sam-validates-smb-connection.md | sam-validates-smb-connection.md | Sam the Server Steward | Credentials form |
| PG04 | Provider Authorization | Auth | Must-have | In | docs/ux-ui/screens/provider-authorization.md | clara-authorizes-cloud-provider.md | clara-authorizes-cloud-provider.md | Clara the Cloud Collector | Provider selected |
| PG05 | Folder Picker | List | Must-have | In | docs/ux-ui/screens/folder-picker.md | sam-selects-smb-library-folder.md; clara-selects-cloud-library-folder.md | sam-selects-smb-library-folder.md; clara-selects-cloud-library-folder.md | Sam the Server Steward; Clara the Cloud Collector | Folder browsing |
| PG06 | Sync Progress | Dashboard | Must-have | In | docs/ux-ui/screens/sync-progress.md | sync-worker-indexes-smb-source.md; sync-worker-indexes-cloud-source.md | sync-worker-indexes-smb-source.md; sync-worker-indexes-cloud-source.md | Sync Worker; Sam the Server Steward; Clara the Cloud Collector | Indexing |
| PG11 | Discovered Books | List | Must-have | In | docs/ux-ui/screens/discovered-books.md | sam-reviews-discovered-smb-books.md; clara-reviews-discovered-cloud-books.md; leo-reviews-discovered-book.md; leo-adds-book-to-listening-library.md | sam-reviews-discovered-smb-books.md; clara-reviews-discovered-cloud-books.md; leo-reviews-discovered-book.md; leo-adds-book-to-listening-library.md | Leo the Living Room Listener; Sam the Server Steward; Clara the Cloud Collector | Discovered list |
| PG07 | Library | List | Must-have | In | docs/ux-ui/screens/library.md | leo-scans-cached-library.md; leo-adds-book-to-listening-library.md | leo-scans-cached-library.md; leo-adds-book-to-listening-library.md | Leo the Living Room Listener | Loaded grid |
| PG08 | Book Detail | Detail | Must-have | In | docs/ux-ui/screens/book-detail.md | leo-reviews-book-detail.md; leo-reviews-discovered-book.md; leo-starts-selected-book.md | leo-reviews-book-detail.md; leo-reviews-discovered-book.md; leo-starts-selected-book.md | Leo the Living Room Listener | Ready |
| PG09 | Now Playing | Detail | Must-have | In | docs/ux-ui/screens/now-playing.md | leo-resumes-current-book.md; leo-starts-selected-book.md; leo-sees-playback-source-failure.md | leo-resumes-current-book.md; leo-starts-selected-book.md; leo-sees-playback-source-failure.md | Leo the Living Room Listener; Playback Engine | Playing |
| PG10 | Source Repair | Error | Must-have | In | docs/ux-ui/screens/source-repair.md | leo-retries-failed-source.md; sam-validates-smb-connection.md; clara-authorizes-cloud-provider.md | leo-retries-failed-source.md; sam-validates-smb-connection.md; clara-authorizes-cloud-provider.md | Leo the Living Room Listener; Sam the Server Steward; Clara the Cloud Collector | Source unavailable |

## Scope note

PG11 Discovered Books was added by the story-sizing pass to represent discovery and explicit add-to-listening-library behavior. Library is now the curated listening library, not every indexed item.
