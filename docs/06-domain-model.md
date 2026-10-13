# Domain Model

## Purpose and status

Owns a small conceptual vocabulary shared by the documentation. It does not define database tables, classes, interfaces, or independent business rules. Behavior is authoritative only in [Product Requirements](02-business-requirements.md); technical state ownership is in [Architecture](05-architecture.md).

## Established terms

| Term | Meaning in the agreed product |
| --- | --- |
| Worker | The Amazon Flex worker preparing packages |
| Source media | Worker-provided route screenshots or one screen recording |
| Route | The collection of delivery information imported into the app |
| Route entry | An item associating address information, a stop number, an expected package count, and recorded progress; exact source grouping is still A-01/Q-01 |
| Address | The location text used for lookup, including meaningful unit details where present |
| Stop number | The delivery-order number shown to the worker for physical labeling; it is not automatically an app-internal unique identifier |
| Expected package count | The source-provided quantity assumed available under A-01 |
| Found count | The worker-recorded quantity for an entry; authoritative behavior is FR-008 |
| Completion | The checklist presentation governed by FR-009, not proof of physical possession or delivery completion |
| Package | The physical item the worker labels and organizes; individual package identity is outside confirmed MVP tracking |
| Candidate | A possible matching route entry awaiting clarification under FR-006 |

## Relationships and unresolved identity

A route contains entries; an entry links lookup information with worker-recorded progress. Source media supplies information used to form entries. Multiple physical packages can correspond to one entry. Address text alone cannot distinguish individual packages.

**OPEN QUESTION:** Q-01/Q-03 determine how source stops, addresses, and groups relate. Do not assume one address equals one stop or that address text is a unique key. Neither a route-entry identity scheme nor package identifier has been selected.

**PROPOSED technical direction:** Retain stable internal entry identity independently of editable address text if the chosen design needs it, so corrections do not accidentally redirect progress. This is an architecture consideration for approval, not a confirmed product identifier requirement.

## Ownership boundary

Count validation, edit effects, match rules, and deletion behavior belong to the requirements, including unresolved Q-04/Q-06. Storage representations belong to [Architecture](05-architecture.md#arc-04--persistence-and-deletion). This document must not introduce additional invariants to fill those gaps.
