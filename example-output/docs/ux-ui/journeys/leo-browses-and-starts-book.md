> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Journey: Leo browses and starts book

> File: docs/ux-ui/journeys/leo-browses-and-starts-book.md
> Primary actor: Leo the Living Room Listener
> Real-world trigger: Leo wants a different audiobook or has no current book.
> Starting context: Leo wants a different audiobook or has no current book.
> Resolved end state: Leo reaches a selected book or playback start path.

## Stages

### Stage 1: Scanning the library
Remote folder browsing is too slow and hard to control from a TV remote. A cache-first library feels local even when files live on SMB or cloud.

**Data needed:** Listening library book list, title, author, progress, source badge, artwork fallback.
**Friction risk:** Large libraries preserve focus and scroll position.

### Stage 2: Confirming a book
A card alone does not show enough context to choose a chapter or trust source availability. Book Detail lets Leo confirm the book before playback starts.

**Data needed:** Book metadata, chapter list, progress, source health.
**Friction risk:** Back returns to the same focused Library card.

### Stage 3: Starting selected playback
Playback can fail after cached metadata looked ready. The start transition proves cache-backed browsing still leads to reliable streaming.

**Data needed:** Selected book, selected chapter, playable asset reference, saved position, source status.
**Friction risk:** Source failure routes to Source Repair with origin preserved.

## Moments that matter

- **Story boundaries:** Each stage maps to a smaller story rather than one epic flow.
- **Context preservation:** Back, repair, and add-to-library actions preserve the selected source, book, focused card, or playback position.
- **Discovery versus library:** Discovered books are not assumed to be in the listening library until an add action succeeds.

## Story opportunities

| Stage | Story candidate | Why it matters |
| --- | --- | --- |
| Scanning the library | leo-scans-cached-library.md | A cache-first library feels local even when files live on SMB or cloud. |
| Confirming a book | leo-reviews-book-detail.md | Book Detail lets Leo confirm the book before playback starts. |
| Starting selected playback | leo-starts-selected-book.md | The start transition proves cache-backed browsing still leads to reliable streaming. |

## Screens implied

| Stage | Screen needed |
| --- | --- |
| Scanning the library | Home, Library |
| Confirming a book | Book Detail |
| Starting selected playback | Book Detail, Now Playing |

## Stories and flows that implement this journey

| Story file | Flow file |
| --- | --- |
| leo-scans-cached-library.md | leo-scans-cached-library.md |
| leo-reviews-book-detail.md | leo-reviews-book-detail.md |
| leo-starts-selected-book.md | leo-starts-selected-book.md |
