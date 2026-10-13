# Product Vision

## Purpose and ownership

This document owns product purpose, target users, goals, direction, and high-level success criteria. Detailed behavior and acceptance criteria belong exclusively to [Product Requirements](02-business-requirements.md); interactions belong to [User Experience](04-ux-spec.md). The [documentation ownership map](02-business-requirements.md#documentation-ownership) explains all existing filenames and responsibilities.

## Product overview and value proposition

**CONFIRMED:** An iOS application for Amazon Flex workers that helps them identify the delivery stop number associated with a package address and organize packages before leaving the station.

Workers provide route screenshots or a single screen recording. An in-app route list supports camera address lookup, manual search, and a worker-managed package checklist. The value is less time locating stop numbers during preparation and less searching for packages during delivery.

## Target users and problem

The intended users are Amazon Flex workers handling packages under time pressure at the station. They need to associate packages with delivery numbers, arrange them in delivery order, and notice possible discrepancies before departure.

The product owner describes repeatedly reading a package address and scrolling through the Amazon Flex route list to find its stop number. The reported lack of a quick address search makes this repetitive task inefficient. This is the owner's description of the problem, not an independently verified statement about the current Amazon Flex application.

Poor preparation can also make packages harder to locate at delivery stops. A clear account of packages found can help workers investigate what might be missing or extra while still at the station.

## Product goals

- Reduce the time and effort spent associating packages with delivery stops.
- Help workers label and organize packages by delivery number.
- Make package retrieval easier during deliveries through better preparation.
- Help workers see where expected packages remain unaccounted for.
- Offer a fast, clear experience suitable for someone handling packages.

## High-level MVP scope

**CONFIRMED:** Both screenshot and single-screen-recording import; an in-app route list; camera address lookup; manual address search; clarification of ambiguous matches; correction of imported information; worker-managed counts and completion indicators; pre-departure review; offline lookup and checklist use after import; and route privacy and deletion.

The app supports the worker's judgment about discrepancies. Its initial checklist does not independently verify possession of individual packages.

## Product direction and boundaries

Automatic package counting and duplicate-package scan detection are **PROPOSED future opportunities**, explicitly outside the MVP. No future release is committed. A unique package identifier was discussed as a possible way to distinguish packages, not as a selected solution.

**WORKING ASSUMPTION:** The source material exposes addresses, stop numbers, and expected package counts. A real sample is still needed. The authoritative [assumptions and open questions](02-business-requirements.md#assumptions-and-open-questions) govern this uncertainty; technical choices remain in [Architecture](05-architecture.md).

## High-level success criteria

Success means workers can prepare packages with less effort than repeated manual scrolling, identify the correct delivery numbers, understand incomplete checklist entries, and retrieve organized packages more easily during delivery. Workers should be able to continue lookup and checklist use after import without internet access.

These are intended outcomes, not achieved results. No numerical speed or time-saving targets have been agreed. [Testing Strategy](09-test-strategy.md) owns the validation approach; requirements own testable acceptance criteria.
