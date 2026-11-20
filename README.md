# Lanework plugins

The marketplace for [Lanework](https://lanework.dev)'s Claude Code plugins.

| Plugin | What it brings |
| --- | --- |
| [`lanework`](plugins/lanework/) | The board's MCP tools, and a checkpoint on your card after every turn so another agent can pick the work up. |

```text
/plugin marketplace add lanework-dev/plugins
/plugin install lanework@lanework
```

Using the Lanework desktop app? You do not need this plugin: the app sets up
the same MCP server and hook from **Settings → Agents**.

## Where the code comes from

`plugins/lanework/bin/lanework-checkpoint.cjs` is a build output, committed
because a Claude Code plugin installs by cloning this repository. Its source
is the hook in [fuongz/lanework](https://github.com/fuongz/lanework)
(`apps/desktop/electron/hook/`), which the desktop app bundles too.
`plugins/lanework/build.json` names the commit it was built from and the bun
that built it.

Every push to fuongz/lanework's main rebuilds it (`plugin-sync` workflow
there); when the bundle changed, it opens or refreshes the `sync/hook` pull
request here with the bundle, `build.json` and a patch bump of the plugin's
version. Review and merge it once `check` passes.

To do the same by hand, from a clone of fuongz/lanework with the change
committed and this repository cloned next to it as `../lanework-dev/plugins`:

```sh
bun run build:plugin            # or: node scripts/build-plugin.mjs --out <this clone>
```

Then commit the bundle and `build.json` here, and bump `version` in
`plugins/lanework/.claude-plugin/plugin.json` so installs pick it up.

CI (`.github/workflows/check.yml`) checks out the commit `build.json` names,
rebuilds the bundle and fails if it differs from the one committed here.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md), including the commit message
convention.

## License

MIT, see [LICENSE](LICENSE).
