> Provisional: updated after page-state coverage pass. Review before treating as authoritative.

# Prototype Build Brief

> File: docs/ux-ui/prepare-brief.md
> Self-contained generation brief for v0, Lovable, Bolt, Claude Design, Google Stitch. Use alongside docs/ux-ui/design.md.

## Overview

**Product:** Local & Cloud Network Audiobook Player for Android TV
**Goal:** Connect SMB or first-class cloud audiobook sources, index them into a local cache, browse from the couch, and resume/play with reliable progress and repair.
**Fidelity:** Mid-fi
**Target tool:** Other
**Primary story:** leo-resumes-current-book.md
**Primary flow:** leo-resumes-current-book.md
**Screens:** PG01, PG02, PG03, PG04, PG05, PG06, PG11, PG07, PG08, PG09, PG10

## Design system summary

- Framework: Native Android TV, Jetpack Compose for TV
- Component library + version: androidx.tv:tv-material, version not supplied
- Styling: Compose theme tokens
- Dark mode: Primary
- Navigation: D-pad remote, Home-led drill-downs, linear setup/repair branches
- Primary color: Provisional #3B82F6 for focus and active state
- Border radius: 16dp default
- Font: System TV sans

## Global UI decisions

- Navigation model: Home -> Library/Book Detail/Now Playing; Add source -> Sources -> setup -> Folder Picker -> Sync Progress -> Discovered Books -> Library; source failure -> Source Repair -> origin.
- Primary action hierarchy: One dominant action per state, secondary actions grouped, repair/destructive actions source-specific.
- Focus/input model: D-pad focus is first-class and visible by scale plus border/glow.
- Data freshness: Home, Library, and Book Detail use local metadata cache; remote calls happen in setup, sync, repair, and playback asset resolution.
- Loading/empty/error treatment: Preserve cached content, name source/failure, and give one primary recovery.
- Offline/degraded treatment: Keep cached content visible when safe and disable/repair source-dependent actions.
- Provider/source identity: SMB and named cloud providers are first-class; WebDAV is advanced/custom.
- Layout constraints: 48dp minimum TV safe margin; 64dp preferred; no phone nav.
- Copy conventions: Sentence case, specific verb + object actions, no generic error copy.

## Screens to build

| Order | ID | Name | Spec file | Entry? | Notes |
| --- | --- | --- | --- | --- | --- |
| 1 | PG01 | Home | docs/ux-ui/screens/home.md | Yes | Resume available |
| 2 | PG02 | Sources | docs/ux-ui/screens/sources.md | Yes | Default providers |
| 3 | PG03 | SMB Setup | docs/ux-ui/screens/smb-setup.md | No | Credentials form |
| 4 | PG04 | Provider Authorization | docs/ux-ui/screens/provider-authorization.md | No | Provider selected |
| 5 | PG05 | Folder Picker | docs/ux-ui/screens/folder-picker.md | No | Folder browsing |
| 6 | PG06 | Sync Progress | docs/ux-ui/screens/sync-progress.md | No | Indexing |
| 7 | PG11 | Discovered Books | docs/ux-ui/screens/discovered-books.md | No | Discovered list |
| 8 | PG07 | Library | docs/ux-ui/screens/library.md | Yes | Loaded grid |
| 9 | PG08 | Book Detail | docs/ux-ui/screens/book-detail.md | No | Ready |
| 10 | PG09 | Now Playing | docs/ux-ui/screens/now-playing.md | Yes | Playing |
| 11 | PG10 | Source Repair | docs/ux-ui/screens/source-repair.md | No | Source unavailable |

## Core flow

1. User opens Home and sees Project Hail Mary by Andy Weir at 9:42:18 of 16:10:44.
2. User selects Resume -> Now Playing.
3. Now Playing resolves the playable asset reference, buffers, then plays from the saved position.
4. User can Browse library -> Library -> Book Detail -> Now Playing.
5. User can Add source -> Sources -> SMB Setup or Provider Authorization -> Folder Picker -> Sync Progress -> Discovered Books -> Library.
6. Source failure from Home, Book Detail, Library, Now Playing, or Sync Progress -> Source Repair -> repair branch -> origin.

## Mock data

### Current playback

| Field | Value |
| --- | --- |
| Book title | Project Hail Mary |
| Author | Andy Weir |
| Chapter | Chapter 18 - Petrova Line |
| Position | 9:42:18 |
| Duration | 16:10:44 |
| Speed | 1.25x |
| Source | Family NAS / Audiobooks |
| Source health | Healthy |

### Books

| Title | Author | Progress | Source | Chapters |
| --- | --- | --- | --- | --- |
| Project Hail Mary | Andy Weir | 60% | Family NAS | 32 |
| The Left Hand of Darkness | Ursula K. Le Guin | Not started | Google Drive | 18 |
| The Hobbit | J.R.R. Tolkien | 22% | Dropbox | 19 |
| Dune | Frank Herbert | 8% | OneDrive | 48 |
| The Long Way to a Small Angry Planet | Becky Chambers | Complete | Family NAS | 21 |

### Sources

| Name | Type | Status | Last sync |
| --- | --- | --- | --- |
| Family NAS | SMB | Healthy | 12 minutes ago |
| Cloud Audiobooks | Google Drive | Auth expired | Yesterday |
| Shared Classics | Dropbox | Partial sync | 2 hours ago |

## States to show

