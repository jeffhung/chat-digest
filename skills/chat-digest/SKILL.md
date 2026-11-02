---
name: chat-digest
description: |
  Use when a user wants an AI conversation organized and summarized into
  a reusable Markdown document that preserves key context, requirements,
  options, trade-offs, and decisions.
version: 0.1.1
---

# Chat Digest

Turn the current conversation into a self-contained Markdown document that
makes the discussion easy to understand and continue later. Deliver it as
a Markdown file when the host can create one; otherwise deliver it as a single
copyable code block (see Output). Do not provide only an in-chat summary.


## Source and fidelity

- Use all available conversation context, not only the latest message.
- Preserve the evolution of the discussion when it affects the final
  understanding: late-arriving requirements, constraints, rejected approaches,
  corrections, unresolved questions, and decisions.
- Remove repetition and conversational noise, but retain distinct ideas even if
  they appeared briefly or were later deprioritized.
- Do not invent facts, requirements, measurements, evidence, implementation
  details, or decisions. Mark unknown or unvalidated points as such.
- Distinguish explicit user requirements from assistant suggestions and
  inferred considerations. Never present a suggestion as an accepted decision
  unless the conversation supports that status.
- Keep terminology consistent with the conversation. Prefer established names
  over newly invented ones.
- Omit sections that lack useful content. Do not pad the document.
- Use readable Markdown headings, lists, and tables where they improve
  scanning. Do not use HTML headings.


## Document structure

Use these top-level sections, in this order, when supported by the
conversation:

1. Background (optional)
2. Problem Statements
3. Proposed Methods
4. Analysis Topics
5. Proposed Solutions
6. Comparisons
7. Open Questions (optional)
8. Decisions and Next Steps (optional)

Start with a concise, topic-specific title. Add Background before Problem
Statements when it explains the environment, assumptions, use case, or basis of
the discussion.


### Problem Statements

Explain why the topic is being explored. Capture goals, requirements,
constraints, concerns, and risks. Group related points and include the context
needed to understand them. Preserve priority or mandatory status only when
stated or clearly established. Separate facts, requirements, assumptions, and
unresolved questions when that distinction matters.


### Proposed Methods

Document each distinct method variant that may address a requirement or
concern. Methods are building blocks and may be combined; they do not need to
solve the whole problem alone. A method may be a tool, component, algorithm,
protocol, architecture pattern, or usage pattern.

Give each method a nested heading using its name only, without numbering or
a prefix. Describe how it works using supported details, then include:

- **Pros:** benefits of this method on its own.
- **Cons:** limitations, costs, risks, and prerequisites of this method on its
  own.

Do not compare methods in these pros and cons. Prefer quantitative facts when
available; never invent measurements. Include specific protocols, connectors,
adapters, and orchestrators needed to connect components only when established
in the conversation.


### Analysis Topics

Include aspects that need separate evaluation, validation, inference, or
investigation because they affect requirements, concerns, prerequisites, or
trade-offs. Give each topic a nested heading containing only its name. Explain
why it matters, then describe how the proposed methods address it and their
relevant benefits and trade-offs. Keep each topic focused on one aspect. Do not
rank methods or compare them overall here. Mark unknown behavior as requiring
validation.


### Proposed Solutions

Present a small set of meaningful solution variants, not every possible
combination. Each variant must have a clear primary advantage and trade-off.

- Use nested headings for variants, without numbering.
- Reuse names and phrases established earlier. If no established name exists,
  use a concise name based on the included methods.
- Explain the component arrangement and workflow in prose or a diagram when
  useful.
- Explain how the methods connect. Any specific wiring component or protocol
  must already be described in Proposed Methods.
- Treat methods that can coexist as optional configuration choices within one
  solution family. Split variants only when feasibility constraints make them
  mutually exclusive.
- For each optional method, explain the unique value it adds, including any
  synergy that depends on it. Do not claim overlapping benefits as unique.
- If there are more than two optional methods or distinct value aspects, use
  a table to map optional methods to their unique contributions; otherwise use
  bullets.
- If only one feasible solution exists, describe it directly without a variant
  heading and omit Comparisons.
- Do not recommend a winner in this section.


### Comparisons

Compare the solution variants as a whole across important analysis topics and
requirements. Show benefits, unmet needs, prerequisites, risks, and trade-offs
so the user can decide. Use one holistic comparison view, usually a table.
Include only relevant dimensions. Mark evidence that is unknown, assumed, or
needs validation. Avoid unsupported scores and false precision. Omit this
section if there is only one solution variant.


### Optional closing sections

- **Open Questions:** unresolved questions, assumptions to verify, and evidence
  still needed.
- **Decisions and Next Steps:** decisions actually made and practical follow-up
  actions. Distinguish confirmed decisions from suggestions.


## Final quality check

Before delivering the document, verify that all important requirements and
concerns are included; every distinct method variant is represented; methods,
analysis topics, solutions, and comparisons have distinct purposes; each method
has its own pros and cons; each analysis topic focuses on one aspect;
coexisting options are consolidated; optional methods have clear unique
contributions; comparisons are objective and holistic; unknowns and disputed
points remain explicit; and the Markdown can be understood without rereading
the chat.


## Output

Choose the delivery mode by what the host supports.


### Host can create files or artifacts

Create a Markdown file with a descriptive filename such as `chat-digest.md` or
a topic-specific name. Attach it as an artifact. In the chat response, briefly
identify the artifact and any material gaps. Do not reproduce the full document
in chat when the artifact is available.


### Host cannot create files or artifacts (for example, Gemini web)

Output the complete document inside one fenced code block with the `markdown`
language identifier, so the chat UI renders it as a single block with a copy
button.

- The outer fence must be longer than any backtick run inside the document, so
  inner code fences never end the block early. Default to four backticks (`
  ````markdown `, closed with four backticks); this is confirmed to render as
  one copyable block on Gemini web only.
- If the host does not render the four-backtick fence as a single block, fall
  back to a three-backtick fence when the document contains no code fences. If
  it does contain code fences, use a tilde fence (`~~~markdown`) as the outer
  fence instead.
- Put the whole document in the block, from the title heading to the last
  section. Do not split it across several blocks.
- Write nothing outside the block: no introduction, no closing summary. Record
  material gaps inside the document under Open Questions.

