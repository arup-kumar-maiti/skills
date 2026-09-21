# Scope

1. In a Git repository, run `git ls-files` before any general file-discovery command.
2. Use only its output as the candidate file list for classifying languages and authored formats.
3. If Git is unavailable, use the working tree as the candidate file list.
4. Inspect before modifying anything:
   - root and workspace-level package/build manifests, lockfiles, and language configuration from that candidate file list;
   - existing formatter, linter, pre-commit, Cocogitto, hook, and CI configuration from that candidate file list; and
   - generated, vendored, dependency, and build-output paths.
5. In a Git repository, use `git ls-files --others --exclude-standard` only to find configuration files at paths this skill would create.
6. Treat those files as user-owned conflicts.
7. Do not use that command's output to select languages, formats, tools, additions, replacements, or removals.
8. Classify every language and authored markup or configuration format in the candidate file list, plus explicit user selections.
9. Treat a language or format found only in generated, vendored, dependency, or build-output paths as out of scope.
10. Treat every invocation as reconciliation of the complete detected scope. A language or format newly present in the candidate file list expands that scope automatically; one no longer present contracts it.
11. Present one compact summary:
   - detected and requested languages and formats;
   - the selected combined formatter and linter suite;
   - existing user-owned tooling to preserve;
   - proposed additions, replacements, and removals; and
   - conflicts requiring a decision.
12. For a blank repository, ask which languages and authored formats it should contain. The answer may include multiple values.
13. In a nonblank repository, use the scope derived from the candidate file list without confirmation.
14. Ask before modifying files only when existing user-owned tooling conflicts.
15. In a blank repository, the user's selection is that confirmation.
