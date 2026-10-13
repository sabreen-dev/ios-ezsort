# API and Boundary Contract Status

## Purpose and status

Owns the status of interface contracts and the questions needed before contracts can be specified. It does not prescribe a backend or duplicate product behavior. [Architecture](05-architecture.md) owns boundaries; [Product Requirements](02-business-requirements.md) owns observable semantics.

**CONFIRMED:** No remote service integration, endpoint, authentication scheme, or wire format has been agreed. The discussed import source is worker-provided media. No direct integration with Amazon systems has been authorized as product scope.

**OPEN QUESTION:** Whether any external processing is appropriate is Q-08. There are no approved API schemas to document. This is a deliberate unresolved status, not a claim that a backend has been ruled out permanently.

## Potential boundary contracts

The following are **PROPOSED contract topics**, not required interfaces or selected implementations. In-process functions may be sufficient. Detailed contracts should only be added when a real implementation boundary is justified.

| Boundary | Related requirements | Information to settle before specifying a contract |
| --- | --- | --- |
| Source interpretation to route state | FR-001, FR-002, FR-003, FR-007 | Source mapping, incomplete content, repeated captures, correction handoff: Q-01/Q-02/Q-04 |
| Address capture/filtering to matching | FR-004, FR-005, FR-006 | Address representation, candidate identity, variation semantics, failed reading: Q-03/Q-05 |
| Count edits to route state | FR-008, FR-009, FR-010 | Valid values, correction outcomes, overcounts: Q-04 |
| Route storage and deletion | FR-011, NFR-002, NFR-003 | Lifetime, atomicity needs, media scope, interrupted operations: Q-06 |
| Any future external processing | NFR-002, NFR-003 | Permitted data, purpose, network scope, retention, failures: Q-08 |

## Contract documentation expectations

When a boundary is approved, record its purpose, input/output meanings, valid inputs, failure and cancellation behavior, state effects, and requirement references. Externally consumed contracts additionally need compatibility and data-handling expectations. Follow [Engineering Principles](00-engineering-principles.md) without generating unused interfaces.

No endpoint names, request schemas, credentials, dependency choices, or fictitious service responses are established by this document. Approved contracts will be checked through [integration validation](09-test-strategy.md#test-organization-and-levels).
