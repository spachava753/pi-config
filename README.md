# Pi configuration

My personal instructions and preferences for the [Pi coding agent](https://pi.dev).

- [`AGENTS.md`](AGENTS.md): working preferences and approval rules. These contain my name, GitHub handle, and local path conventions; adapt them before using them yourself.
- [`settings.json`](settings.json): model, display preferences, and the `npm:pi-mcp-adapter` package declaration.
- [`mcp.example.json`](mcp.example.json): MCP server configuration with the authorization credential replaced by a placeholder.
- [`skills/`](skills/): snapshots of the shared skills installed in `~/.agents/skills`: `ast-grep`, `ast-grep-outline`, `bb-cli`, and `bro`, including their reference files.

## Setup

Install Pi separately, then clone this repository:

```sh
git clone git@github.com:spachava753/pi-config.git ~/dev/pi-config
```

Review the files before installing them. Pi's default configuration directory is `~/.pi/agent` (singular `agent`); use your configured directory instead if you set `PI_CODING_AGENT_DIR`.

Back up existing files before copying. These commands ask before overwriting:

```sh
mkdir -p ~/.pi/agent ~/.agents/skills
cp -i ~/dev/pi-config/AGENTS.md ~/.pi/agent/AGENTS.md
cp -i ~/dev/pi-config/settings.json ~/.pi/agent/settings.json
cp -Ri ~/dev/pi-config/skills/. ~/.agents/skills/
```

These are copies, not symlinks. Copying skills does not remove obsolete destination files. Review existing skills before installing; `~/.agents/skills` is shared with other agents, not exclusive to Pi.

Restart Pi after installing the configuration. Authenticate separately through Pi; credentials are not part of this repository.

The configured `openai-codex` provider, `gpt-6-astra` model, `low` thinking level, `dark/dark` theme, and fullscreen TUI reflect this machine's settings. Model and theme availability can differ between installations. This repository does not install providers, model catalogs, or themes. The MCP adapter package is declared in settings rather than vendored; its version is not pinned, so this is a configuration snapshot, not a fully locked environment.

### MCP servers

The template declares:

- `1password`: the local `1password-mcp` executable, which must be installed and available on `PATH` separately.
- `parallel`: `https://search.parallel.ai/mcp`, requiring a local authorization value.

To configure another machine, copy the template only after reviewing any existing MCP configuration:

```sh
cp -i ~/dev/pi-config/mcp.example.json ~/.pi/agent/mcp.json
chmod 600 ~/.pi/agent/mcp.json
```

Replace `REPLACE_WITH_LOCAL_AUTHORIZATION_VALUE` locally with the required authorization header value, using your password manager. The placeholder is literal, not environment-variable interpolation. Do not enable the Parallel server until its credential is configured. Authenticate/configure the 1Password server separately. Never copy the resulting `mcp.json` back into Git.

### Shared skill sources

The local installer metadata identifies `ast-grep` and `ast-grep-outline` as coming from [ast-grep/agent-skill](https://github.com/ast-grep/agent-skill), and `bro` from [cursor/plugins](https://github.com/cursor/plugins) (`pstack/skills/bro`). It does not identify a source for `bb-cli`. The files here preserve the installed contents rather than assuming upstream still matches them.

The installer lock file is not included: it also lists a skill no longer present locally and contains machine-specific installation metadata. These snapshots do not install the tools that the skills describe, such as `ast-grep`, `bb`, or `bro`.

## Updating

Changes in `~/.pi/agent` and `~/.agents/skills` are not automatically synced here. Pull repository changes before editing on another machine. Copy intentional local changes back into this checkout and review the diff before committing; omit runtime bookkeeping such as `lastChangelogVersion` from `settings.json`. Compare skill directories for removals as well as additions.

For MCP changes, update only the credential-free template. Keep live authorization values local. After reviewing and committing changes, push them and pull/apply them on the other machine. No automatic commits, pushes, or live-config modifications are performed by this repository.

The `.gitignore` allows only reviewed root files and Markdown files in the four snapshotted skill directories. Add new customization files to that allowlist deliberately. Never commit authentication files, session history, logs, cached model catalogs, downloaded binaries, package caches, or local trust decisions. Ignore rules are a safeguard, not a substitute for reviewing staged changes.
