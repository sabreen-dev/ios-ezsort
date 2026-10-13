# Product Requirements

## Purpose and authority

This existing filename is retained as the equivalent of the requested `02-product-requirements.md`. It is the **sole authoritative source for functional requirements, nonfunctional product requirements, business rules, and acceptance criteria**. Its scope includes product behavior, not architecture, detailed screen design, or development tasks.

[Product Vision](01-product-vision.md) owns why the product exists. [Engineering Principles](00-engineering-principles.md) governs engineering quality and remains unchanged.

## Documentation ownership

Existing equivalent filenames are preserved; no parallel documents with the suggested replacement names are needed.

| Document | Sole responsibility |
| --- | --- |
| [00 Engineering Principles](00-engineering-principles.md) | Universal engineering standards |
| [01 Product Vision](01-product-vision.md) | Purpose, users, goals, high-level scope and direction |
| [02 Product Requirements](02-business-requirements.md) | All functional and nonfunctional product requirements, business rules, acceptance criteria, and product open questions |
| [03 Requirements Traceability](03-functional-requirements.md) | Cross-document coverage references; no independent requirement definitions |
| [04 User Experience](04-ux-spec.md) | Journeys, interaction responsibilities, and proposed presentation states |
| [05 Architecture](05-architecture.md) | Technical responsibilities, boundaries, options, and tradeoffs |
| [06 Domain Model](06-domain-model.md) | Supporting conceptual vocabulary and relationships; no database schema or independent business rules |
| [07 API Contracts](07-api-contracts.md) | Interface-contract status and unresolved boundary contracts; no assumed backend |
| [08 Implementation Plan](08-implementation-plan.md) | Development sequencing, dependencies, and milestone completion |
| [09 Testing Strategy](09-test-strategy.md) | Verification approach, planned scenarios, and evidence requirements |
| [10 Decision Log](10-decision-log.md) | Significant decisions, provenance, known rationale, and consequences |

Change a requirement here first, preserve its identifier, then update affected supporting references. Retired identifiers are not reassigned. References and summaries elsewhere do not create additional requirements. The [traceability matrix](03-functional-requirements.md) connects each confirmed requirement to UX, architecture, milestones, and planned verification.

## Classification and scope

- **CONFIRMED:** Explicitly established through discussion.
- **WORKING ASSUMPTION:** Authorized provisional basis for planning, not verified fact.
- **PROPOSED:** Recommendation requiring owner approval; not implementation authorization.
- **OPEN QUESTION:** Missing information or unresolved decision. Its blocking impact is stated below.

All FR and NFR identifiers below describe CONFIRMED MVP commitments. Acceptance criteria operationalize the agreed behavior; where an edge case lacks an agreed outcome, it is referenced as an open question rather than given an invented result. Conditional source-data assumptions do not guarantee successful import of unknown material. Proposed capabilities and questions receive no FR/NFR identifiers.

## Functional requirements

### FR-001 — Screenshot route import

**Behavior, input, output:** Accept worker-provided route screenshots and create the app's own route list from their visible information.

**Acceptance:** Given readable screenshots containing the agreed planning fields, import produces route entries reflecting the supplied addresses, stop numbers, and package counts, without substituting invented values. A set of screenshots is an input route source, not a separate route per image by definition.

**Unresolved validation/failures:** Actual source layout, overlapping captures, incomplete coverage, and unreadable fields: Q-01 and Q-02. Supported file constraints are not decided.

### FR-002 — Screen-recording route import

**Behavior, input, output:** Accept a single worker-provided screen recording of the route list and create the in-app route list from its visible information.

**Acceptance:** Given a readable recording containing the planning fields, imported entries reflect the visible source information. This is an alternative import method to FR-001, not a future enhancement.

**Unresolved validation/failures:** Repeated visible content, scrolling gaps, unreadable content, recording length and format: Q-01 and Q-02. No sampling algorithm is prescribed.

### FR-003 — In-app route list

**Behavior, input, output:** Present imported addresses with their stop numbers, expected package counts, and worker-recorded progress.

**Acceptance:** For an imported entry with known fields, the worker can associate its address with its source stop number, expected count, and recorded found count. Completion presentation follows FR-009.

