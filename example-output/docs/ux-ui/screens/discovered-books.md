> Provisional: regenerated after updating flow-first-prototyping Story Sizing Rules. Review before treating as authoritative.

# Discovered Books

> File: docs/ux-ui/screens/discovered-books.md
> Screen ID: PG11

| Attribute | Value |
|---|---|
| Route | /discovered |
| Access | Listener / source owner |
| Mobile | Not required |
| TV | Critical |
| Scope | In scope |

### Design intent

- Primary purpose: Review audiobooks discovered by sync and add selected books to the listening library.
- Primary actors: Leo the Living Room Listener; Sam the Server Steward; Clara the Cloud Collector; Sync Worker.
- Primary job: Decide whether a discovered book belongs in the listening library.
- Principle served: Cache first, never wait on folders.
- Entry points: Sync Progress complete/partial; Library empty Add discovered books.
- Success outcome: A selected discovered book is added to Library or clearly skipped/blocked.
- Content priority: Primary: discovered book list, source, support status, Add to library. Secondary: skipped/unsupported warnings.
- Critical variants: discovered list, partial results, empty discovered, added state, unsupported blocked.
- User state of mind: Reviewing what the app found and deciding what belongs in the listening library.
- Usage context: Android TV, D-pad remote, large lists, possible partial sync.
- Data range: zero discovered books, typical 12 books, maximum 500+ books, duplicates, unsupported files, long titles.
- Anti-goals: Do not imply every indexed file is already in the listening library; do not show raw paths as primary labels.
- Fidelity target: Mid-fi
- Exit paths: Library, Book Detail, Sync Progress, Source Repair.

### Related flows

- sam-reviews-discovered-smb-books.md: Reviews discovered SMB books.
- clara-reviews-discovered-cloud-books.md: Reviews discovered cloud books.
- leo-reviews-discovered-book.md: Opens a discovered book for detail.
- leo-adds-book-to-listening-library.md: Adds a discovered book to Library.

### Related stories

- sam-reviews-discovered-smb-books.md
- clara-reviews-discovered-cloud-books.md
- leo-reviews-discovered-book.md
- leo-adds-book-to-listening-library.md

### Decisions on this screen

| ID | Decision | Stakes | Reversible |
|---|---|---|---|
| D1 | Add a discovered book to the listening library | Medium | Yes |

### States

| State | Description | Transitions |
|---|---|---|
| discovered_list | Supported discovered books visible | Add -> added_state; Open -> Book Detail |
| partial_results | Some books discovered and some skipped | Review warning or add supported books |
| empty_discovered | Sync found no supported books | Choose another folder or Add source |
| added_state | Focused book already in Library | Open Library or keep browsing discovered |
| unsupported_blocked | Focused item cannot be added | Show reason and recovery |

### Actions

| Action | Description | Precondition |
|---|---|---|
| Add to library | Add focused discovered book to listening library | Supported and not already added |
| Open details | Review discovered book detail | Discovered book exists |
| View library | Open listening library | At least one added book |
| Review source issue | Open Source Repair or sync warning | Partial or blocked result |
| Choose another folder | Return to Folder Picker | No discovered books or wrong folder |

### In-flow contextual actions

| Moment / object | User intent | Trigger / affordance | Result | Preserve / return behaviour | When not available |
|---|---|---|---|---|---|
| Focused discovered book | Add to listening library | Row/card action | Creates listening library item | Return to same focused row with Added badge | Unsupported or already added |

### Transition contract

| From | Trigger | To | Resulting state | Back / exit behaviour | Blocked / error behaviour |
|---|---|---|---|---|---|
| Sync Progress | Review discovered books | Discovered Books | discovered_list / partial_results / empty_discovered | Back returns Sync Progress | Source failure routes Source Repair |
| Discovered Books | Add to library | Discovered Books | added_state | Focus remains on added item | Duplicate add shows already added |
| Discovered Books | Open details | Book Detail | discovered_not_added / added | Back returns same discovered item | Unsupported book shows blocked detail |
| Discovered Books | View library | Library | loaded_grid | Back returns Discovered Books | Disabled when no added books |

### Interaction states

| Element or action | Default | Focus | Pressed / active | Disabled | Loading | Success feedback | Error feedback / recovery |
|---|---|---|---|---|---|---|---|
| Add to library | Row/card action | Scale and focus ring | Adds selected book | Disabled if unsupported/already added | Adding... | Added badge | Reason and retry/source repair |
| Open details | Secondary action | Focus ring | Opens detail | Disabled if no item | N/A | Detail opens | N/A |

### Data required

| Data | Source | Offline | Notes |
|---|---|---|---|
| Discovered book list | Local metadata cache | Cached | Generated by sync |
| Added status | Local metadata cache | Cached | Prevent duplicate add |
| Support status | Sync Worker | Cached | Unsupported, duplicate, partial |
| Source status | Local DB / Provider | Cached / Real-time | Repair if source blocked |

### Screen robustness

| Concern | Requirement |
|---|---|
| Empty / zero data | Empty discovered state with Choose another folder / Add source |
| Typical data | 12 discovered books |
| Maximum / dense data | 500+ discovered books with stable focused row/card |
| Long text / overflow | Titles and source names wrap/truncate safely |
| Loading / slow response | Add action has row-level loading |
| Offline / degraded connection | Cached discovered results remain visible |
| Permission / restricted access | Blocked items show reason and repair |
| Duplicate or concurrent action | Already-added state disables Add |
| Responsive / safe area | TV safe margins |
| Keyboard / focus | D-pad focus returns to same row |

### Visual indicators

| Indicator | Meaning |
|---|---|
| Added badge | Already in listening library |
| Unsupported badge | Cannot be added/played |
| Warning badge | Partial sync or source issue |

### Critical variants

**Discovered list**
Shows supported discovered books with Add to library.

**Partial results**
Shows discovered books plus warning about skipped/unsupported items.

**Empty discovered**
Explains no supported books were found and offers folder/source recovery.

**Added state**
Focused book shows Added and cannot be added twice.

### Layout regions

| Region | Purpose | Required content |
|---|---|---|
| Header | Source/discovery context | Source, sync result, count |
| Discovered list | Review books | Rows/cards with title, author, status |
| Action area | Add/recover | Add to library, View library, Review issue |

### Content

| Element | Copy |
|---|---|
| Page title | Discovered books |
| Primary action label | Add to library |
| Empty state heading | No audiobooks discovered |
| Empty state body | Choose another folder or source to find supported audiobooks. |
| Empty state CTA | Choose another folder |
| Error heading | Some books need attention |
| Error body | Some discovered items could not be added or played. |
| Offline message | Showing discovered books from the local cache. |
| Success message | Added to listening library. |

### Screen generation prompt

> Target tool: Other

Design an Android TV Discovered Books screen where a listener or source owner reviews audiobooks found by sync and adds selected books to the listening library. Make the distinction between discovered and added explicit, show source/sync status, support/duplicate badges, and row-level Add to library behavior. Render discovered list, partial results, empty discovered, added, and unsupported states with D-pad focus and no raw source paths as primary labels.

### Acceptance criteria

- [ ] A user can tell discovered books are not automatically in the listening library.
- [ ] Add to library is disabled for unsupported or already-added books.
- [ ] Partial sync results still allow supported books to be added.
- [ ] Empty discovered state has a clear folder/source recovery path.
- [ ] Focus returns to the same discovered item after add or detail review.
