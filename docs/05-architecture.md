# Architecture

## Purpose and authority

Owns technical structure, responsibility boundaries, state ownership, data flow, persistence options, and technical tradeoffs. [Product Requirements](02-business-requirements.md) defines behavior; [Engineering Principles](00-engineering-principles.md) controls engineering standards. [Domain Model](06-domain-model.md) supplies vocabulary, and [API Contracts](07-api-contracts.md) owns contract status.

**Status:** No implementation technologies or detailed architecture have been approved. The design below is **PROPOSED**, except the referenced confirmed product constraints. It describes logical responsibilities, not mandatory classes, services, layers, or interfaces. Do not introduce a backend, third-party dependency, or framework merely because this document describes a boundary.

## ARC-01 — Media intake and interpretation

Related: FR-001, FR-002, FR-003, FR-007.

**PROPOSED:** Keep source-media interpretation separate from route lookup and checklist rules. Image and recording inputs can share interpretation of recognized route information; recording-specific handling remains isolated where it differs. Preserve enough source association during processing to diagnose uncertain extraction without putting sensitive content in logs.

Flow: supplied media → interpreted candidate entries → accepted/corrected route state. Candidate versus usable state is a proposed reliability boundary, not an approved mandatory review step.

Options: shared interpretation reduces inconsistent handling; separate source adapters accommodate media differences but can add needless indirection if made too granular. Real examples under Q-01/Q-02 must guide the design. No recognition engine, frame-selection algorithm, or deduplication strategy is selected.

## ARC-02 — Address lookup

Related: FR-004, FR-005, FR-006, NFR-002.

**PROPOSED:** Separate camera address capture from matching against route entries. Keep manual-query filtering and candidate resolution understandable and testable without camera hardware. Matching produces a result that presentation can show without modifying found counts.

Flow: captured address or manual query + current route → match/candidate/filter result → presentation. These results must preserve route-entry identity, especially where address text repeats.

Options: exact matching is easier to explain but misses textual variations; normalization may improve usefulness but can merge distinct addresses or units. Q-03 must settle semantics before an algorithm is accepted. Camera recognition used after import must respect the confirmed offline constraint; a network-only dependency is incompatible with that scope.

## ARC-03 — Route and checklist state

Related: FR-003, FR-007, FR-008, FR-009, FR-010.

**PROPOSED ownership:** A cohesive route/checklist responsibility owns current entries and explicit corrections. The presentation owns transient query text, camera activity, and selected candidate; it does not independently maintain a conflicting copy of package counts. Import owns in-progress interpretation until applied to route state.

Keep state changes explicit and serialize or otherwise coordinate competing updates. Favor immutable snapshots where practical. Derive completion presentation from the authoritative count state rather than independently editable flags. This is a technical proposal, not a new business rule; unresolved count cases remain Q-04.

Concurrent camera/import work needs cancellation, lifecycle ownership, and stale-result handling under engineering principles. Returning late results must not overwrite a later correction or newly selected route. The exact concurrency mechanism is unselected.

## ARC-04 — Persistence and deletion

Related: FR-011, NFR-002, NFR-003.

**PROPOSED:** Encapsulate storage operations sufficiently to test failure and deletion without coupling business rules to a particular storage API. Use a direct, cohesive implementation where adequate; do not add a generic repository layer by default.

Options: in-memory state offers low complexity but no restart survival; local durable storage supports restart survival with migration, deletion, and consistency obligations. A structured file may be sufficient for simple route state; a local database adds query and update capabilities with added complexity. Neither storage method nor restart behavior is selected. Q-06 blocks the lifetime decision; offline availability during use alone does not establish permanent retention.

Media retention, checklist lifetime, route replacement, and deletion scope must be decided before a durable schema or cleanup contract is finalized.

## ARC-05 — Runtime, boundaries, and privacy

Related: NFR-001, NFR-002, NFR-003; cross-cutting FR-001–FR-011.

**CONFIRMED constraints:** Consult the NFR definitions; they determine platform, offline scope, and local-data preference.

**PROPOSED dependency direction:** User-facing interaction and media/storage adapters invoke focused route operations. Business rules should not require a camera, external service, or concrete persistence API to be tested. Add small contracts only at boundaries that genuinely need substitution or isolation. Keep cohesive code together rather than manufacturing architectural layers.

No language, UI framework, recognition library, storage technology, dependency injection framework, external integration, or remote API is selected. Evaluate candidates against offline capability, clarity, privacy, testability, lifecycle behavior, and actual workload. Native capabilities may reduce dependencies; third-party options may offer capability at maintenance and privacy cost. These are options, not adopted decisions.

### Error and security strategy

**PROPOSED:** Distinguish input/read failures, unresolved matching, validation failures, and persistence failures at their responsible boundary. Propagate enough context to the user-facing layer for the approved recovery flow, without leaking customer content. Do not convert failed interpretation into invented data or a false success state. Bound expensive processing and release media/camera resources on completion, cancellation, or failure.

Input validation, sensitive-data protection, and safe resource handling are mandatory engineering standards; error wording, allowed field values, and product recovery choices remain owned by requirements/UX. Avoid sensitive logs and unnecessary retention. Any off-device flow needs Q-08 resolution, not an inferred permission from an architecture sketch.

## Architecture decisions pending

| Decision area | Options and tradeoff | Required evidence or approval |
| --- | --- | --- |
| Recognition and recording interpretation | Simpler direct processing versus additional processing stages; complexity must earn its place | Real media, offline lookup evidence, Q-01/Q-02/Q-08 |
| Address normalization | More matches versus false equivalence | Q-03 and representative ambiguous examples |
| Storage/lifetime | Transient simplicity versus durable recovery and deletion obligations | Q-06 |
| Platform/tooling | Available platform capabilities versus additional dependency cost | Q-07 and technical evaluation |
| External processing | Potential capability versus privacy/network dependency | Q-08; cannot break NFR-002 |

These are **OPEN QUESTION** technical choices. The [Decision Log](10-decision-log.md#dec-008--technical-structure-proposal) records proposal status, not invented history. [Implementation Plan](08-implementation-plan.md) owns evaluation sequencing.
