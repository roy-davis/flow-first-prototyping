> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Journey: Leo resumes current book

> File: docs/ux-ui/journeys/leo-resumes-current-book.md
> Primary actor: Leo the Living Room Listener
> Real-world trigger: Leo returns to the TV after an interrupted listening session.
> Starting context: Leo returns to the TV after an interrupted listening session.
> Resolved end state: Playback resumes at the saved millisecond.

## Stages

### Stage 1: Checking resume context
Long-form progress is hard to recover if the app loses context or blocks on source health. The fastest path proves the app is built for audiobooks.

**Data needed:** Current book, chapter, saved millisecond, source health, playable asset reference.
**Friction risk:** Source failure preserves progress and routes to repair.

## Moments that matter

- **Story boundaries:** Each stage maps to a smaller story rather than one epic flow.
- **Context preservation:** Back, repair, and add-to-library actions preserve the selected source, book, focused card, or playback position.
- **Discovery versus library:** Discovered books are not assumed to be in the listening library until an add action succeeds.

## Story opportunities

| Stage | Story candidate | Why it matters |
| --- | --- | --- |
| Checking resume context | leo-resumes-current-book.md | The fastest path proves the app is built for audiobooks. |

## Screens implied

| Stage | Screen needed |
| --- | --- |
| Checking resume context | Home, Library |

## Stories and flows that implement this journey

| Story file | Flow file |
| --- | --- |
| leo-resumes-current-book.md | leo-resumes-current-book.md |
