Please set up Release Please for this GitHub repository, releasing from `main`. I want it to maintain one reviewable release PR with the next SemVer version and changelog, then create the Git tag and GitHub Release when that PR is merged.

First, inspect the existing release setup, history, version source, changelog, and Conventional Commit history. Preserve anything compatible. If there is no prior release, include the current `main` history in the first release PR. Before changing files, summarize the plan and flag any conflict that needs my approval.

Use manifest configuration. If the repository is not an established package or module, use one root `simple` component, `version.txt` at `0.0.0`, and a `CHANGELOG.md` containing only its heading. Do not invent a package manifest. Ask me before configuring multiple independently versioned components when the boundaries are unclear.

Create the minimal GitHub Actions workflow using the current stable major of `googleapis/release-please-action`, the `RELEASE_PLEASE_TOKEN` secret, and only `contents: write`, `issues: write`, and `pull-requests: write` permissions. Do not create or expose credentials, or add publishing, deployment, a GitHub App, or branch-protection changes or bypasses.

Validate the JSON and workflow YAML without creating a release PR, tag, GitHub Release, publication, or deployment. At the end, tell me about any missing one-time setup; if the secret is missing, tell me how to create a repository-scoped `release-please` token with the necessary permissions and save it as `RELEASE_PLEASE_TOKEN`.
