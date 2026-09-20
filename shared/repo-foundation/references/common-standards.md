# Common Standards

Apply these after language and tool selection is confirmed.

## Prerequisites

1. Ensure Git, Python, and Cocogitto are available. If any are absent, present the required machine-level installation commands together and obtain one confirmation before running them.

## Managed Hooks

1. Use `.pre-commit-config.yaml` as the single formatter and linter hook configuration. Preserve a compatible existing configuration; otherwise ask before replacing or merging it. Treat another manager for `pre-commit` or `commit-msg` as a conflict.
2. Configure every formatter and linter in a managed pre-commit environment with its exact stable version pinned. Prefer a maintained external hook repository. When a compatible maintained hook is unavailable, use `repo: local` with a managed language and pinned `additional_dependencies`; do not use `language: system` for those tools.
3. Let each hook's `types`, `types_or`, or `files` selector limit it to its matching selected files. Use `.gitignore` as a discovery signal, not hook configuration. Set a global `exclude` for detected tracked generated, vendored, dependency, build-output paths, and lockfiles without excluding first-party files.
4. Reuse one formatter hook for every selected file type that its tool supports.
5. For each formatter, configure a writing `pre-commit` hook and a matching non-mutating `manual`-stage check hook.
6. Run linters without auto-fixing. Within each language, place formatting before linting; place the Conventional Commit hook last.
7. If formatting changes files during a commit, let pre-commit abort it so the developer can review and stage the changes. Never auto-stage files.
8. Ensure `pre-commit` is available through an existing project Python environment; otherwise create `.venv` with `python -m venv`, add `.venv/` to `.gitignore`, and install `pre-commit` there. Do not install language tooling globally.
9. Install the hooks with `pre-commit install --install-hooks --hook-type pre-commit --hook-type commit-msg`.

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
