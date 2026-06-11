> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Journey: Leo discovers and adds book

> File: docs/ux-ui/journeys/leo-discovers-and-adds-book.md
> Primary actor: Leo the Living Room Listener
> Real-world trigger: New audiobooks have been discovered from a synced source.
> Starting context: New audiobooks have been discovered from a synced source.
> Resolved end state: One discovered book is added to the listening library.

## Stages

### Stage 1: Inspecting a discovered book
A discovered folder may not be a book Leo wants in his listening library. Leo can decide with title, author, chapters, source, and support status visible.

**Data needed:** Discovered book metadata, chapters, source, support status, added status.
**Friction risk:** Back returns to the same discovered item.

### Stage 2: Adding to listening library
Discovery alone does not explain how a book becomes part of Leo's listening library. The product gains an explicit curation step between indexed catalog and listening library.

**Data needed:** Discovered book, listening library item, added status, source health.
**Friction risk:** Library shows the newly added book.

## Moments that matter

- **Story boundaries:** Each stage maps to a smaller story rather than one epic flow.
- **Context preservation:** Back, repair, and add-to-library actions preserve the selected source, book, focused card, or playback position.
- **Discovery versus library:** Discovered books are not assumed to be in the listening library until an add action succeeds.

## Story opportunities

| Stage | Story candidate | Why it matters |
| --- | --- | --- |
| Inspecting a discovered book | leo-reviews-discovered-book.md | Leo can decide with title, author, chapters, source, and support status visible. |
| Adding to listening library | leo-adds-book-to-listening-library.md | The product gains an explicit curation step between indexed catalog and listening library. |

## Screens implied

| Stage | Screen needed |
| --- | --- |
| Inspecting a discovered book | Discovered Books, Book Detail, Library |
| Adding to listening library | Discovered Books, Book Detail, Library |

## Stories and flows that implement this journey

| Story file | Flow file |
| --- | --- |
| leo-reviews-discovered-book.md | leo-reviews-discovered-book.md |
| leo-adds-book-to-listening-library.md | leo-adds-book-to-listening-library.md |
