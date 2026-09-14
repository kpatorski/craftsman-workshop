# craftsman-workshop

A reference workshop for [craftsman](https://github.com/kpatorski/craftsman) — this author's own directives (what
must be true about the code right now), protocols (what order to work in, and where to stop), and bundles (themed
groups of the two, installed and enabled together). Written against the format defined in craftsman's own
[`core.md`](https://github.com/kpatorski/craftsman/blob/main/plugins/craftsman/core.md).

This workshop is useless without the `craftsman` plugin installed — every directive, protocol, and bundle assumes it.
Individual files here mention `core.md` by name only, without a link: the plugin caches its own code under a path
that moves on every update, so no fixed link from this repo could stay valid. An agent running a `craftsman` protocol
already has `core.md` locally (it loaded it the same way it loaded this workshop's content); the link above is for a
human browsing this repo to find the current copy on GitHub.

It is a starting point, not a default everyone must adopt: install it, fork it privately, or write your own from
scratch against `core.md`.

## Layout

- `directives/`, `protocols/` — fundament: entries used by more than one theme, or a single standalone preference.
  17 protocols, 25 directives.
- `bundles/` — 7 themed groups, each installable and toggleable as a unit: `testing`, `tdd` (requires `testing`),
  `legacy-code` (requires `testing`, `tdd`), `module-bootstrap`, `event-storming`, `spec-writing`, `gwt-digest`.
- Every collection has its own `index.md` — the lookup table, `## Examples` walking the fundament-vs-bundle and
  directive-vs-protocol calls on real entries from this repo.

## Installing

From inside a Claude Code session with the `craftsman` plugin installed:

```
/craftsman:install https://github.com/kpatorski/craftsman-workshop
```

See craftsman's own [README](https://github.com/kpatorski/craftsman#readme) for installing the plugin itself first.

## Updating

No auto-update. Re-run the same command any time:

```
/craftsman:install https://github.com/kpatorski/craftsman-workshop
```

If nothing changed since your last install, it says so and stops. If something did, it shows what and asks before
touching anything — see craftsman's own `MANAGEMENT.md`, "Checking a known source for updates":
[github.com/kpatorski/craftsman/blob/main/plugins/craftsman/MANAGEMENT.md](https://github.com/kpatorski/craftsman/blob/main/plugins/craftsman/MANAGEMENT.md)

## License

[PolyForm Internal Use License 1.0.0](LICENSE.md) — free to use, including commercially, for your own internal
purposes. Redistribution (forking and republishing, mirroring, or otherwise passing this repository or a modified
version of it on to third parties) is not permitted.
