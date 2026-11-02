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

## Upload to Claude.ai, ChatGPT, or Gemini

Build the upload package:

```
make package
```

This creates `dist/chat-digest-v<version>.zip`, where the version is read from
`plugin.json`. The zip holds the `chat-digest` skill folder with
`SKILL.md` inside, the layout these hosts accept for skill uploads.

- Claude.ai: Settings > Capabilities > Skills > Upload skill. Code execution
  and file creation must be enabled for the skill to produce a Markdown file.
- Gemini (gemini.google.com): upload on the Skills page. Gemini cannot
  create files or artifacts, so the skill outputs the digest as one
  copyable `markdown` code block in the chat.
- ChatGPT (chatgpt.com): upload as a custom skill. Not yet verified.