**Unresolved validation/edge cases:** The availability and grouping of source fields are assumption A-01, not verified facts. Repeated addresses and grouped stops require Q-01 and Q-03; do not assume address text uniquely identifies an entry.

### FR-004 — Camera address lookup

**Behavior, input, output:** Use the package address read through the camera to locate a route entry and prominently display its stop number for physical package labeling.

**Acceptance:** With a readable address that unambiguously matches an imported entry, the worker sees the corresponding address and stop number. Lookup alone leaves recorded counts unchanged. Ambiguity is governed by FR-006.

**Unresolved validation/failures:** Address variations, unreadable labels, and no-match presentation: Q-03 and Q-05. A no-match result does not establish that a package is extra (FR-010).

### FR-005 — Manual address search

**Behavior, input, output:** Filter the route list as the worker types part or all of an address. Matching entries expose their addresses and stop numbers; clearing the query restores the full list.

**Acceptance:** With entries containing `123 Main`, typing `123` narrows the list to addresses containing that entered text; continuing with `123 Main` narrows it further. Clearing the query restores all entries. Searching does not change found counts or completion state.

**Unresolved edge cases:** Case, punctuation, abbreviations, unit handling, and no-result presentation: Q-03 and Q-05. These examples do not approve fuzzy matching or ranking behavior.

### FR-006 — Ambiguous-match clarification

**Behavior, input, output:** When an address has multiple plausible route matches, let the worker choose instead of silently selecting one stop.

**Acceptance:** Given multiple plausible candidates, no single candidate is presented as the confirmed result before the worker resolves the ambiguity. The worker can select the intended entry and obtain its stop number.

**Unresolved validation/edge cases:** Candidate qualification and presentation, repeated addresses under different stops, and inability to choose: Q-03 and Q-05.

### FR-007 — Imported information corrections

**Behavior, input, output:** Allow workers to correct imported addresses, stop numbers, and expected package counts.

**Acceptance:** After a worker corrects a field and applies the correction, the route list exposes the corrected value for that entry. The app does not continue presenting the superseded value as current.

**Unresolved validation/edge cases:** Allowed values, edit controls, duplicate or conflicting edits, and changes to expected counts when progress exists: Q-04. Specific numeric bounds or correction propagation policies are not yet agreed.

### FR-008 — Worker-managed found counts

**Behavior, input, output:** Let the worker manually record and correct how many packages have been found for an entry. Address scanning and search do not automatically increment counts.

**Acceptance:** An explicit count update changes the recorded found count for the intended entry. A correction can revise that count. Repeated scans or searches without a count update leave the recorded count unchanged.

**Unresolved validation/edge cases:** Count controls, invalid values, values above the expected total, and initialization/reset details: Q-04 and Q-06. No individual-package identity or duplicate detection is implied.

### FR-009 — Progress and completion

**Behavior, input, output:** Display found-versus-expected progress for each entry and a checkmark once all expected packages have been recorded as found.

**Acceptance:** For an entry expecting three packages, recorded counts zero, one, and two display `0/3`, `1/3`, and `2/3`; a recorded count of three displays a completion checkmark. For an entry expecting one package, recording that package completes the entry. Correcting a completed entry to fewer found packages returns it to incomplete progress.

**Unresolved validation/edge cases:** Overcounts, invalid expected counts, and edits to expected counts: Q-04. Completion indicates a worker-recorded count, not independent physical verification.

### FR-010 — Pre-departure checklist review

**Behavior, input, output:** Let the worker review route entries and their progress to determine what may still be missing before departure.

**Acceptance:** Entries below their expected counts remain visibly incomplete; complete entries show FR-009's completion state. The list enables the worker to distinguish these states. Neither incomplete entries nor unmatched addresses are represented as independently verified missing or extra packages.

**Unresolved interactions:** A dedicated incomplete-only filter or special extra-package workflow has not been approved; Q-05 covers discrepancy handling.

### FR-011 — Route deletion

**Behavior, input, output:** Make it easy for the worker to delete a route.

**Acceptance:** After the worker completes deletion, that route is no longer available as an active route for lookup and checklist use.

