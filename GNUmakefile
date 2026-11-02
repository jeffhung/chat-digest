# Packaging for the chat-digest skill.

SKILL_NAME := chat-digest
SKILL_DIR  := skills/$(SKILL_NAME)
MANIFEST   := plugin.json
DIST       := dist

# plugin.json (Agent Plugins) is the source of truth for all metadata.
VERSION := $(shell sed -n 's/.*"version": *"\([^"]*\)".*/\1/p' $(MANIFEST))
ZIP     := $(DIST)/$(SKILL_NAME)-v$(VERSION).zip

# Build the zip for uploading as a skill to Claude.ai, ChatGPT, and Gemini.
.PHONY: package
package: $(ZIP)

# These hosts expect a zip whose top-level entry is the skill folder, which
# itself contains SKILL.md. Stray .DS_Store/.pyc files can fail the upload.
$(ZIP): $(MANIFEST) $(shell find $(SKILL_DIR) -type f)
	@[ -n "$(VERSION)" ] || (echo "Cannot read version from $(MANIFEST)" && exit 1)
	mkdir -p $(DIST)
	rm -f $@
	cd skills && zip -r ../$@ $(SKILL_NAME) -x '*.DS_Store' -x '*.pyc'

.PHONY: dist-clean
dist-clean:
	rm -rf $(DIST)
