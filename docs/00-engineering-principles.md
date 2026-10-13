# Engineering Principles

## Purpose and requirement language

This document establishes reusable standards for engineering software of any size, in any language, platform, framework, or domain. The priority is code that a human engineer can readily read, understand, review, debug, test, and maintain.

- **MUST** indicates a mandatory requirement.
- **SHOULD** indicates a recommended default. Departures require a concrete reason and an explanation of the tradeoff in the code review or relevant documentation.
- **MUST NOT** indicates a prohibited practice.

Apply requirements wherever the relevant concern exists. These standards do not require adding infrastructure, architectural layers, or features merely to demonstrate compliance.

## 1. Engineering philosophy and architecture

- Implementations MUST favor readability and maintainability over cleverness.
- Architecture MUST be proportional to demonstrated complexity, risk, and current requirements. A small program may need only a few cohesive functions or modules.
- Designs SHOULD apply pragmatic Clean Architecture: keep business policy independent of incidental presentation, persistence, and external-service details where those dependencies impede understanding, testing, or change. This does not prescribe a layer count, directory template, or framework.
- Code MUST separate distinct concerns, keep related behavior together, and minimize coupling between responsibilities. Dependencies and module boundaries MUST be understandable.
- Designs SHOULD apply SOLID principles proportionally:
  - **Single responsibility:** group behavior that changes for the same reason; separate unrelated responsibilities.
  - **Open/closed:** provide extension points for established variation without speculative extensibility.
  - **Liskov substitution:** replacements must preserve the behavioral contract expected by callers.
  - **Interface segregation:** expose focused contracts without forcing consumers to depend on unrelated operations.
  - **Dependency inversion:** where appropriate, make policy depend on stable contracts rather than volatile implementation details.
