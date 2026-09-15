# Pi configuration

My personal instructions and preferences for the [Pi coding agent](https://pi.dev).

- [`AGENTS.md`](AGENTS.md): working preferences and approval rules. These contain my name, GitHub handle, and local path conventions; adapt them before using them yourself.
- [`settings.json`](settings.json): editor, model, and display preferences.

## Setup

Install Pi separately, then clone this repository:

```sh
git clone git@github.com:spachava753/pi-config.git ~/dev/pi-config
```

Review the files before installing them. Pi's default configuration directory is `~/.pi/agent` (singular `agent`); use your configured directory instead if you set `PI_CODING_AGENT_DIR`.

Back up existing files before copying. These commands ask before overwriting:

```sh
mkdir -p ~/.pi/agent
cp -i ~/dev/pi-config/AGENTS.md ~/.pi/agent/AGENTS.md
cp -i ~/dev/pi-config/settings.json ~/.pi/agent/settings.json
```

Restart Pi after installing the configuration. Authenticate separately through Pi; credentials are not part of this repository.

The configured `openai-codex` provider, `gpt-5.6-sol` model, `xhigh` thinking level, and `dark/dark` theme reflect my installation. They may not be available in yours. Select an available model and theme or edit the settings to match your setup. This repository does not install providers, models, or themes.

## Updating

Changes in `~/.pi/agent` are not automatically synced here. Copy intentional changes back into this checkout and review the diff before committing. Omit runtime bookkeeping such as `lastChangelogVersion` from `settings.json`.

The `.gitignore` allows only the four reviewed files at the repository root. Add new public customization files to that allowlist deliberately. Never commit authentication files, session history, logs, cached model catalogs, downloaded binaries, or package caches. Ignore rules are a safeguard, not a substitute for reviewing staged changes.
