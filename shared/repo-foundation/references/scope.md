# Scope

1. Inspect before modifying anything:
   - first-party tracked files and their extensions; if Git is unavailable, inspect the working tree instead;
   - root and workspace-level package/build manifests, lockfiles, and language configuration;
   - existing formatter, linter, pre-commit, Cocogitto, hook, and CI configuration; and
   - generated, vendored, dependency, and build-output paths.
2. Classify every detected or explicitly requested programming language and authored markup or configuration format.
3. Treat a language or format found only in generated, vendored, dependency, or build-output paths as out of scope.
4. Present one compact summary:
   - detected and requested languages and formats;
   - selected formatter and linter for each in-scope language or format;
   - existing tooling to preserve;
   - proposed additions; and
   - conflicts.
5. For a blank repository, ask which languages and authored formats it should contain. The answer may include multiple values.
6. Before modifying files, ask for scope confirmation only when the requested languages or formats are unclear or existing tooling conflicts. In a blank repository, the user's selection is that confirmation.
