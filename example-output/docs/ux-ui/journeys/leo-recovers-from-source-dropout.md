> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Journey: Leo recovers from source dropout

> File: docs/ux-ui/journeys/leo-recovers-from-source-dropout.md
> Primary actor: Leo the Living Room Listener
> Real-world trigger: Playback stalls or fails because a source cannot stream.
> Starting context: Playback stalls or fails because a source cannot stream.
> Resolved end state: Leo retries or enters source-specific repair with position preserved.

## Stages

### Stage 1: Playback interruption
Source failures can look like player bugs and can threaten audiobook progress. A specific playback error keeps trust in progress persistence.

**Data needed:** Playback state, saved position, source identity, failure category.
**Friction risk:** No raw URL, token, file ID, or stack trace appears.

### Stage 2: Diagnosing source health
Some failures are brief network dropouts and should not force full setup. Retry is the smallest safe recovery action.

**Data needed:** Source type, failure category, last sync, cached availability, origin route.
**Friction risk:** Credential/auth repair is shown only when diagnosis requires it.

## Moments that matter

- **Story boundaries:** Each stage maps to a smaller story rather than one epic flow.
- **Context preservation:** Back, repair, and add-to-library actions preserve the selected source, book, focused card, or playback position.
- **Discovery versus library:** Discovered books are not assumed to be in the listening library until an add action succeeds.

## Story opportunities

| Stage | Story candidate | Why it matters |
| --- | --- | --- |
| Playback interruption | leo-sees-playback-source-failure.md | A specific playback error keeps trust in progress persistence. |
| Diagnosing source health | leo-retries-failed-source.md | Retry is the smallest safe recovery action. |

## Screens implied

| Stage | Screen needed |
| --- | --- |
| Playback interruption | Now Playing, Source Repair |
| Diagnosing source health | Home, Library |

## Stories and flows that implement this journey

| Story file | Flow file |
| --- | --- |
| leo-sees-playback-source-failure.md | leo-sees-playback-source-failure.md |
| leo-retries-failed-source.md | leo-retries-failed-source.md |
