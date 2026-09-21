# Common Standards

Apply these after language and tool selection is confirmed.

## Managed Files

1. Mark every formatter/linter configuration and pull-request workflow created by this skill with `Managed by repo-standards`, using the file format's comment syntax.
2. On a later run, regenerate a marked file from the complete selected suite.
3. Add needed configuration and remove obsolete managed hooks, dependencies, and workflow steps.
4. If a marked file's rendered content is unchanged, do not modify it.
5. When generated configuration fails a selected formatter or linter, first change that configuration to satisfy the baseline.
6. If documented syntax or tool compatibility makes that impossible, use the narrowest file- and rule-specific exception and explain it beside the exception.
7. Preserve every unrelated baseline rule. Never relax a global rule solely to pass generated output.
8. Treat an unmarked existing formatter/linter configuration or pull-request workflow as user-owned. Ask before replacing or merging a conflict.
9. Update `.gitignore` only by adding required entries; never mark or regenerate it.
10. In managed YAML, omit optional `name` fields.
11. Retain workflow and job labels in generated CI workflows, and every `name` field required by its owning schema.

## Prerequisites

1. Verify that Git, Python, and Cocogitto are available.
2. If any are absent, present the required machine-level installation commands together.
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
9. Reuse one formatter hook for every selected file type that its tool supports.
10. Set every writing formatter hook's `stages` to `[pre-commit]`.
11. Set every matching non-mutating formatter-check hook's `stages` to `[manual]`.
12. Set every linter hook's `stages` to `[pre-commit, manual]`.
13. Run linters without auto-fixing.
14. Within each language, place formatting before linting; place the Conventional Commit hook last.
15. If formatting changes files during a commit, let pre-commit abort it so the developer can review and stage the changes. Never auto-stage files.
16. Use an existing project Python environment for `pre-commit` when one is available.
17. Otherwise create `.venv` with `python -m venv`.
18. Add `.venv/` to `.gitignore`.
19. Install `pre-commit` in the selected project Python environment.
20. Do not install language tooling globally.
21. Install the hooks with `pre-commit install --install-hooks --hook-type pre-commit --hook-type commit-msg`.

## Commit Messages

1. Add one `repo: local`, `language: system` `commit-msg` hook whose entry is `cog verify --file`. This exception is only for Cocogitto; it receives the commit-message filename from pre-commit.
2. Preserve an existing `cog.toml`; create one only when the repository needs non-default Cocogitto policy.

## Changed-File CI

1. Configure pull-request CI to run the non-mutating `manual`-stage formatter and linter hooks against the pull request range.
2. On every CI platform, provision Python and every selected runtime that pre-commit cannot bootstrap, using repository-declared versions, then install `pre-commit`.
3. For GitHub Actions, run on `pull_request` activity types `opened`, `reopened`, and `synchronize`; check out the head SHA with full history and use each first-party action's current stable major version.
4. For another CI platform, use its equivalent pull-request base and head SHAs with a checkout containing both revisions.
5. Check Conventional Commits only in the pull request's `<base-sha>..<head-sha>` range; do not validate older history.
6. Run:

   ```sh
   pre-commit run --hook-stage manual --from-ref <base-sha> --to-ref <head-sha>
   ```

7. Do not add a full-program type check such as `tsc --noEmit`.

## Verification

1. Ensure `pre-commit` and `cog` are available, then run `pre-commit validate-config`.
2. Run `cog verify` with one valid and one intentionally invalid message; the invalid result is expected.
3. If a relevant first-party file is already staged, run `pre-commit run --hook-stage pre-commit`.
4. Never create a test commit or auto-stage files. If no suitable staged file exists, report that end-to-end hook verification is pending the next normal commit.
5. Do not weaken rules to hide existing failures.
