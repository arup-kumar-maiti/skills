# Scope

1. Inspect before modifying anything:
   - first-party files returned by `git ls-files` and their extensions; if Git is unavailable, inspect the working tree instead;
   - root and workspace-level package/build manifests, lockfiles, and language configuration;
   - existing formatter, linter, pre-commit, Cocogitto, hook, and CI configuration; and
   - generated, vendored, dependency, and build-output paths.
2. In a Git repository, use `git ls-files --others --exclude-standard` only to find configuration files at paths this skill would create. Treat those files as user-owned conflicts. Do not use that command's output to select languages, formats, tools, additions, replacements, or removals.
3. Classify every detected or explicitly requested programming language and authored markup or configuration format.
4. Treat a language or format found only in generated, vendored, dependency, or build-output paths as out of scope.
5. Treat every invocation as reconciliation of the complete detected scope. A language or format newly present in `git ls-files` expands that scope automatically; one no longer present contracts it.
6. Present one compact summary:
   - detected and requested languages and formats;
   - the selected combined formatter and linter suite;
   - existing user-owned tooling to preserve;
   - proposed additions, replacements, and removals; and
   - conflicts requiring a decision.
7. For a blank repository, ask which languages and authored formats it should contain. The answer may include multiple values.
8. In a nonblank repository, use the scope derived from `git ls-files` without confirmation.
9. Ask before modifying files only when existing user-owned tooling conflicts.
10. In a blank repository, the user's selection is that confirmation.
