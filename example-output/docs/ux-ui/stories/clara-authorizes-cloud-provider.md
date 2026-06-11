> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Story: Authorize cloud provider

> File: docs/ux-ui/stories/clara-authorizes-cloud-provider.md
> Primary actor: Clara the Cloud Collector
> Journey: clara-connects-cloud-library.md
> Journey stage: Authorizing account
> Priority: Must-have

- Task slice: Authorize the selected cloud provider account.
- Real-world trigger: Clara selects a first-class provider.
- Problem: Provider auth can time out or authorize the wrong account.
- Story statement: As Clara the Cloud Collector, I want to authorize the selected cloud provider account, so I can make progress without losing audiobook or source context.
- Value: Provider-specific auth keeps cloud setup understandable from the TV.
- Outcome: The provider is authorized or Clara gets a retry/cancel path.
- Preconditions: Relevant source, cache, selection, or playback context exists.
- Acceptance criteria:
  - Selected provider is visible.
  - Pending/success/error states are distinct.
  - Cancel and Retry are available.
  - No token or raw provider URL appears.
- Data needed: Provider identity, auth state, account label, permission status.
- In-flow intent opportunities: Keep the action contextual to the focused source, book, chapter, playback state, or discovered item and preserve return context.
- Edge cases: Empty data, stale source, unavailable permissions, duplicate action, long text, and slow loading/error states must be represented where applicable.
- Flow files: clara-authorizes-cloud-provider.md
