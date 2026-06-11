> Provisional: updated after story-splitting pass. Review before treating as authoritative.

# Action Specifications

> File: docs/ux-ui/actions.md

## Index

| ID | Action | Type | Page | Actor | Priority |
| --- | --- | --- | --- | --- | --- |
| A01 | Resume | Progression | PG01 Home | Leo | Primary |
| A02 | Browse library | Progression | PG01 Home | Leo | Secondary |
| A03 | Add source | Progression | PG01/PG07 | Sam/Clara | Primary when empty |
| A04 | Select SMB | Progression | PG02 Sources | Sam | Primary |
| A05 | Select cloud provider | Progression | PG02 Sources | Clara | Primary |
| A06 | Test connection | Investigation | PG03 SMB Setup | Sam | Primary |
| A07 | Start authorization | Progression | PG04 Provider Authorization | Clara | Primary |
| A08 | Select this folder | Progression | PG05 Folder Picker | Sam/Clara | Primary |
| A09 | Review discovered books | Progression | PG06 Sync Progress | Sam/Clara/Leo | Primary when results exist |
| A10 | Select book | Progression | PG07 Library | Leo | Primary |
| A11 | Resume book | Progression | PG08 Book Detail | Leo | Primary |
| A12 | Play/Pause | Modification | PG09 Now Playing | Leo | Primary |
| A13 | Change speed | Modification | PG09 Now Playing | Leo | Secondary |
| A14 | Retry playback | Recovery | PG09 Now Playing | Leo | Primary in error |
| A15 | Repair source | Recovery | PG01/PG08/PG09/PG10 | Leo/Sam/Clara | Primary in source error |
| A16 | Retry source | Recovery | PG10 Source Repair | Leo/Sam/Clara | Primary |
| A17 | Edit SMB credentials | Recovery | PG10 Source Repair | Sam | Secondary |
| A18 | Reauthorize provider | Recovery | PG10 Source Repair | Clara | Secondary |
| A19 | View cached library | Recovery | PG10 Source Repair | Leo | Secondary |
| A20 | Add to library | Modification | PG11 Discovered Books / PG08 Book Detail | Leo | Primary |

---

## Resume - A01

**Type:** Progression | **Page:** PG01 Home | **Story:** leo-resumes-current-book.md | **Flow:** leo-resumes-current-book.md | **Actor:** Leo | **Priority:** Primary

### Intent
Resume moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Resume is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Leo.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG01 Home transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: resume
- Properties: screen_id, actor_type, source_type, state, result

---

## Browse library - A02

**Type:** Progression | **Page:** PG01 Home | **Story:** leo-scans-cached-library.md | **Flow:** leo-scans-cached-library.md | **Actor:** Leo | **Priority:** Secondary

### Intent
Browse library moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Browse library is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Leo.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG01 Home transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: browse_library
- Properties: screen_id, actor_type, source_type, state, result

---

## Add source - A03

**Type:** Progression | **Page:** PG01/PG07 | **Story:** sam-chooses-smb-source.md; clara-chooses-cloud-provider.md | **Flow:** sam-chooses-smb-source.md; clara-chooses-cloud-provider.md | **Actor:** Sam/Clara | **Priority:** Primary when empty

### Intent
Add source moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Add source is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Sam/Clara.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG01/PG07 transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: add_source
- Properties: screen_id, actor_type, source_type, state, result

---

## Select SMB - A04

**Type:** Progression | **Page:** PG02 Sources | **Story:** sam-chooses-smb-source.md | **Flow:** sam-chooses-smb-source.md | **Actor:** Sam | **Priority:** Primary

### Intent
Select SMB moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Select SMB is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Sam.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG02 Sources transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: select_smb
- Properties: screen_id, actor_type, source_type, state, result

---

## Select cloud provider - A05

**Type:** Progression | **Page:** PG02 Sources | **Story:** clara-chooses-cloud-provider.md | **Flow:** clara-chooses-cloud-provider.md | **Actor:** Clara | **Priority:** Primary

### Intent
Select cloud provider moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Select cloud provider is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Clara.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG02 Sources transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: select_cloud_provider
- Properties: screen_id, actor_type, source_type, state, result

---

## Test connection - A06

**Type:** Investigation | **Page:** PG03 SMB Setup | **Story:** sam-validates-smb-connection.md | **Flow:** sam-validates-smb-connection.md | **Actor:** Sam | **Priority:** Primary

