> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Journey: Clara connects cloud library

> File: docs/ux-ui/journeys/clara-connects-cloud-library.md
> Primary actor: Clara the Cloud Collector
> Real-world trigger: Clara wants to connect audiobooks stored in a first-class cloud provider.
> Starting context: Clara wants to connect audiobooks stored in a first-class cloud provider.
> Resolved end state: Cloud books are discovered and ready for review.

## Stages

### Stage 1: Choosing provider
Named providers should not be hidden behind generic WebDAV. Clara can choose the provider she recognizes.

**Data needed:** Provider list, connected status, provider availability.
**Friction risk:** Offline state explains auth requires internet.

### Stage 2: Authorizing account
Provider auth can time out or authorize the wrong account. Provider-specific auth keeps cloud setup understandable from the TV.

**Data needed:** Provider identity, auth state, account label, permission status.
**Friction risk:** No token or raw provider URL appears.

### Stage 3: Selecting provider folder
Provider permissions and capabilities can block folder access or streaming. Folder choice happens with provider-specific status before indexing.

**Data needed:** Provider folder list, selected path, capability model, permission state.
**Friction risk:** Back returns to Provider Authorization with context.

### Stage 4: Indexing cloud library
Cloud providers may rate-limit, skip files, or restrict folder access. Cloud metadata becomes locally discoverable without blocking browsing.

**Data needed:** Provider source, folder, book/track counts, skipped files, auth/rate status.
**Friction risk:** Auth failures route to Source Repair.

### Stage 5: Indexing cloud library
Cloud folders can include unrelated audio, duplicates, or unsupported files. Clara can curate discovered books instead of polluting the listener's library.

**Data needed:** Discovered book list, provider, support/duplicate status, added status.
**Friction risk:** Already-added books are marked.

## Moments that matter

- **Story boundaries:** Each stage maps to a smaller story rather than one epic flow.
- **Context preservation:** Back, repair, and add-to-library actions preserve the selected source, book, focused card, or playback position.
- **Discovery versus library:** Discovered books are not assumed to be in the listening library until an add action succeeds.

## Story opportunities

| Stage | Story candidate | Why it matters |
| --- | --- | --- |
| Choosing provider | clara-chooses-cloud-provider.md | Clara can choose the provider she recognizes. |
| Authorizing account | clara-authorizes-cloud-provider.md | Provider-specific auth keeps cloud setup understandable from the TV. |
| Selecting provider folder | clara-selects-cloud-library-folder.md | Folder choice happens with provider-specific status before indexing. |
| Indexing cloud library | sync-worker-indexes-cloud-source.md | Cloud metadata becomes locally discoverable without blocking browsing. |
| Indexing cloud library | clara-reviews-discovered-cloud-books.md | Clara can curate discovered books instead of polluting the listener's library. |

## Screens implied

| Stage | Screen needed |
| --- | --- |
| Choosing provider | Sources, Provider Authorization, Folder Picker, Sync Progress, Discovered Books |
| Authorizing account | Sources, Provider Authorization, Folder Picker, Sync Progress, Discovered Books |
| Selecting provider folder | Sources, Provider Authorization, Folder Picker, Sync Progress, Discovered Books |
| Indexing cloud library | Sources, Provider Authorization, Folder Picker, Sync Progress, Discovered Books |
| Indexing cloud library | Sources, Provider Authorization, Folder Picker, Sync Progress, Discovered Books |

## Stories and flows that implement this journey

| Story file | Flow file |
| --- | --- |
| clara-chooses-cloud-provider.md | clara-chooses-cloud-provider.md |
| clara-authorizes-cloud-provider.md | clara-authorizes-cloud-provider.md |
| clara-selects-cloud-library-folder.md | clara-selects-cloud-library-folder.md |
| sync-worker-indexes-cloud-source.md | sync-worker-indexes-cloud-source.md |
| clara-reviews-discovered-cloud-books.md | clara-reviews-discovered-cloud-books.md |
