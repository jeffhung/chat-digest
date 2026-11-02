# Chat Digest

Turns an AI conversation into an organized, reusable Markdown document that
preserves problems, constraints, methods, solution variants, trade-offs, and
decisions.

The skill lives in `skills/chat-digest/SKILL.md` and is packaged for three
hosts:

| Host        | Manifest                         |
|-------------|----------------------------------|
| Codex       | `.codex-plugin/plugin.json`      |
| Agent Plugins | `plugin.json` (source of truth) |
| Claude Code | `.claude-plugin/plugin.json`     |

## Install in Claude Code

Load the plugin directly from a local checkout:

```
claude --plugin-dir /path/to/chat-digest
```

Then ask Claude to digest the conversation, or invoke
`/chat-digest:chat-digest`.

## Upload to ChatGPT, Claude.ai, or Gemini

Build the upload packages:

```
make package
```

This creates two zips in `dist/`:

- `chat-digest-v<version>.zip`: the plugin package, with the plugin manifests
  and `skills/` at the zip root. This is the main package, for ChatGPT and
  Claude.ai. ChatGPT rejects archives without them there.
- `chat-digest-skill-v<version>.zip`: the skill package, with the skill folder
  (`chat-digest/SKILL.md`) at the top level. Gemini accepts only this form,
  while Claude.ai rejects it.

`make package-plugin` and `make package-skill` build each one separately.

- ChatGPT (chatgpt.com): upload the plugin package.
- Gemini (gemini.google.com): upload the skill package on the Skills page.
  Gemini cannot create files or artifacts, so the skill outputs the digest as
  one copyable `markdown` code block in the chat.
- Claude.ai: upload the plugin package. Code execution and file creation must
  be enabled for the skill to produce a Markdown file.
