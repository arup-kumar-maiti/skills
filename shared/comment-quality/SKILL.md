---
name: comment-quality
description: "Review comments, including docstrings, in changed author-maintained implementation and configuration files before reporting completion, or when the user requests comment review."
---

# Comment Quality

Review comments in author-maintained implementation and configuration files written or changed during the current task, or in files the user explicitly names for comment review.

Tooling decides the required documentation shape. This skill adds the minimum useful meaning where documentation is required or a comment provides context the file cannot convey.

1. In scope: comments, including docstrings, in author-maintained source, configuration, CI, build, infrastructure, shell, SQL, and template files. This includes hidden markup comments in authored documentation and templates.
2. Do not rewrite visible user-facing documentation prose unless the user asks.
3. Out of scope: generated, vendored, dependency, lockfile, and build-output files. Do not inspect or modify them through this skill.
4. Preserve and honor comments that mark generated content, tool ownership, or file management, including `Managed by repo-standards`. Do not treat them as ordinary comments to triage.
5. Do not edit a generated or managed file through this skill. If the user explicitly asks, use its owning workflow; this skill does not authorize or configure that workflow.
6. For editable comments, follow this authority order: explicit user request; required ownership, generated-file, and tool comments; repository tooling and conventions; then this skill.
7. Inspect the active formatting, linting, documentation, and language conventions for each in-scope changed file. Treat their requirements as the required comment shape.
8. Classify each existing or candidate comment:
   - Keep durable rationale, invariants, external constraints, safety boundaries, deliberate trade-offs, and compact mental models for complex logic.
   - Rewrite useful but vague, stale, or misleading comments.
   - Remove comments that only narrate code, keys, types, parameters, return values, or obvious control flow when no applicable convention requires them and they do not state a non-obvious contract.
9. Add a comment or docstring only when important context cannot be conveyed by the file itself.
10. When tooling requires documentation, write the smallest useful compliant form.
11. Add documentation sections only when required or when they communicate non-obvious behavior, side effects, failures, or contracts.
12. Prefer clear code normally, but do not refactor solely to eliminate a comment.
13. Modify only comments added or changed in the current task, or comments directly affected by its implementation. Report unrelated pre-existing comments instead of modifying them unless the user asks for a broader cleanup.
14. Let the normal repository validation workflow verify comment changes. Do not add, remove, weaken, or replace formatting, linting, or documentation rules.
