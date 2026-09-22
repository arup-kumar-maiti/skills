---
name: implementation-simplicity
description: "Review implementation and its affected test surface before reporting completion to avoid needless complexity and redundant tests. Use whenever code or tests are added or changed, or when the user requests a review, audit, or report-only assessment of implementation code or tests."
---

# Implementation Simplicity

Keep the implementation as small as the requested behavior safely permits. Fewer lines alone are not a goal.

1. In scope: author-maintained implementation code and tests.
2. Do not use this skill to format or reorder code, review comments or prose, or change linting, testing, or CI configuration.
3. Do not change code solely to match an existing style, naming convention, abstraction pattern, or preference.
4. Inspect the changed code and tests, or the user-requested audit area, plus enough of the affected implementation surface to establish the contract, callers, callees, shared abstractions, data flow, and existing coverage.
5. There is no fixed file or line limit; stop expanding the review once that context is sufficient.
6. Question every new abstraction, helper, dependency, state holder, branch, conversion, option, feature flag, and parallel implementation.
7. Keep a new moving part only when current behavior, risk, or clarity requires it.
8. Reuse, extend, or replace an existing repository primitive when that yields the clearer fit.
9. Preserve existing behavior unless the user authorizes a compatibility change.
10. Remove replaced or demonstrably dead code.
11. Consolidate only behavior that is semantically equivalent.
12. Do not create a generic abstraction for one use case or force unrelated code together.
13. Add tests only for distinct observable behavior, meaningful boundaries, failure modes, regressions, or integration seams.
14. Do not add tests that mirror implementation details, repeat framework or library behavior, or duplicate an already-proven contract.
15. Parameterize only when each case represents a distinct contract or risk.
16. Simplify or remove a superseded test only when its needed behavior remains covered.
17. Preserve compatibility, security, concurrency, error-handling, and regression coverage.
18. Consider runtime efficiency only when there is credible cost or a relevant hot path.
19. Do not micro-optimize.
20. For performance-motivated changes, do not replace an algorithm without evidence.
21. Make only clear, behavior-preserving simplifications.
22. Never remove validation, error handling, security controls, observability, compatibility behavior, or necessary tests merely to reduce code.
23. Treat review, audit, report-only, and "do not edit" requests as non-mutating.
24. For those requests, report findings only. Make changes only when the user asks.
25. When the user requests implementation or change, automatically modify changed code and any existing implementation or tests directly affected by the task, including code replaced, consolidated, or adapted to preserve behavior.
26. Run the repository's normal validation relevant to the changed implementation and tests.
27. Do not add, remove, weaken, or replace repository checks.
