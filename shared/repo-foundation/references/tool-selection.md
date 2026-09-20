# Tool Selection

Apply this once for each detected or explicitly requested language or format.

1. Inspect the language or format's current established formatter and linter ecosystem. Prefer maintained, broadly adopted tools with a managed pre-commit hook; do not select tools from memory when current documentation can resolve the choice.
2. Reuse one tool when it supports multiple selected file types without weakening their linting or formatting coverage. Do not add overlapping tools for the same role.
3. Use the tool's stable comprehensive baseline: its documented recommended rules when that is the maintained standard, or its explicit all-rules option when the tool provides one intended for normal use. Do not enable an unstable `all` preset merely because it is named `all`. A parser-only syntax check is not a linter; add one only when it covers a gap in the selected linter.
4. Configure only documented, intentional exclusions. Keep generated, vendored, dependency, build-output paths, and lockfiles out of hooks; keep all first-party source, configuration, and documentation in scope.
5. For tools needing a runtime that pre-commit cannot bootstrap, provision the repository's established runtime; if none is established, use that tool's standard project-local setup without asking the user.
6. If no maintained formatter or linter can be safely selected, report that language or format and do not invent a tool or configuration.
