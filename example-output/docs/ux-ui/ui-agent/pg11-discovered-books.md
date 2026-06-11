> Provisional: updated after story-splitting pass. Review before treating as authoritative.

# PG11 Discovered Books

PRODUCT AND DESIGN CONTEXT

Android TV audiobook app with a new discovery/import boundary: discovered books are indexed from sources, while Library contains books explicitly added to the listening library.

---

SCREEN CONTEXT

Discovered Books is reached after Sync Progress or from an empty Library. It lets the user review indexed audiobooks and add selected items.

---

SCREEN SPECIFICATION - PG11 Discovered Books

States to render: discovered list, partial results, empty discovered, added state, unsupported blocked.

Actions: Add to library, Open details, View library, Review source issue, Choose another folder.

Transition contract: Sync Progress -> Discovered Books -> Book Detail or Library. Add to library stays on the focused item and changes it to Added.

Content: Page title "Discovered books"; primary action "Add to library"; empty heading "No audiobooks discovered"; success "Added to listening library."

Acceptance: Generated screen must make discovered-vs-added clear, prevent duplicate add, preserve focus after add, and show partial/unsupported results without raw paths.