- Code SHOULD follow DRY (Don't Repeat Yourself): keep each business rule or piece of knowledge authoritative in one place. Similar syntax alone does not justify a shared abstraction.
- Designs MUST follow KISS (Keep It Simple) and YAGNI (You Aren't Gonna Need It): choose the simplest clear solution that satisfies established needs, and omit speculative capabilities.
- Composition SHOULD be preferred over inheritance when it makes behavior and dependencies clearer. Inheritance MUST preserve a meaningful substitutable relationship.
- Contributors MUST NOT introduce interfaces, abstractions, layers, or indirection without an identifiable benefit to current correctness, clarity, testing, or maintainability.

## 2. Naming conventions

- Identifiers MUST be clear, descriptive, and unambiguous in their context. Class, method, function, variable, constant, and file names MUST communicate their actual responsibility or meaning.
- Names MUST accurately reflect behavior, including meaningful distinctions between querying, mutating, validating, and performing external operations.
- Code and documentation MUST use consistent domain terminology. The same concept MUST NOT acquire different names without a meaningful distinction.
- Names MUST follow the applicable language conventions and established project conventions where compatible with these standards.
- Contributors MUST NOT use cryptic abbreviations or generic names that conceal purpose. Standard abbreviations are acceptable only when their meaning is clear to the intended reader.

## 3. Documentation and comments

- Every nontrivial method or function MUST have a concise documentation comment describing its purpose, behavior, and relevant parameters. Nontrivial behavior includes business rules, branching that requires interpretation, side effects, non-obvious constraints, or meaningful failure conditions.
- Documentation MUST describe return values, side effects, failure conditions, and usage constraints when callers need that information to use the operation correctly.
- Public APIs MUST document their contracts, including relevant input expectations, outputs, errors, and lifecycle obligations.
- Complex algorithms, non-obvious data transformations, important business rules, significant assumptions, unusual implementation decisions, and significant tradeoffs MUST be documented near the code or in directly discoverable supporting documentation. Documentation MUST explain the intent and reasoning behind the implementation rather than merely restate the code.
- Comments SHOULD explain why a decision exists rather than narrate obvious operations.
- Contributors MUST update or remove comments when behavior changes and MUST NOT leave misleading, redundant, or excessively verbose documentation.

## 4. Code structure and complexity

- Methods and functions MUST remain small enough to understand as a focused operation. Classes and modules MUST have cohesive, clearly defined responsibilities.
- Control flow MUST be readable. Contributors SHOULD reduce nesting and use early returns where they make normal and exceptional paths easier to follow.
- Code MUST NOT contain god classes, unnecessarily long methods, convoluted logic, or clever one-liners that sacrifice readability.
- Non-obvious literal values MUST have meaningful names or an explanation of their origin and purpose.
- Code MUST NOT retain dead code, obsolete branches, unused declarations, or commented-out implementations.
- Contributors MUST assess complexity by the effort required to understand and change the code, not arbitrary limits on lines, methods, or class size.

## 5. Testing and quality assurance

- Every class or module containing meaningful business logic MUST have appropriate automated unit tests.
- Tests MUST cover successful behavior, failures, edge cases, and relevant boundaries. Changes to behavior MUST include corresponding test additions or updates.
- Tests MUST be deterministic and independent. They MUST NOT rely on execution order or uncontrolled shared state.
- Test names MUST follow a consistent, descriptive convention that clearly communicates the scenario and expected behavior.
- Tests MUST be logically organized, with files and classes clearly associated with their corresponding production components. The organization MUST make navigation between implementation and tests straightforward without requiring a particular framework or directory structure.
- Tests SHOULD verify observable behavior and contracts rather than private structure or incidental implementation details.
- Mocks and fakes SHOULD isolate nondeterminism, expensive operations, or external boundaries. They MUST NOT replace the business behavior being tested or impose irrelevant internal call sequences.
- Integration tests MUST cover component interactions that introduce meaningful risk, including incompatible contracts or behavior that isolated tests cannot establish.
- Contributors MUST NOT create meaningless assertions or duplicate implementation logic merely to increase coverage. Coverage metrics do not establish correctness by themselves.
- Relevant available tests and validation checks MUST be executed before reporting work as verified. Reports MUST distinguish passed, failed, skipped, and unexecuted checks and disclose blockers.
- Contributors MUST NOT claim that tests passed unless those tests were actually executed and produced passing results.
- All contributors, including AI coding agents, MUST perform a self-review before declaring implementation complete. The review MUST evaluate readability and clarity, naming conventions and consistency, method and class responsibilities, unnecessary complexity and abstractions, duplicated logic, correctness and potential defects, and compliance with these engineering principles. Identified issues MUST be resolved or explicitly disclosed as remaining limitations; disclosure does not make noncompliant work complete.

## 6. Error handling and reliability

- Error handling MUST be explicit and predictable. Operations MUST communicate failures through clear contracts and meaningful messages with enough context to diagnose the problem without exposing sensitive data.
- Code MUST NOT silently swallow exceptions, suppress errors or failures to conceal underlying problems, or report success after an unhandled failure. Intentional recovery or suppression MUST have a documented reason and an observable, appropriate outcome.
- Inputs MUST be validated at appropriate trust and system boundaries. Internal invariants MUST be enforced where invalid state could otherwise propagate.
- Missing, null, or absent values MUST be handled deliberately. Defaults MUST NOT disguise invalid data or failed operations.
- Resources MUST be released on success, failure, and cancellation paths.
- Operations SHOULD fail gracefully and preserve a consistent state. Recovery and retries MUST be bounded and safe for the operation, including the possibility of repeated side effects.

## 7. State management and concurrency

- Mutable state MUST have clear ownership and controlled mutation paths. State transitions and their invariants MUST be understandable.
- Data SHOULD be immutable where practical, and shared mutable state SHOULD be minimized.
- Asynchronous work MUST have defined ownership, completion and error handling, and appropriate cancellation and lifecycle management.
- Concurrent access MUST prevent race conditions and inconsistent updates through appropriate coordination or isolation.
- Implementations MUST prevent abandoned work, stale results, and resource leaks from violating correctness or outliving their intended lifecycle.

## 8. Security and performance

- Implementations MUST use secure defaults and grant only the access needed for their responsibilities.
- Sensitive data MUST be protected during handling, storage, and transmission as applicable. Code MUST NOT hardcode credentials or secrets or expose sensitive data in logs or error messages.
- External input MUST be treated as untrusted and validated before use. Validation MUST NOT substitute for authorization where access control is required.
- Dependencies MUST be justified, obtained from trusted sources, and reviewed for maintenance, security, licensing, and compatibility risks. Known risks MUST be addressed or explicitly documented for resolution.
- Code MUST use resources responsibly and avoid evident waste, unbounded accumulation, and unnecessary repeated work.
- Performance changes SHOULD be driven by requirements and measurements. Contributors MUST NOT sacrifice clarity for speculative optimization; necessary tradeoffs MUST be explained and verified.

## 9. Consistency and maintainability

- Formatting, organization, terminology, and conventions MUST be consistent within a project. Contributors MUST use established formatting and analysis tools when available.
- Files and directories MUST follow a predictable structure that makes responsibilities and related code easy to locate.
- Module boundaries and dependency direction MUST be clear. Internal details SHOULD remain encapsulated behind the smallest useful contract.
- Dependencies MUST be kept to what the solution needs. Contributors SHOULD prefer existing suitable capabilities before adding another dependency.
- Code MUST communicate intent without requiring excessive investigation across unrelated files, hidden side effects, or undocumented assumptions.
- Contributors MUST NOT introduce unexplained temporary workarounds, use hardcoded behavior to bypass actual requirements, present placeholders as complete functionality, or apply quick fixes that introduce unnecessary technical debt.
- A genuinely necessary temporary workaround MUST be clearly identified, justified, documented with its limitations, and linked to a tracked resolution item with explicit criteria for removal or replacement. Temporary solutions MUST NOT be represented as permanent or production-ready implementations.

## 10. AI-generated code standards

AI coding agents are subject to the same standards as human contributors. They MUST:

- Examine relevant instructions, existing code conventions, and tests before modifying code.
- Make focused, minimal changes sufficient to satisfy the requested scope, without unrelated refactoring.
- Avoid unnecessary dependencies, abstractions, and speculative functionality.
- Document significant architectural decisions with their rationale and material tradeoffs.
- Create or update relevant tests and execute available validation appropriate to the change.
- Report exactly what was implemented and verified, including test results, assumptions, incomplete work, limitations, and blocked checks.

Agents MUST NOT fabricate functionality, tool execution, test outcomes, or other verification results. Unverified work MUST be identified as unverified.

## 11. Definition of done

Before declaring work complete, the contributor MUST review this checklist and provide evidence appropriate to the change:

- [ ] Requirements are satisfied, and the implementation remains within the requested scope.
- [ ] Code is readable and maintainable, with clear responsibilities, control flow, and naming.
- [ ] The mandatory self-review in Section 5 is complete, and its findings have been resolved or explicitly disclosed.
- [ ] Documentation and comments accurately explain relevant behavior and contracts.
- [ ] Meaningful automated tests cover new or changed business behavior and relevant risks.
- [ ] Applicable verification has succeeded, or blockers and unexecuted checks are explicitly disclosed. Blocked verification MUST NOT be described as a fully verified result.
- [ ] Errors, invalid inputs, absent values, resource cleanup, and applicable concurrency concerns are handled appropriately.
- [ ] No unnecessary complexity, dependencies, dead code, or unrelated changes remain.
- [ ] Applicable security and performance concerns have been addressed.
- [ ] A clear implementation summary explains the changes, validation results, and remaining limitations.

Items that do not apply to the change MUST be marked as not applicable with a brief reason rather than used to justify unnecessary work. Disclosing a blocker does not waive an unmet requirement.