| Screen | State | How |
| --- | --- | --- |
| PG01 Home | resume available | Current book exists with saved progress |
| PG01 Home | no source | No source has been configured |
| PG01 Home | source unavailable | Current source cannot be reached |
| PG02 Sources | default providers | SMB and first-class providers are visible |
| PG02 Sources | advanced webdav | WebDAV is revealed under advanced |
| PG03 SMB Setup | credentials form | Fields ready for host/share/credentials |
| PG03 SMB Setup | testing connection | Validation in progress |
| PG03 SMB Setup | connection error | Host/share/auth validation failed |
| PG03 SMB Setup | anonymous login | Anonymous mode selected |
| PG04 Provider Authorization | provider selected | Provider chosen; auth not started |
| PG04 Provider Authorization | auth pending | Device/browser authorization in progress |
| PG04 Provider Authorization | auth success | Provider authorized |
| PG04 Provider Authorization | auth error | Provider rejected or timed out |
| PG05 Folder Picker | folder browsing | Folders visible and navigable |
| PG05 Folder Picker | permission blocked | Selected folder cannot be listed/read |
| PG05 Folder Picker | empty folder | Folder has no supported audiobook files or folders |
| PG06 Sync Progress | queued | Worker queued or waiting for constraints |
| PG06 Sync Progress | indexing | Worker crawling source |
| PG06 Sync Progress | complete | Sync finished successfully |
| PG06 Sync Progress | partial error | Some folders/files failed |
| PG11 Discovered Books | discovered list | Supported discovered books visible |
| PG11 Discovered Books | partial results | Some books discovered and some skipped |
| PG11 Discovered Books | empty discovered | Sync found no supported books |
| PG11 Discovered Books | added state | Focused book already in Library |
| PG11 Discovered Books | unsupported blocked | Focused item cannot be added |
| PG07 Library | loading cache | Local metadata read in progress |
| PG07 Library | loaded grid | Cached books visible |
| PG07 Library | empty library | No supported books indexed |
| PG07 Library | stale source | Cached books visible but source degraded |
| PG08 Book Detail | ready | Book playable or resumable |
| PG08 Book Detail | discovered not added | Book is discovered but not yet in the listening library |
| PG08 Book Detail | added | Book has just been added to the listening library |
| PG08 Book Detail | source unavailable | Metadata cached but source cannot stream |
| PG08 Book Detail | no chapters | Book has no playable chapters indexed |
| PG09 Now Playing | buffering | Resolving asset or filling buffer |
| PG09 Now Playing | playing | Audio active |
| PG09 Now Playing | paused | Audio paused with saved position |
| PG09 Now Playing | playback error | Stream failed or source unavailable |
| PG10 Source Repair | source unavailable | Network/source cannot be reached |
| PG10 Source Repair | reauthorization required | Provider token expired or revoked |
| PG10 Source Repair | credentials required | SMB credentials invalid |
| PG10 Source Repair | repair complete | Source is reachable again |

## Implement

| From | Trigger | To |
| --- | --- | --- |
| Home | Resume | Now Playing |
| Home | Browse library | Library |
| Home/Library | Add source | Sources |
| Sources | Select SMB | SMB Setup |
| Sources | Select cloud provider | Provider Authorization |
| SMB Setup/Provider Authorization | Validated/authorized | Folder Picker |
| Folder Picker | Select this folder | Sync Progress |
| Sync Progress | Review discovered books | Discovered Books |
| Discovered Books | Add to library | Discovered Books |
| Discovered Books | View library | Library |
| Library | Select book | Book Detail |
| Book Detail | Resume/Start | Now Playing |
| Now Playing | Repair source | Source Repair |
| Source Repair | Edit SMB credentials | SMB Setup |
| Source Repair | Reauthorize provider | Provider Authorization |

## Stub

- Actual SMB validation: deterministic success/error states.
- Actual OAuth/device authorization: pending, success, and error states without real provider calls.
- Actual playback: simulated controls, buffering, saved progress, and errors.
- Background sync: simulated progress counts and partial errors.

## Edge cases

| Case | Screen | How |
| --- | --- | --- |
| No source exists | Home / Library | Empty state with Add source |
| Empty selected folder | Folder Picker / Library | No audiobooks found |
| Auth expired | Provider Authorization / Source Repair | Reauthorization required |
| SMB host unreachable | SMB Setup / Source Repair | Host/network error |
| Partial sync | Sync Progress | Warning with usable library option |
| Long title | Home / Library / Book Detail / Now Playing | Wrap/truncate safely |
| Large library | Library | Grid implies virtualization/paging |
| Playback source dropout | Now Playing / Source Repair | Preserve saved position and repair |

## Do not

- Generate screens not in the inventory.
- Use phone-style bottom navigation, tab bars, hover-only controls, or touch-only gestures.
- Browse remote folders live from Library.
- Expose passwords, OAuth tokens, raw provider URLs, provider file IDs, or stack traces.
- Collapse Dropbox, Google Drive, iCloud Drive, and OneDrive into generic WebDAV.
- Use lorem ipsum or placeholder data.

## Acceptance

- [ ] All screens render with listed states.
- [ ] Primary resume and browse-to-play flows complete end to end.
- [ ] Source setup supports SMB and first-class cloud branches.
- [ ] Empty, loading, error, permission, partial, buffering, and repair states are present.
- [ ] D-pad focus is visible on every interactive element.
- [ ] Long text and maximum data examples do not overlap controls.
- [ ] Realistic mock data appears throughout.
