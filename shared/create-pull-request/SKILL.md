---
name: create-pull-request
description: "Use when creating or opening a pull request. Builds it from the current branch using the repository template and required conventions."
---

# Create Pull Request

Use the repository's template when it exists. Otherwise, use [this skill's fallback template](assets/pull_request_template.md) so every PR follows the same minimum standard.

1. Inspect the current branch, intended base branch, included commits, and committed PR diff (`<base>...HEAD`). Infer the base branch when clear; otherwise, ask. If that committed diff is empty, explain that there is no PR to create and stop.
2. Inspect the worktree. Do not include or push uncommitted changes implicitly.
3. Detect the remote hosting platform. Use its current documented template convention to find the repository template. If more than one exists, ask which to use. If none exists, use [the fallback template](assets/pull_request_template.md). Do not modify the repository merely to install a template.
4. Draft a clear Conventional Commit title and complete the template from the diff: summarize what changed and why, then state material risk and a practical rollback path, or `No material risk.` Mark risk or rollback details as unknown when the available evidence does not establish them.
5. Publish the committed current branch if needed, then create the PR with the matching platform client, honoring a draft request. If credentials or remote access are unavailable, report the needed action.
6. Return the URL, base branch, title, and validation status: checks already run, checks not run, and pending CI.
