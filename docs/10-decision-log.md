# Decision Log

## Purpose and authority

Owns significant product and technical decisions, their status, known context, rationale, and consequences. [Product Requirements](02-business-requirements.md) owns normative behavior; entries reference it rather than define competing rules. No decision dates, participants beyond the owner/assistant conversation, or implementation history are invented.

Statuses are **CONFIRMED**, **WORKING ASSUMPTION**, **PROPOSED**, and **OPEN QUESTION** as defined in the requirements. Confirmed entries below derive from conversation; proposals added during documentation are labeled accordingly. Alternatives or rationale not explicitly discussed are identified as unrecorded. Consequences are analysis of the decision, not invented historical justification.

## DEC-001 — Product and initial import scope

- **Status:** CONFIRMED.
- **Context:** The owner described manually scrolling a route list to number packages at the station.
- **Decision:** Build the iOS preparation tool described in [Product Vision](01-product-vision.md), with both screenshot and single-screen-recording input in the MVP.
- **Related requirements:** FR-001, FR-002, FR-003, FR-004, NFR-001.
- **Recorded rationale:** Reduce preparation effort and make packages easier to locate during deliveries.
- **Alternatives considered:** Screenshots and a recording were requested as supported options; no alternative platform selection discussion was recorded.
- **Consequences/tradeoffs:** Both media paths need validation; recording support cannot silently become a future enhancement. The current Amazon Flex search limitation is an owner-reported problem, not independently verified here.

## DEC-002 — Proceed on assumed source fields

- **Status:** WORKING ASSUMPTION.
- **Context:** The owner could not provide a sample route list yet.
- **Decision:** Plan using A-01 in [Product Requirements](02-business-requirements.md#a-01--source-fields), revisiting it when a screenshot is available.
- **Related requirements:** FR-001, FR-002, FR-003.
- **Recorded rationale:** Continue planning now and adjust after seeing a real example.
- **Alternatives considered:** No detailed alternatives were discussed.
- **Consequences/tradeoffs:** Real import fidelity and grouping remain unverified. This decision approves a planning assumption, not a guarantee of source fields.

## DEC-003 — Worker-managed counts in the MVP

- **Status:** CONFIRMED.
- **Context:** Multiple packages can share an address, and scanning address text cannot distinguish distinct packages from repeated scans of one package.
- **Decision:** Use worker-managed counts in the MVP; automatic counting and duplicate-package identification remain deferred opportunities. The subsequent clarified workflow separates lookup from count updates.
- **Related requirements:** FR-008, FR-009, FR-010; FR-004/FR-005 for nonmutation during lookup.
- **Recorded rationale:** The owner chose to let the worker manage counts for now and consider automatic management later.
- **Alternatives considered:** Capturing a unique package identifier was discussed as a possible route to distinguishing packages; no mechanism was selected.
- **Consequences/tradeoffs:** Checklist accuracy depends on manual entries. It supports investigation of missing packages rather than independent verification.

## DEC-004 — Manual address search

- **Status:** CONFIRMED.
- **Context:** The owner requested typing part or all of an address to narrow the imported list.
- **Decision:** Include manual search alongside scanning, with authoritative behavior in FR-005.
- **Related requirements:** FR-005.
- **Recorded rationale:** Let workers quickly locate the stop number without searching the list by scrolling.
- **Alternatives considered:** No different search design was discussed; camera lookup remains another entry path.
- **Consequences/tradeoffs:** Search presentation must remain associated with the correct route entry. Detailed normalization is unresolved, not implied by approval of partial-text lookup.

## DEC-005 — Accuracy, corrections, offline use, and privacy priorities

- **Status:** CONFIRMED.
- **Context:** During the initial principles discussion, the assistant proposed accuracy over silent guessing, corrections, offline use after import, keeping data on the device where practical, and easy route deletion. The owner agreed.
- **Decision:** Preserve those product commitments in the requirements rather than in universal engineering standards.
- **Related requirements:** FR-006, FR-007, FR-011, NFR-002, NFR-003.
- **Recorded rationale:** The discussion emphasized speed/simplicity, accurate matching, worker corrections, and address-data protection. No detailed technology-selection rationale was discussed.
- **Alternatives considered:** No specific technical alternatives were approved.
- **Consequences/tradeoffs:** Post-import camera lookup must work offline; local handling is a preference requiring explicit resolution of any exception. Route lifetime, external processing, and screen controls remain undecided.

## DEC-006 — Keep engineering standards universal

- **Status:** CONFIRMED.
- **Context:** The owner rejected project-specific functionality in the engineering-principles document.
- **Decision:** Keep [Engineering Principles](00-engineering-principles.md) reusable across all projects and maintain product behavior elsewhere. It is not modified in this documentation pass.
- **Related requirements:** No new product requirement; applies to document ownership and engineering practice.
- **Recorded rationale:** Establish a permanent, technology-agnostic standard for readable, maintainable, testable code.
- **Alternatives considered:** The prior mixed product/principles document was explicitly rejected.
- **Consequences/tradeoffs:** Product commitments must remain traceable in product documents even when removed from engineering standards.

## DEC-007 — Preserve filenames and consolidate authority

- **Status:** CONFIRMED documentation policy; file-role mapping implements the current task instruction.
- **Context:** The owner requested coordinated documentation, existing equivalent filenames, and a single requirements authority. The repository has separate empty business and functional requirement files plus domain/API placeholders.
- **Decision:** Retain filenames. [02-business-requirements.md](02-business-requirements.md) serves as the requested product requirements authority; [03-functional-requirements.md](03-functional-requirements.md) contains traceability only. Existing domain and API documents have narrow supporting responsibilities under architecture. The full mapping is in [documentation ownership](02-business-requirements.md#documentation-ownership).
- **Related requirements:** All FR/NFR definitions and references.
- **Recorded rationale:** The current task requires preservation of equivalents and avoidance of duplicate authoritative definitions.
- **Alternatives considered:** The owner supplied suggested replacement filenames while allowing equivalents; no separate file-renaming decision was requested.
- **Consequences/tradeoffs:** Some filenames are broader or narrower than their displayed titles, so the ownership map is explicit. No duplicate replacement files are created.

## DEC-008 — Technical structure proposal

- **Status:** PROPOSED; not approved or implemented.
- **Context:** Architecture and sequencing are requested, but technologies, persistence, recognition, matching semantics, and specific UI organization have not been selected.
- **Proposal:** Evaluate the minimal responsibility boundaries in [Architecture](05-architecture.md), the interaction proposals in [User Experience](04-ux-spec.md), and the staged sequence in [Implementation Plan](08-implementation-plan.md).
- **Related requirements:** FR-001–FR-011 and NFR-001–NFR-003.
- **Proposed rationale:** Keep core behavior testable while isolating actual media and storage differences without unnecessary layers.
- **Options for future consideration:** Storage, recognition, and normalization options and their tradeoffs are documented in architecture. They were not previously evaluated or selected.
- **Consequences/tradeoffs:** Owner decisions and source evidence are needed at the listed gates. No backend, dependencies, automatic counting, accessibility specification, or durable retention policy is approved by this entry.

## Pending decisions

The authoritative [open-question register](02-business-requirements.md#open-questions-and-blockers) owns unresolved product questions and their blocking impact. Technical options remain in architecture. When a decision is made, add or update a record with actual rationale and update requirements first if behavior changes. Do not manufacture approval or assign FR/NFR identifiers to proposals merely to close a documentation gap.
