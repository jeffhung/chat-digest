# History

## 0.1.2

- The package can now be uploaded to ChatGPT and Claude.ai.
- Gemini uses a separate skill package.

## 0.1.1

- Support hosts that cannot create files or artifacts, such as Gemini web. The
  skill now outputs the digest as a single copyable `markdown` code block in
  the chat, with fallback fences if the host does not render it.
- Add a Claude Code plugin manifest (`.claude-plugin/plugin.json`).
- Add `make package`, which builds a versioned zip for uploading the skill to
  Claude.ai, ChatGPT, and Gemini.
- Add `AGENTS.md` and `CLAUDE.md`, and a README with install and upload steps.

## 0.1.0

- Initial version of the chat-digest skill, created with the ChatGPT Plugin
  Creator.