### Intent
Test connection moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Test connection is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Sam.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG03 SMB Setup transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: test_connection
- Properties: screen_id, actor_type, source_type, state, result

---

## Start authorization - A07

**Type:** Progression | **Page:** PG04 Provider Authorization | **Story:** clara-authorizes-cloud-provider.md | **Flow:** clara-authorizes-cloud-provider.md | **Actor:** Clara | **Priority:** Primary

### Intent
Start authorization moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Start authorization is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Clara.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG04 Provider Authorization transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: start_authorization
- Properties: screen_id, actor_type, source_type, state, result

---

## Select this folder - A08

**Type:** Progression | **Page:** PG05 Folder Picker | **Story:** sam-selects-smb-library-folder.md; clara-selects-cloud-library-folder.md | **Flow:** sam-selects-smb-library-folder.md; clara-selects-cloud-library-folder.md | **Actor:** Sam/Clara | **Priority:** Primary

### Intent
Select this folder moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Select this folder is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Sam/Clara.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG05 Folder Picker transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: select_this_folder
- Properties: screen_id, actor_type, source_type, state, result

---

## Review discovered books - A09

**Type:** Progression | **Page:** PG06 Sync Progress | **Story:** sam-reviews-discovered-smb-books.md; clara-reviews-discovered-cloud-books.md | **Flow:** sam-reviews-discovered-smb-books.md; clara-reviews-discovered-cloud-books.md | **Actor:** Sam/Clara/Leo | **Priority:** Primary when results exist

### Intent
Review discovered books moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Review discovered books is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Sam/Clara/Leo.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG06 Sync Progress transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: review_discovered_books
- Properties: screen_id, actor_type, source_type, state, result

---

## Select book - A10

**Type:** Progression | **Page:** PG07 Library | **Story:** leo-reviews-book-detail.md | **Flow:** leo-reviews-book-detail.md | **Actor:** Leo | **Priority:** Primary

### Intent
Select book moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Select book is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Leo.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG07 Library transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: select_book
- Properties: screen_id, actor_type, source_type, state, result

---

## Resume book - A11

**Type:** Progression | **Page:** PG08 Book Detail | **Story:** leo-starts-selected-book.md | **Flow:** leo-starts-selected-book.md | **Actor:** Leo | **Priority:** Primary

### Intent
Resume book moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Resume book is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Leo.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG08 Book Detail transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: resume_book
- Properties: screen_id, actor_type, source_type, state, result

---

## Play/Pause - A12

**Type:** Modification | **Page:** PG09 Now Playing | **Story:** leo-resumes-current-book.md | **Flow:** leo-resumes-current-book.md | **Actor:** Leo | **Priority:** Primary

### Intent
Play/Pause moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Play/Pause is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Leo.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG09 Now Playing transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: play_pause
- Properties: screen_id, actor_type, source_type, state, result

---

## Change speed - A13

**Type:** Modification | **Page:** PG09 Now Playing | **Story:** leo-resumes-current-book.md | **Flow:** leo-resumes-current-book.md | **Actor:** Leo | **Priority:** Secondary

### Intent
Change speed moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Change speed is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Leo.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG09 Now Playing transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: change_speed
- Properties: screen_id, actor_type, source_type, state, result

---

## Retry playback - A14

**Type:** Recovery | **Page:** PG09 Now Playing | **Story:** leo-sees-playback-source-failure.md | **Flow:** leo-sees-playback-source-failure.md | **Actor:** Leo | **Priority:** Primary in error

### Intent
Retry playback moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Retry playback is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Leo.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG09 Now Playing transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: retry_playback
- Properties: screen_id, actor_type, source_type, state, result

---

## Repair source - A15

**Type:** Recovery | **Page:** PG01/PG08/PG09/PG10 | **Story:** leo-retries-failed-source.md | **Flow:** leo-retries-failed-source.md | **Actor:** Leo/Sam/Clara | **Priority:** Primary in source error

### Intent
Repair source moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Repair source is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Leo/Sam/Clara.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG01/PG08/PG09/PG10 transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: repair_source
- Properties: screen_id, actor_type, source_type, state, result

---

## Retry source - A16

