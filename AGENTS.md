# AGENTS.md — simple-agents-releases

> Read this before changing the public release repository.

## Identity

This repository is the public binary destination for Simple Agents. It contains
release metadata and assets, not the private TUI/Core source code.

## Release ownership

**Policy effective and last verified: 2026-08-15.** Releases are owned by
`yarumolabs/simple-agents-tui` and dispatched only through:

```bash
cd /path/to/simple-agents-tui
bun run release -- --dry-run
bun run release
```

Never call `gh release create`, `gh release upload`, or the TUI workflow
directly unless the human explicitly authorizes a recovery operation. Never
delete or mutate releases, tags, or assets speculatively.

## Actions cost behavior

This repository has no workflow files. A push to its `main` branch does not
start GitHub Actions and consumes no Actions minutes. Production build minutes
are charged to the TUI repository only after the release CLI dispatches.

## Asset contract

Every published latest release must contain:

- `simple-agents-darwin-arm64.zip`
- `simple-agents-linux-x64.tar.gz`
- `simple-agents-linux-arm64.tar.gz`
- `simple-agents-windows-x64.zip`

GitHub's automatic source archives are expected and contain only this public
repository. They are not private product source.

## Product isolation

Do not publish Tauri/desktop assets here. GitHub exposes only one latest release
per repository, and replacing it would break the TUI installer and updater. A
desktop application requires its own release repository.

## Safe repository work

Before documentation changes:

```bash
git pull --rebase origin main
```

Never force-push. Preserve the binary-only role and keep this README aligned
with the TUI's authoritative `docs/RELEASING.md`.
