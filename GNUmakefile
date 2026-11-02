# Packaging for the chat-digest skill.

SKILL_NAME := chat-digest
SKILL_DIR  := skills/$(SKILL_NAME)
MANIFEST   := plugin.json
DIST       := dist

# plugin.json (Agent Plugins) is the source of truth for all metadata.
VERSION    := $(shell sed -n 's/.*"version": *"\([^"]*\)".*/\1/p' $(MANIFEST))
SKILL_ZIP  := $(DIST)/$(SKILL_NAME)-skill-v$(VERSION).zip
PLUGIN_ZIP := $(DIST)/$(SKILL_NAME)-v$(VERSION).zip

SKILL_FILES  := $(shell find $(SKILL_DIR) -type f)
PLUGIN_FILES := plugin.json .claude-plugin .codex-plugin skills
ZIP_EXCLUDES := -x '*.DS_Store' -x '*.pyc'

.PHONY: package
package: package-plugin package-skill

# Main package: the plugin zip, for ChatGPT and Claude.ai. The plugin
# manifests and skills/ sit at the zip root, as these hosts reject archives
# without them there.
.PHONY: package-plugin
package-plugin: $(PLUGIN_ZIP)

$(PLUGIN_ZIP): $(MANIFEST) .claude-plugin/plugin.json .codex-plugin/plugin.json $(SKILL_FILES)
	@[ -n "$(VERSION)" ] || (echo "Cannot read version from $(MANIFEST)" && exit 1)
	mkdir -p $(DIST)
	rm -f $@
	zip -r $@ $(PLUGIN_FILES) $(ZIP_EXCLUDES)

# Additional package: the skill zip, for Gemini only (which rejects the plugin
# zip, while Claude.ai rejects the skill zip). The top-level entry is the skill
# folder, which itself contains SKILL.md. Stray .DS_Store/.pyc files can fail
# uploads.
.PHONY: package-skill
package-skill: $(SKILL_ZIP)

$(SKILL_ZIP): $(MANIFEST) $(SKILL_FILES)
	@[ -n "$(VERSION)" ] || (echo "Cannot read version from $(MANIFEST)" && exit 1)
	mkdir -p $(DIST)
	rm -f $@
	cd skills && zip -r ../$@ $(SKILL_NAME) $(ZIP_EXCLUDES)

.PHONY: dist-clean
dist-clean:
	rm -rf $(DIST)
