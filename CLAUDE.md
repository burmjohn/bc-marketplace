# bc-marketplace

Claude Code plugin for searching and installing Boomi Marketplace recipes. Installs recipe bundles into a target account as reference samples that can inform how integrations are built.

## Installation

```bash
/plugin marketplace add git@bitbucket.org:officialboomi/boomi-marketplace.git
/plugin install bc-marketplace@boomi-marketplace
```

Requires `boomi-integration` plugin for recipe installs. The install script sources `boomi-common.sh` from bc-integration for authentication and activity logging. Catalog search works standalone. This plugin also depends on bc-integration's folder management, component pulling tools, and platform knowledge to complete its workflow.

## Structure

```
.claude-plugin/plugin.json
skills/
  boomi-marketplace/
    SKILL.md
    scripts/
      boomi-marketplace-install.sh
    references/
      graphql-api.md
      bundle-api.md
```