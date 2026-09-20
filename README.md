# Skills

Reusable skills for Claude Code, Codex, and Cursor.

## Install

Paste this into Claude Code, Codex, or Cursor:

```text
Install every skill in the `shared/` directory of https://github.com/arup-kumar-maiti/skills for this client.

Use the client’s normal user-level skill location when available; otherwise use its normal project location. Copy each skill directory unchanged.

For each selected skill, classify its target directory independently:
- If it is absent, install it.
- If its `.agent-skills-origin` contains `https://github.com/arup-kumar-maiti/skills`, refresh it.
- Otherwise preserve it and report a conflict.

For a refresh, first copy and verify the replacement in a sibling temporary directory, then replace the marked target directory. Never copy a skill directory into an existing target directory or leave a nested skill directory.

Use the client’s normal mechanism to make each installed skill invocable. When a command wrapper is required, mark it with `<!-- agent-skills-origin: https://github.com/arup-kumar-maiti/skills -->`.

Clean up temporary files and report installed, refreshed, and skipped skills.
```

To install one skill, replace “every skill” with its directory name, such as `repo-standards`.

## Use

Invoke a skill by name:

- Claude Code: `/repo-standards`
- Codex: `$repo-standards`
- Cursor: `/repo-standards`

## Uninstall

Paste this into Claude Code, Codex, or Cursor:

```text
Uninstall every skill from https://github.com/arup-kumar-maiti/skills for this client.

Remove only skill directories whose `.agent-skills-origin` contains `https://github.com/arup-kumar-maiti/skills` and only command wrappers marked `<!-- agent-skills-origin: https://github.com/arup-kumar-maiti/skills -->`.

Preserve everything else. Clean up temporary files and report removed and skipped skills.
```

To uninstall one skill, replace “every skill” with its directory name, such as `repo-standards`.
