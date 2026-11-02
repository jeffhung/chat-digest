# Agent Instructions

This repository holds the `chat-digest` skill, packaged as a plugin for several
hosts (Claude Code, Codex, and skill uploads to Claude.ai, ChatGPT, and
Gemini).

## Layout

- `skills/chat-digest/SKILL.md`: the skill itself. Keep it host-neutral.
- `plugin.json`: Agent Plugins manifest. **Source of truth for all plugin
  metadata.**
- `.claude-plugin/plugin.json`: Claude Code manifest, derived from
  `plugin.json`.
- `.codex-plugin/plugin.json`: Codex manifest, derived from `plugin.json`.
- `GNUmakefile`: `make package` builds `dist/chat-digest-v<version>.zip` for
  skill uploads. The version is read from `plugin.json`.
- `notes/`: design notes and the original prompt.

## Keeping metadata in sync

Whenever `plugin.json` changes, update the derived manifests in the same
change:

- Copy `name`, `version`, `description`, `author`, and `keywords` to both
  `.claude-plugin/plugin.json` and `.codex-plugin/plugin.json`.
- Copy `extensions."com.openai".interface` from `plugin.json` to the
  `interface` field of `.codex-plugin/plugin.json`.
- Leave host-only fields (such as `skills`) as they are.
- Never edit shared metadata in a derived manifest alone. Change `plugin.json`
  first, then propagate.

Before finishing, confirm all three files agree, and that
`claude plugin validate .` passes.

## Versioning

Never bump `version` on your own. Version bumps are triggered by a human only.

## Packaging

- Run `make package` to build the upload zip. The zip must have the
  `chat-digest` folder at its top level with `SKILL.md` inside.
- Do not add `.DS_Store` or `.pyc` files to the skill folder; they can make
  uploads fail.
- `dist/` is generated and gitignored.
