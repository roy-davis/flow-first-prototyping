> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story Overview

> File: docs/ux-ui/stories/overview.md

| Story file | Story name | Primary actor | Journey file | Journey stage | Flow file(s) | Priority |
| --- | --- | --- | --- | --- | --- | --- |
| leo-resumes-current-book.md | Resume current book | Leo the Living Room Listener | leo-resumes-current-book.md | Checking resume context | leo-resumes-current-book.md | Must-have |
| leo-scans-cached-library.md | Scan cached library | Leo the Living Room Listener | leo-browses-and-starts-book.md | Scanning the library | leo-scans-cached-library.md | Must-have |
| leo-reviews-book-detail.md | Review book detail | Leo the Living Room Listener | leo-browses-and-starts-book.md | Confirming a book | leo-reviews-book-detail.md | Must-have |
| leo-starts-selected-book.md | Start selected book | Leo the Living Room Listener | leo-browses-and-starts-book.md | Starting selected playback | leo-starts-selected-book.md | Must-have |
| leo-sees-playback-source-failure.md | See playback source failure | Leo the Living Room Listener | leo-recovers-from-source-dropout.md | Playback interruption | leo-sees-playback-source-failure.md | Must-have |
| leo-retries-failed-source.md | Retry failed source | Leo the Living Room Listener | leo-recovers-from-source-dropout.md | Diagnosing source health | leo-retries-failed-source.md | Should-have |
| sam-chooses-smb-source.md | Choose SMB source | Sam the Server Steward | sam-connects-smb-library.md | Preparing source details | sam-chooses-smb-source.md | Must-have |
| sam-validates-smb-connection.md | Validate SMB connection | Sam the Server Steward | sam-connects-smb-library.md | Validating SMB connection | sam-validates-smb-connection.md | Must-have |
| sam-selects-smb-library-folder.md | Select SMB library folder | Sam the Server Steward | sam-connects-smb-library.md | Choosing library folder | sam-selects-smb-library-folder.md | Must-have |
| sync-worker-indexes-smb-source.md | Index SMB source | Sync Worker | sam-connects-smb-library.md | Indexing and handoff | sync-worker-indexes-smb-source.md | Must-have |
| sam-reviews-discovered-smb-books.md | Review discovered SMB books | Sam the Server Steward | sam-connects-smb-library.md | Indexing and handoff | sam-reviews-discovered-smb-books.md | Should-have |
| clara-chooses-cloud-provider.md | Choose cloud provider | Clara the Cloud Collector | clara-connects-cloud-library.md | Choosing provider | clara-chooses-cloud-provider.md | Must-have |
| clara-authorizes-cloud-provider.md | Authorize cloud provider | Clara the Cloud Collector | clara-connects-cloud-library.md | Authorizing account | clara-authorizes-cloud-provider.md | Must-have |
| clara-selects-cloud-library-folder.md | Select cloud library folder | Clara the Cloud Collector | clara-connects-cloud-library.md | Selecting provider folder | clara-selects-cloud-library-folder.md | Must-have |
| sync-worker-indexes-cloud-source.md | Index cloud source | Sync Worker | clara-connects-cloud-library.md | Indexing cloud library | sync-worker-indexes-cloud-source.md | Must-have |
| clara-reviews-discovered-cloud-books.md | Review discovered cloud books | Clara the Cloud Collector | clara-connects-cloud-library.md | Indexing cloud library | clara-reviews-discovered-cloud-books.md | Should-have |
| leo-reviews-discovered-book.md | Review discovered book | Leo the Living Room Listener | leo-discovers-and-adds-book.md | Inspecting a discovered book | leo-reviews-discovered-book.md | Should-have |
| leo-adds-book-to-listening-library.md | Add book to listening library | Leo the Living Room Listener | leo-discovers-and-adds-book.md | Adding to listening library | leo-adds-book-to-listening-library.md | Must-have |