**Type:** Recovery | **Page:** PG10 Source Repair | **Story:** leo-retries-failed-source.md | **Flow:** leo-retries-failed-source.md | **Actor:** Leo/Sam/Clara | **Priority:** Primary

### Intent
Retry source moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Retry source is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Leo/Sam/Clara.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG10 Source Repair transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: retry_source
- Properties: screen_id, actor_type, source_type, state, result

---

## Edit SMB credentials - A17

**Type:** Recovery | **Page:** PG10 Source Repair | **Story:** sam-validates-smb-connection.md | **Flow:** sam-validates-smb-connection.md | **Actor:** Sam | **Priority:** Secondary

### Intent
Edit SMB credentials moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Edit SMB credentials is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Sam.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG10 Source Repair transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: edit_smb_credentials
- Properties: screen_id, actor_type, source_type, state, result

---

## Reauthorize provider - A18

**Type:** Recovery | **Page:** PG10 Source Repair | **Story:** clara-authorizes-cloud-provider.md | **Flow:** clara-authorizes-cloud-provider.md | **Actor:** Clara | **Priority:** Secondary

### Intent
Reauthorize provider moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for Reauthorize provider is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Clara.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG10 Source Repair transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: reauthorize_provider
- Properties: screen_id, actor_type, source_type, state, result

---

## View cached library - A19

**Type:** Recovery | **Page:** PG10 Source Repair | **Story:** leo-retries-failed-source.md | **Flow:** leo-retries-failed-source.md | **Actor:** Leo | **Priority:** Secondary

### Intent
View cached library moves the user through the audiobook/source flow while preserving cached context, focus, and source/playback state.

### Preconditions
- Actor has access to the current screen.
- Required data for View cached library is visible or the action is disabled.
- Source-dependent actions require source state to allow the action.

### Permission rules
- Allowed for: Leo.
- Blocked for: actors not listed or states where data/states.md marks the action blocked.
- Conditions: hide or disable if the associated source, book, playback, or folder state does not allow the action.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Required context present | Required information is missing. | Disable action until context exists |
| Source reachable when needed | Source unavailable. | Offer Repair source or Retry |
| Duplicate activation | Working... | Keep focus and block repeated action |

### Confirmation
- Required: No
- Style: None
- Heading: N/A
- Body: N/A
- Confirm label: N/A
- Cancel label: N/A
- Destructive: No

### Result
The screen transitions or local state updates as defined in sitemap.md and the relevant screen transition contract.

### State transition
See docs/ux-ui/data/states.md for Source, Library, Book, and Playback state transitions.

### Destination
See PG10 Source Repair transition contract and docs/ux-ui/screens/sitemap.md.

### Success feedback
- Style: Inline state update, navigation, or short status/toast.
- Copy: Product-specific success message from the source screen where specified.

### Error feedback
- Style: Inline or page-level source-specific error.
- Copy: Use the source screen's Error heading/body.
- Recovery: Retry, repair, reauthorize, edit credentials, choose another folder, or view cached library depending on failure category.

### Undo
- Available: Back/cancel where applicable; no destructive undo in Phase 1.
- Window: Current flow state.
- Trigger: Back or Cancel.

### Analytics
- Event: view_cached_library
- Properties: screen_id, actor_type, source_type, state, result


---

## Add to library - A20

**Type:** Modification | **Page:** PG11 Discovered Books / PG08 Book Detail | **Story:** leo-adds-book-to-listening-library.md | **Flow:** leo-adds-book-to-listening-library.md | **Actor:** Leo the Living Room Listener | **Priority:** Primary

### Intent
Add one discovered audiobook to the curated listening library.

### Preconditions
- Discovered book is supported.
- Book is not already added.
- Local metadata cache is writable.

### Validation

| Rule | Message | Behaviour |
| --- | --- | --- |
| Already added | This book is already in your listening library. | Disable Add and show Added badge |
| Unsupported | This discovered item cannot be added yet. | Disable Add and show reason |
| Source unavailable | The book was found, but its source needs attention. | Offer Source Repair |

### Result
Creates a listening-library item and updates the discovered row to Added.

### State transition
Discovered Book from discovered -> added.

### Destination
Stay on Discovered Books or open Library by user action.

### Success feedback
- Style: Row badge plus optional toast.
- Copy: Added to listening library.

### Error feedback
- Style: Row-level error.
- Copy: Some books need attention.
- Recovery: Review source issue or retry.
