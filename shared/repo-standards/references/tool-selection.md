# Tool Selection

Apply this to the complete detected or explicitly requested scope, not separately to each language or format.

1. For each selected language or format, inspect its current established formatter and linter ecosystem. Prefer maintained, broadly adopted tools with a managed pre-commit hook; do not select tools from memory when current documentation can resolve the choice.
2. Choose one combined formatter and linter suite from those candidates.
3. Reuse one tool when it supports multiple selected file types without weakening their linting or formatting coverage.
4. When several tools remain suitable, prefer the established tool for that language or format.
5. Choose a cross-language tool only when it provides equivalent coverage for every selected type it replaces and reduces the total managed hook environments.
6. Do not add overlapping tools for the same role.
7. With unchanged complete scope, retain the existing managed suite and its exact pinned versions.
8. When the scope changes, re-evaluate the combined suite; retain the pins of tools that remain and pin newly selected tools.
9. Reconsider version upgrades only when the user explicitly requests a tooling update.
10. Use the tool's stable comprehensive baseline: its documented recommended rules when that is the maintained standard, or its explicit all-rules option when the tool provides one intended for normal use. Do not enable an unstable `all` preset merely because it is named `all`.
11. A parser-only syntax check is not a linter; add one only when it covers a gap in the selected linter.
12. Configure only documented, intentional exclusions. Keep generated, vendored, dependency, build-output paths, and lockfiles out of hooks; keep all first-party source, configuration, and documentation in scope.
13. Declare every runtime that pre-commit cannot bootstrap in repository and CI configuration. If an optional machine-level runtime is unavailable locally, do not install it or request confirmation; report the pending local check after verification.
14. If no maintained formatter or linter can be safely selected, report that language or format and do not invent a tool or configuration.
