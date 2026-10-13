# Implementation Plan

## Purpose and status

Owns incremental development sequencing, dependencies, deliverables, and completion gates. It does not define new product behavior. [Product Requirements](02-business-requirements.md) is authoritative, [Architecture](05-architecture.md) contains technical proposals, and [Testing Strategy](09-test-strategy.md) defines verification evidence.

This is a **PROPOSED execution sequence** for the confirmed MVP, not a report of completed implementation. No source code was inspected or implemented for this documentation task. No deadlines, effort estimates, selected technologies, or passed tests are implied. An unresolved question may permit a narrow experiment while still blocking milestone acceptance; experiments must not be presented as completed features.

## M-01 — Resolve evidence and design gates

- **Objective:** Establish enough evidence to implement without guessing at source formats or product rules.
- **Scope/requirements:** Readiness for FR-001–FR-011 and NFR-001–NFR-003; this milestone does not deliver those features.
- **Dependencies:** Owner-supplied representative screenshots/recordings and responses to relevant Q-01–Q-08.
- **Deliverables:** Reviewed source examples, decisions on blocking behaviors, approved technical/UX choices needed for the next increment, and updated authoritative criteria where decisions add detail.
- **Verification:** Check examples against A-01 and maintain traceability when decisions change requirements.
- **Completion:** Enough questions are resolved for the next milestone; remaining gates retain explicit owners and blocking scope. Synthetic data may support exploration but does not close Q-01.

## M-02 — Route list, search, and corrections

- **Objective:** Produce a working route-view and text-lookup increment using controlled sample data before media integration.
- **Scope/requirements:** FR-003, FR-005, FR-007; applicable NFR-001/NFR-003 constraints.
- **Dependencies:** Relevant Q-03/Q-04 decisions and an approved minimal route-state approach. Approved fixture data can stand in for import during development only.
- **Deliverables:** List, search, correction interactions, and associated automated tests; no claim of import completion.
- **Verification:** TST-003, TST-005, TST-007; applicable quality gates.
- **Completion:** Agreed behavior works with controlled inputs, corrections are observable, and unresolved validation cases are not hidden behind hardcoded behavior.

## M-03 — Worker-managed checklist

- **Objective:** Make found-package progress useful for preparation and review.
- **Scope/requirements:** FR-008, FR-009, FR-010; NFR-002 for this increment.
- **Dependencies:** M-02 and count-policy decisions under Q-04.
- **Deliverables:** Count editing and checklist presentation integrated with route entries; focused unit and interaction tests.
- **Verification:** TST-008, TST-009, TST-010; relevant offline portion of TST-013.
- **Completion:** Count changes, corrections, and completion transitions pass approved criteria; lookup never acts as implicit counting.

## M-04 — Camera lookup and clarification

- **Objective:** Identify a package's stop through the camera workflow.
- **Scope/requirements:** FR-004, FR-006; regression for FR-005/FR-008; NFR-002.
- **Dependencies:** M-02; approved Q-03/Q-05 semantics and a recognition option compatible with offline lookup. M-03 enables integrated count-nonmutation verification.
- **Deliverables:** Camera-to-match flow, candidate choice, agreed failure states, matching tests, and representative device checks.
- **Verification:** TST-004, TST-006, TST-008, and the lookup portion of TST-013.
- **Completion:** Correct and ambiguous examples are handled under agreed criteria; actual camera evidence complements deterministic tests.

## M-05 — Screenshot import

- **Objective:** Replace development-only route inputs with a worker-supplied screenshot workflow.
- **Scope/requirements:** FR-001 integrated with FR-003/FR-007; NFR-003.
- **Dependencies:** M-02, validated samples for Q-01, agreed import exceptions under Q-02, and any needed Q-08 decision.
- **Deliverables:** Screenshot intake, interpretation, correction handoff, and representative import fixtures/tests.
- **Verification:** TST-001, TST-003, TST-007, TST-014.
- **Completion:** Representative screenshot import passes approved criteria, including decided overlap and failure cases; synthetic success alone is insufficient.

## M-06 — Screen-recording import

- **Objective:** Deliver the second confirmed import method.
- **Scope/requirements:** FR-002 integrated with FR-003/FR-007; NFR-003.
- **Dependencies:** M-05's shared route interpretation where suitable; real recordings and Q-01/Q-02 decisions. Reuse is justified only where responsibilities align.
- **Deliverables:** Recording intake and interpretation integrated with the same route workflow; recording-specific tests.
- **Verification:** TST-002 with TST-003/TST-007 regressions and TST-014.
- **Completion:** Decided repeated-content, skipped-content, and unreadability cases have evidence. This milestone cannot be deferred from MVP without an explicit scope change.

## M-07 — Route lifecycle and data handling

- **Objective:** Complete the approved route-lifetime and deletion behavior and verify offline operation across the integrated product.
- **Scope/requirements:** FR-011, NFR-002, NFR-003; regression across FR-003–FR-010.
- **Dependencies:** Q-06/Q-08 decisions and M-02–M-06. Basic offline/privacy constraints apply throughout earlier milestones, not only here.
- **Deliverables:** Approved lifecycle/deletion implementation, any justified persistence, failure handling, and integrated offline/data-flow evidence.
- **Verification:** TST-011, TST-013, TST-014 and affected regression scenarios.
- **Completion:** Selected retention/deletion policy is tested; no assumed multi-route history or unapproved external processing is introduced.

## M-08 — Validate the complete preparation journey

- **Objective:** Establish MVP readiness with representative workflow and device evidence.
- **Scope/requirements:** FR-001–FR-011, NFR-001–NFR-003.
- **Dependencies:** Prior feature milestones, Q-07 support decisions, and all blockers relevant to claimed completion resolved.
- **Deliverables:** Integrated scenario results, compatibility checks, worker usability observations, issue disposition, and a clear limitations summary.
- **Verification:** TST-001–TST-014 plus the [end-to-end validation approach](09-test-strategy.md#journey-and-user-validation).
- **Completion:** Requirements and applicable engineering Definition of Done are satisfied. Failed or unexecuted checks are disclosed; blockers do not count as passing validation.

## Ongoing completion discipline

Each increment includes relevant tests, applicable validation execution, self-review, focused changes, and truthful evidence under [Engineering Principles](00-engineering-principles.md). Update [traceability](03-functional-requirements.md) with actual test references when they exist; do not invent paths or results. Automatic counting and individual-package duplicate detection are excluded from this plan.
