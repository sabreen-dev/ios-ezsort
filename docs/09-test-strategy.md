# Testing Strategy

## Purpose and status

Owns verification methods, test organization, risk coverage, and evidence gates. Acceptance criteria remain solely in [Product Requirements](02-business-requirements.md); this document references them rather than redefining them. [Engineering Principles](00-engineering-principles.md) supplies mandatory testing and self-review standards.

All TST references below are **planned verification scenarios**, not existing automated tests or executed results. Implementation and runtime behavior have not been verified in this documentation task. Test frameworks, tooling, supported device matrix, and performance thresholds are unselected.

## Test organization and levels

- Every module or class containing meaningful business logic must have appropriate automated unit tests. Prioritize lookup outcomes, candidate handling, count changes, completion, and correction effects once their rules are approved.
- Use consistent, descriptive test names communicating scenario and expected behavior. Organize files/classes so the corresponding production responsibility is easy to locate and navigate to; no framework or directory convention is mandated here.
- Keep unit tests deterministic and independent. Use controlled media-recognition outputs, timing, and storage doubles where appropriate without replacing the business behavior under test. Avoid asserting incidental call order or private structure.
- Integration tests target meaningful boundary risks: media interpretation to route entries, recognition to lookup, correction to active state, and storage/deletion if adopted. Verify actual adapters as well as isolated rules.
- UI/end-to-end tests target a small set of high-value journeys and state transitions. Physical camera input and device conditions also require representative device validation; deterministic simulated inputs alone cannot establish real recognition quality.
- Success, failure, edge-case, and boundary coverage is required for implemented behavior. Unknown outcomes must first be resolved in requirements, not invented by tests. No arbitrary coverage quota is imposed.

## Planned verification scenarios

Each row points to the authoritative acceptance criteria. Detailed fixture outcomes must be derived from those criteria and later approved resolutions of Q-01–Q-08.

| Reference | Requirement | Verification approach and principal risk |
| --- | --- | --- |
| TST-001 | FR-001 | Automated import integration with labeled screenshots; compare resulting entries to source truth. Add decided overlap, unreadability, and incomplete-source cases. Real sample coverage blocked by Q-01/Q-02. |
| TST-002 | FR-002 | Automated recording integration with known content; validate source fidelity across scrolling and repeated visibility once Q-01/Q-02 settle expected handling. |
| TST-003 | FR-003 | Route-to-presentation integration and UI checks for field association; include repeated-address examples after grouping decisions. |
| TST-004 | FR-004 | Unit/integration tests of recognized-address outcomes plus camera/device checks; verify the displayed stop and absence of implicit count changes. |
| TST-005 | FR-005 | Deterministic query-filter tests and UI typing/clear checks; apply only approved matching semantics. |
| TST-006 | FR-006 | Candidate-result unit tests and UI selection checks; ensure ambiguity is not silently resolved and chosen entry identity is retained. |
| TST-007 | FR-007 | Edit/state integration and UI confirmation of current values; validation and progress interactions await Q-04. |
| TST-008 | FR-008 | Unit tests for explicit updates and corrections; repeat scan/search interactions without count edits; invalid/overcount cases await Q-04. |
| TST-009 | FR-009 | Unit and presentation checks for single-package and multi-package progression, completion, and correction back to incomplete. |
| TST-010 | FR-010 | Checklist UI/journey checks for distinguishing incomplete and complete entries; inspect discrepancy wording against authoritative limitations. |
| TST-011 | FR-011 | Deletion integration/UI checks; inject storage failures if applicable. Final retention and interrupted-deletion outcomes await Q-06. |
| TST-012 | NFR-001 | Execute agreed workflows on the approved device/version matrix; compatibility completion blocked by Q-07. |
| TST-013 | NFR-002 | Disable network access after route import and exercise the applicable lookup, clarification, count, and review acceptance criteria. Use actual recognition capability in device validation. |
| TST-014 | NFR-003 | Review implemented data flows/dependencies, inspect logs for sensitive content, and verify storage/network behavior against approved handling. Use automated assertions where meaningful and manual inspection where necessary; final scope depends on Q-06/Q-08. |

## High-risk and unresolved scenarios

**Planned risk coverage:** Similar addresses and units; the same address under different stops; multiple packages at one address; repeated scans; inaccurate counts; corrections after completion; repeated or omitted media content; recognition failure; interrupted asynchronous work; and resource cleanup. The [question register](02-business-requirements.md#open-questions-and-blockers) owns unresolved expected outcomes.

Concurrency, cancellation, stale results, and resource-leak tests follow the actual design risks and engineering principles. They do not establish new user-facing recovery requirements. Retention across restarts and replacement of a route cannot be tested against an invented policy.

## Test data

**PROPOSED approach:** Use synthetic addresses and controlled route fixtures for deterministic rule tests. Maintain expected source-to-entry mappings for import examples. Obtain representative owner-provided samples for fidelity validation and handle customer information according to NFR-003 and engineering standards; avoid exposing such content in reports or logs. A synthetic fixture is not evidence that actual route media can be parsed.

Do not assume anonymization preserves every layout detail; review the usefulness of altered fixtures. Source fields and grouping remain A-01 until validated. No real route examples are currently available.

## Journey and user validation

Exercise the agreed [UX journeys](04-ux-spec.md): import, locate a stop by either lookup method, physically label/organize, explicitly update progress, review incomplete entries, and delete the route under the approved lifecycle policy. Automated UI coverage should verify observable app behavior; labeling a physical package and ease of package retrieval need observed worker use.

**PROPOSED evaluation:** Observe representative preparation tasks and discuss whether lookup reduces repeated scrolling, whether stop numbers and progress are understandable, and whether ambiguity leads to mistakes. These observations evaluate [vision outcomes](01-product-vision.md#high-level-success-criteria), not invented numerical release thresholds. Accessibility and latency acceptance commitments require Q-07 resolution.

## Quality gates and evidence

Before claiming an increment verified:

1. Link changed behavior to FR/NFR criteria and the relevant scenario reference.
2. Resolve questions that block the behavior being claimed; disclose any remaining blocked scope.
3. Execute applicable unit, integration, UI, device, and analysis checks appropriate to the change. Do not substitute a plan for execution.
4. Review results, address defects, and complete the mandatory contributor self-review.
5. Report executed checks, environment and fixture basis, outcomes, skipped/unexecuted checks, and limitations. Add actual test references to traceability when available.

Successful final validation requires evidence for all confirmed MVP requirements and agreed criteria, including real import samples and offline device use. No requirement is considered passed merely because a scenario is listed here. Unresolved privacy, support, or exception policies remain explicit blockers to the relevant completion claim.