**Unresolved scope/failures:** Retention of imported media, associated progress, deletion confirmation, interruption handling, and whether multiple routes can exist: Q-06. This criterion does not claim a defined secure-erasure policy.

## Nonfunctional requirements

### NFR-001 — iOS product

**Requirement:** The initial application is for iOS.

**Acceptance:** The supported release runs its agreed workflows on the selected iOS device/version support set. The support set must be resolved through Q-07 before compatibility validation can be complete.

### NFR-002 — Offline use after import

**Requirement:** After a route is imported, camera address lookup and matching, manual search, and checklist updates work without an internet connection.

**Acceptance:** With an imported route available and network access disabled, FR-004, FR-005, FR-006 where applicable, and FR-008 through FR-010 remain usable and produce their specified outcomes.

**Boundary:** Offline import has not been agreed. Network-dependent recognition for post-import lookup would not satisfy this requirement.

### NFR-003 — Route-data privacy

**Requirement:** Keep route data and processing on the device where practical, and protect address data under the universal engineering standards. Route deletion is defined by FR-011.

**Acceptance:** The data-flow review accounts for where route and address information is processed and retained. Any proposed off-device use is explicitly identified for owner resolution under Q-08 before adoption; it must not be silently assumed. Verification demonstrates that implemented flows match the approved handling and do not expose sensitive address data in logs.

**Limit:** The agreed phrase “where practical” does not settle a blanket no-network policy, retention duration, or external-processing consent design. Final privacy validation is blocked until relevant Q-06/Q-08 choices are resolved.

## Assumptions and open questions

### A-01 — Source fields

**WORKING ASSUMPTION:** The uploaded list contains addresses, expected package counts, and stop numbers. The owner authorized planning on this basis until a sample can be supplied. No sample screenshot or recording has been supplied. Source parsing and fidelity cannot be accepted on synthetic examples alone.

### Open questions and blockers

| Reference | OPEN QUESTION | Blocking impact |
| --- | --- | --- |
| Q-01 | What do real screenshots and recordings contain, including grouped stops, repeated addresses, and package counts? | Blocks validated source mapping and real import acceptance for FR-001–FR-003. Synthetic exploration can proceed under A-01. |
| Q-02 | How should incomplete, overlapping, repeated, unreadable, or malformed import content be handled? Which media constraints apply? | Blocks reliable import exception criteria and production-ready import completion. |
| Q-03 | Which address variations should match, and how should units, repeated addresses, and candidate ambiguity be distinguished? | Blocks full matching edge-case specification; simple exact-text cases can be explored. |
| Q-04 | Which correction/count controls and validation rules apply, including negative or fractional values, overcounts, and edits below existing progress? | Blocks final editing and count-validation behavior. No arbitrary limits are approved. |
| Q-05 | How should unreadable scans, no results, unresolved ambiguity, and possible extra packages be presented and recovered from? | Blocks complete exception UX; no automatic extra-package verdict is authorized. |
| Q-06 | How long do route data, imported media, and progress remain available? What happens on reopening, new import, deletion, or interrupted deletion? | Blocks persistence lifetime, replacement policy, and complete deletion scope. Earlier assistant text suggested saving across app closure, but explicit approval of that lifecycle was not established. |
| Q-07 | Which iOS versions/devices are supported, and what usability, accessibility, and response-time criteria should apply? | Blocks compatibility matrix and measurable quality thresholds. Fast/simple use is a confirmed goal; numeric targets and accessibility commitments remain undecided. |
| Q-08 | Is off-device processing ever acceptable, and must import also work offline? | Blocks any external-processing contract or exception to local handling; post-import offline scope is already fixed by NFR-002. |

These questions require evidence or owner decisions. They are not proposed requirements with reserved FR/NFR identifiers. Proposed UI and technical options are owned by their supporting documents, not approved by inclusion here.

## Deferred scope

Automatic package counting and duplicate-package scan detection are **PROPOSED future opportunities**, outside the confirmed MVP. Unique package identifiers were discussed only as a possible means to distinguish packages. There is no commitment to automatic missing/extra-package verification or a selected identifier mechanism.
