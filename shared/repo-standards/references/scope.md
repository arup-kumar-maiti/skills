# Scope

1. Inspect before modifying anything:
   - first-party tracked files and their extensions; if Git is unavailable, inspect the working tree instead;
   - root and workspace-level package/build manifests, lockfiles, and language configuration;
   - existing formatter, linter, pre-commit, Cocogitto, hook, and CI configuration; and
   - generated, vendored, dependency, and build-output paths.
2. Classify every detected or explicitly requested programming language and authored markup or configuration format.
3. Treat a language or format found only in generated, vendored, dependency, or build-output paths as out of scope.
4. Treat every invocation as reconciliation of the complete detected scope. A newly tracked language or format expands that scope automatically; a no-longer-tracked one contracts it.
5. Present one compact summary:
   - detected and requested languages and formats;
   - the selected combined formatter and linter suite;
   - existing user-owned tooling to preserve;
   - proposed additions, replacements, and removals; and
   - conflicts requiring a decision.
6. For a blank repository, ask which languages and authored formats it should contain. The answer may include multiple values.
7. In a nonblank repository, use the detected tracked scope without confirmation. Ask before modifying files only when existing user-owned tooling conflicts. In a blank repository, the user's selection is that confirmation.
