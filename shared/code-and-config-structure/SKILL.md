---
name: code-and-config-structure
description: Check reader-first structure before reporting implementation or refactoring complete. Use whenever code or hand-maintained configuration is written or changed, and when reviewing their order.
---

# Code and Config Structure

Before reporting implementation or refactoring complete, review every in-scope file written or changed in the current task.

## Boundaries

1. In scope: normal source files; hand-maintained declarative maps such as `.editorconfig`, HCL/Terraform, INI, JSON, TOML, and YAML; and ignore-pattern files.
2. Do not reorganize generated artifacts, lockfiles, framework-mandated layouts, procedural configuration files, execution pipelines, or unrelated existing files.
3. For a review-only task, report clear ordering deviations. When the current task writes or changes an in-scope file, correct every clear, safe ordering deviation in that file before the final response. Do not ask for confirmation.
4. Follow this authority order: explicit user request; language, compiler, framework, and runtime requirements; repository formatter and linter rules; this skill; then existing order when no clear improvement remains.
5. Move complete declarations with their attached comments. Do not change behavior, signatures, visibility, settings, comments, or tool configuration solely to enforce this skill.

## Route

1. For source files or tests, read [source order](references/source-order.md).
2. For declarative maps or ignore-pattern files, read [configuration order](references/configuration-order.md).
3. Apply only clear, safe ordering improvements. Do not undo ordering imposed by the formatter or linter in the normal workflow.
4. Before the final response, review the final diff for clear ordering deviations, complete declaration moves, and unchanged behavior.
