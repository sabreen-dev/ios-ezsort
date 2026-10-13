# User Experience

## Purpose and status

Owns user journeys, interaction responsibilities, and presentation states. [Product Requirements](02-business-requirements.md) alone defines behavior and acceptance criteria. [Engineering Principles](00-engineering-principles.md) governs implementation quality.

**CONFIRMED** journeys below reflect prior discussion. Screen grouping, controls, navigation layout, and exception presentation are **PROPOSED** until approved. Screen responsibilities describe interaction areas, not a commitment to separate screens. Open product questions remain in the [question register](02-business-requirements.md#open-questions-and-blockers).

## UX-01 — Import and review

Related: [FR-001](02-business-requirements.md#fr-001--screenshot-route-import), [FR-002](02-business-requirements.md#fr-002--screen-recording-route-import), [FR-003](02-business-requirements.md#fr-003--in-app-route-list), [FR-007](02-business-requirements.md#fr-007--imported-information-corrections).

**CONFIRMED journey:** The worker provides route screenshots or a single screen recording. The resulting route is available in the app; imported information can be corrected.

**PROPOSED interaction responsibilities:** An import area offers the two source choices. A route review area exposes the imported information and access to corrections. Neither mandatory review of every entry nor a separate approval screen is agreed.

**PROPOSED states:** Before a route exists, explain the available import methods. During processing, indicate that work is underway without showing partial information as a finished route. If processing fails, explain what could not be read and offer a suitable next action after Q-02 is resolved.

**OPEN QUESTION:** Q-01/Q-02 govern source issues; Q-04 governs editing controls. Replacement of an existing route belongs to Q-06. Do not invent import completeness guarantees.

## UX-02 — Identify and label a package

Related: [FR-004](02-business-requirements.md#fr-004--camera-address-lookup), [FR-005](02-business-requirements.md#fr-005--manual-address-search), [FR-006](02-business-requirements.md#fr-006--ambiguous-match-clarification).

**CONFIRMED journey:** The worker locates an entry by scanning the package address or entering address text. The result supplies the stop number for the worker to write on the package. Ambiguous matches require worker choice. Clearing manual search returns the worker to the full route list.

**PROPOSED interaction responsibilities:** The route area exposes search and access to camera lookup. A result area pairs a prominent stop number with enough address context for recognition. Candidate choices remain distinguishable. Returning from a result to route preparation should be straightforward; a tab bar, modal, or particular navigation layout is not selected.

**PROPOSED states:** Distinguish camera reading in progress, a resolved match, candidate selection, and no usable result. Search with no matches should visibly differ from an empty route. Offer manual search after a scan problem as an available alternative, without implying it will resolve every failure.

**OPEN QUESTION:** Q-03/Q-05 govern candidate details, permissions or unreadable-label recovery, no-result wording, and dismissal of unresolved choices. No candidate ranking or automatic confirmation is approved.

## UX-03 — Record progress and review before departure

Related: [FR-008](02-business-requirements.md#fr-008--worker-managed-found-counts), [FR-009](02-business-requirements.md#fr-009--progress-and-completion), [FR-010](02-business-requirements.md#fr-010--pre-departure-checklist-review).

**CONFIRMED journey:** After identifying and organizing a package, the worker explicitly records found-package progress. Before leaving, the worker reviews entries that remain incomplete and investigates discrepancies. The progress display is governed by FR-009; lookup actions are separate from count updates under FR-008.

**PROPOSED interaction responsibilities:** Put current progress near the corresponding route entry and provide an understandable way to adjust it. Keep incomplete and complete states distinguishable. Count-entry fields versus increment/decrement controls remain undecided; no dedicated incomplete-only filter is approved.

**OPEN QUESTION:** Q-04 governs invalid or excessive counts and edits. Q-05 governs unmatched packages. Q-06 governs whether and how progress survives leaving or reopening the app.

## UX-04 — Route management

Related: [FR-011](02-business-requirements.md#fr-011--route-deletion), [NFR-003](02-business-requirements.md#nfr-003--route-data-privacy).

**CONFIRMED responsibility:** Provide an easy way to delete a route. Deletion scope follows the requirements and Q-06, not an assumed history or archive feature.

**PROPOSED states:** A discoverable deletion action and clear indication of its outcome; exact placement, confirmation, recovery, and post-deletion navigation require approval. Multi-route management is not a confirmed capability.

## UX-05 — Cross-workflow usability

Related: [NFR-001](02-business-requirements.md#nfr-001--ios-product), [NFR-002](02-business-requirements.md#nfr-002--offline-use-after-import), [NFR-003](02-business-requirements.md#nfr-003--route-data-privacy).

**CONFIRMED goals:** Fast, clear interactions while handling packages; prominent stop numbers; meaningful match clarification; and continued post-import use without internet. These goals do not establish a numerical interaction or latency budget.

**PROPOSED accessibility considerations:** Readable text, usable touch controls, descriptive assistive-technology labels, sensible focus order, and completion states conveyed without relying only on color. These recommendations require product review under Q-07 and are not new confirmed NFRs.

**PROPOSED state consistency:** Make loading, empty content, no search matches, and errors visually and verbally distinct. Avoid presenting failure as successful completion. Error handling must also comply with engineering principles; precise recovery interactions remain open.

## Review boundary

Owner review of these proposals is required before treating screen layout, accessibility commitments, or exception flows as approved. [Testing Strategy](09-test-strategy.md) validates agreed journeys; [Implementation Plan](08-implementation-plan.md) sequences their delivery.
