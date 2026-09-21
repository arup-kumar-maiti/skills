# Common Standards

Apply these after language and tool selection is confirmed.

## Managed Files

1. Create managed formatter/linter configuration only at documented, comment-capable locations. Do not use a strict JSON file or package manifest as a managed configuration.
2. Mark every formatter/linter configuration and pull-request workflow created by this skill with `Managed by repo-standards`, using the file format's comment syntax.
3. On a later run, regenerate a marked file from the complete selected suite.
4. Add needed configuration and remove obsolete managed hooks, dependencies, and workflow steps.
5. If a marked file's rendered content is unchanged, do not modify it.
6. When generated configuration fails a selected formatter or linter, first change that configuration to satisfy the baseline.
7. If documented syntax or tool compatibility makes that impossible, use the narrowest file- and rule-specific exception and explain it beside the exception.
8. Preserve every unrelated baseline rule. Never relax a global rule solely to pass generated output.
9. Treat an unmarked existing formatter/linter configuration or pull-request workflow as user-owned. Ask before replacing or merging a conflict.
10. Update `.gitignore` only by adding required entries; never mark or regenerate it.
11. In managed YAML, omit optional `name` fields.
12. Retain workflow and job labels in generated CI workflows, and every `name` field required by its owning schema.

## Prerequisites

1. Verify that Python and Cocogitto are available.
2. If either is absent, present the required machine-level installation commands together.
3. Obtain one confirmation before running those commands.

## Managed Hooks

1. Use `.pre-commit-config.yaml` as the single formatter and linter hook configuration. Treat another manager for `pre-commit` or `commit-msg` as a conflict.
2. Configure every formatter and linter in a managed pre-commit environment with its exact stable version pinned.
3. Prefer a maintained external hook repository.
4. When a compatible maintained hook is unavailable, use `repo: local` with a managed language and pinned `additional_dependencies`.
5. Do not use `language: system` for formatter or linter hooks.
6. Let each hook's `types`, `types_or`, or `files` selector limit it to its matching selected files.
7. Use `.gitignore` as a discovery signal, not hook configuration.
8. Set a global `exclude` for generated, vendored, dependency, build-output paths, and lockfiles from the candidate file list without excluding first-party files.
9. Reuse one formatter tool for every selected file type it supports.
10. For every selected formatter, add one writing hook with `stages: [pre-commit]`.
11. For every selected formatter, add one matching non-mutating check hook with `stages: [manual]`.
12. For every selected linter, add one non-mutating hook with `stages: [pre-commit, manual]`.
13. Run linters without auto-fixing.
14. Within each language, place formatting before linting; place the Conventional Commit hook last.
15. If formatting changes files during a commit, let pre-commit abort it so the developer can review and stage the changes. Never auto-stage files.
16. Use an existing project Python environment for `pre-commit` when one is available.
17. Otherwise create `.venv` with `python -m venv`.
18. Add `.venv/` to `.gitignore`.
19. Install `pre-commit` in the selected project Python environment.
20. Do not install language tooling globally.
21. Run `pre-commit validate-config`.
22. Install the hooks with `pre-commit install --install-hooks --hook-type pre-commit --hook-type commit-msg`.

## Commit Messages

1. Add one `repo: local`, `language: system` `commit-msg` hook whose entry is `cog verify --file`. This exception is only for Cocogitto; it receives the commit-message filename from pre-commit.
2. Preserve an existing `cog.toml`; create one only when the repository needs non-default Cocogitto policy.

## Changed-File CI

1. Detect an existing versioned CI provider and the repository host before selecting a workflow target.
2. Extend the existing CI provider. If none exists, use the repository host's native CI convention.
3. If neither provider nor host can be identified safely, report CI setup as pending and do not create a workflow.
4. Configure pull-request CI to run the non-mutating `manual`-stage formatter and linter hooks against the pull request range.
5. Provision Cocogitto before the commit-range check.
6. When adding a GitHub Action reference to a managed workflow, select its current stable major version.
7. On later reconciliations, retain every managed GitHub Action major version. Upgrade one only when the user explicitly requests a tooling update.
8. For GitHub Actions, configure `cocogitto/cocogitto-action` with `command: check` and `args: <base-sha>..<head-sha>`.
9. On every CI platform, provision Python and every selected runtime that pre-commit cannot bootstrap, using repository-declared versions, then install `pre-commit`.
10. For GitHub Actions, run on `pull_request` activity types `opened`, `reopened`, and `synchronize`; check out the head SHA with full history.
11. For another CI platform, use its equivalent pull-request base and head SHAs with a checkout containing both revisions.
12. Check Conventional Commits only in the pull request's `<base-sha>..<head-sha>` range; do not validate older history.
13. Run:

```sh
pre-commit run --hook-stage manual --from-ref <base-sha> --to-ref <head-sha>
```

14. Do not add a full-program type check such as `tsc --noEmit`.

## Verification

1. Ensure `pre-commit` and `cog` are available, then run `pre-commit validate-config`.
2. Create temporary files outside the repository containing one valid and one intentionally invalid Conventional Commit message. Run `cog verify --file` against each; the valid result must succeed and the invalid result must fail. Remove both files afterward.
3. If a relevant first-party file is already staged, run `pre-commit run --hook-stage pre-commit`.
4. Never create a test commit or auto-stage files. If no suitable staged file exists, report that end-to-end hook verification is pending the next normal commit.
5. Do not weaken rules to hide existing failures.
