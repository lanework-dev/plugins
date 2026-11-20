# Contributing

Everything in this repository runs on users' machines after every Claude Code
turn, so every change needs the code owner's review (`.github/CODEOWNERS`).

The hook bundle (`plugins/lanework/bin/lanework-checkpoint.cjs`) is a build
output. Never edit it by hand: change the hook in
[fuongz/lanework](https://github.com/fuongz/lanework) and rebuild it as the
[README](README.md#where-the-code-comes-from) says.

## Commit messages

Use [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/):

```text
<type>(<scope>): <summary>

<body>

<footer>
```

- **type**, one of:

  | Type | For |
  | --- | --- |
  | `feat` | Something a user of a plugin gets: a command, a hook event, an MCP server. |
  | `fix` | A bug a user of a plugin hits. |
  | `build` | A rebuilt hook bundle and its `build.json`. |
  | `ci` | `.github/workflows/`. |
  | `docs` | READMEs and this file. |
  | `chore` | Anything else: licenses, owners, the marketplace's description. |
  | `refactor`, `perf`, `style`, `test`, `revert` | As the spec defines them. |

- **scope**: the plugin's folder name (`lanework`), or `marketplace` for
  `.claude-plugin/marketplace.json`. Leave it out for a change to the whole
  repository.
- **summary**: imperative, lower case, no full stop, at most 72 characters.
  Say what changes for the user: `fix(lanework): skip the hook without Node 18`,
  not `update files`.
- **body** (optional): why, wrapped at 72 columns. A bundle rebuild names the
  fuongz/lanework commit it came from: `Built from fuongz/lanework@<short sha>.`
- **breaking change**: `!` after the type or scope and a
  `BREAKING CHANGE: <what to do>` footer, for anything that makes an existing
  install stop working (a renamed plugin or marketplace, a removed command).
- One logical change per commit. Bump `version` in the plugin's
  `.claude-plugin/plugin.json` in the commit that changes what it ships.

Examples:

```text
build(lanework): rebuild the hook

Built from fuongz/lanework@a74ff27.
```

```text
feat(lanework)!: rename the plugin to lanework-board

BREAKING CHANGE: reinstall with /plugin install lanework-board@lanework.
```
