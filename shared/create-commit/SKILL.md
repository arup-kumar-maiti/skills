---
name: create-commit
description: "Use when the user asks to commit current changes."
---

# Create Commit

Create one or more Conventional Commits from the current Git changes.

1. Resolve the Git worktree root and verify that `cog` is available. If either is absent, report the requirement and stop. Do not create a commit.
2. Read `<worktree-root>/cog.toml` when it exists.
3. Start with Cocogitto's standard types, then add or override configured `commit_types`; only an empty configuration disables a standard type. Treat a declared `scopes` list as exhaustive. Without a configuration, use the standard types and an optional scope.
4. Inspect working-tree status plus staged and unstaged diffs. If no changes are available, say so and stop.
5. Inspect every candidate change before planning it: its diff for a tracked file or its contents for an untracked file. Do not include a change that appears to add sensitive data or whose relevance cannot be established; report it instead.
6. Partition the available changes into the smallest set of cohesive commits. Keep implementation, directly related tests, required configuration, and generated dependency updates together. Split only independently understandable, reviewable, and reversible changes; do not split merely because files differ.
7. Stop and return the proposed plan if it requires splitting different hunks in one file or a selected path has both staged and unstaged edits. Do not perform hunk-level staging or replace an intentional partial staging selection.
8. For each planned commit, decide whether it intentionally introduces a breaking compatibility change.
9. For each planned commit, choose the most specific allowed type and, only when useful and permitted, scope. Write a short, imperative summary.
10. If the index contains a staged path outside the plan, report it and stop.
11. For a multi-commit plan containing staged files, first unstage only the planned paths with `git reset -- <planned-paths>`; their working-tree contents remain unchanged.
12. For each planned commit in dependency order, stage only its paths with `git add -A -- <commit-paths>`.
13. Verify that the index contains exactly that commit's paths. If it does not, report the difference and stop.
14. Run `cog commit <type> [-B] "<summary>" [scope]`, using `-B` only for an intentional breaking change and omitting `[scope]` when unused. Cocogitto constructs and validates each title. Let existing hooks run.
15. If staging, Cocogitto, or a hook fails or changes files, report the failure or changed paths, then stop without retrying or altering the working tree automatically.
