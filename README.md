# simple-agents-releases

Public binary distribution repository for Simple Agents. This repository holds
release tags and compiled assets only; the TUI and Core source repositories are
private and are not mirrored here.

**Release policy effective:** 2026-08-15

**Last verified:** 2026-08-15

## Publishing

Do not create or upload releases manually from this repository. The only
supported production entry point is the guarded CLI in
`yarumolabs/simple-agents-tui`:

```bash
cd /path/to/simple-agents-tui
git pull --rebase origin main
bun run release -- --dry-run
bun run release
```

The command pins the remote TUI and Core `main` commits, creates a draft, builds
every platform, verifies the assets, and publishes only after all builds pass.

## Expected release assets

| Platform | Asset |
|---|---|
| macOS ARM64 | `simple-agents-darwin-arm64.zip` |
| Linux x64 | `simple-agents-linux-x64.tar.gz` |
| Linux ARM64 | `simple-agents-linux-arm64.tar.gz` |
| Windows x64 | `simple-agents-windows-x64.zip` |

GitHub automatically displays “Source code (zip)” and “Source code (tar.gz)”
for every tag. Those archives contain this public release repository's contents;
they are not the private TUI/Core source and are not additional Actions builds.

## Consumers

- `https://simpleagents.co/install.sh` downloads the platform asset from the
  latest release.
- Installed TUI binaries query this repository's `/releases/latest` endpoint for
  patch updates.

There must be one complete latest release. Do not mix another product, such as a
Tauri desktop application, into this repository because it would replace the
TUI's latest-release pointer. Use a separate desktop release repository.

## GitHub Actions usage

This repository contains no GitHub Actions workflows. A documentation push to
its `main` branch consumes no Actions minutes. Binary releases consume minutes
in the private TUI repository only after `bun run release` intentionally
dispatches its workflow.

See `AGENTS.md` before changing tags, releases, or documentation.
