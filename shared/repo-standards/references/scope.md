# Scope

1. Build the candidate file list from every available regular working-tree file. Do not use Git tracking state or follow symlinks.
2. Every candidate-file discovery pass must honor repository ignore files and exclude `.git/`, generated, vendored, dependency, build-output, cache, virtual-environment, and lockfile paths.
3. Keep repo-standards-managed files in the candidate list so their formats can expand the selected suite.
4. Inspect before modifying anything:
   - root and workspace-level package/build manifests, lockfiles, and language configuration from the working tree;
   - existing formatter, linter, pre-commit, Cocogitto, hook, and CI configuration from the working tree; and
   - generated, vendored, dependency, and build-output paths.
5. Classify every language and authored markup or configuration format in the candidate file list, plus explicit user selections.
6. Treat a language or format found only in an excluded path as out of scope.
7. Reconcile to a fixed point:
   - discover the candidate file list, select the suite, and render managed configuration;
   - rediscover and reselect after each render; and
   - finish only when the selected suite and rendered managed files are unchanged.
8. If the scope or selected suite repeats without convergence, stop and report the cycle.
9. Present one compact summary:
   - detected and requested languages and formats;
   - the selected combined formatter and linter suite;
   - existing user-owned tooling to preserve;
   - proposed additions, replacements, and removals; and
   - conflicts requiring a decision.
10. For a blank repository, ask which languages and authored formats it should contain. The answer may include multiple values.
11. In a nonblank repository, use the scope derived from the candidate file list without confirmation.
12. Ask before modifying files only when existing user-owned tooling conflicts.
13. In a blank repository, the user's selection is that confirmation.
