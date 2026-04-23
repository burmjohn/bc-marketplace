# bc-marketplace

A Claude Code plugin for searching and installing Boomi Marketplace recipes. Recipes are installed as reference samples — use them to inform how integrations are built, not as production-ready components.

> **Important:** Boomi Companion is a publicly available developer offering, not an officially supported Boomi product. It is provided as-is and is not covered by Boomi support agreements or SLAs. Boomi curates and maintains this tool on a best-effort basis — treat it as a self-service resource. Boomi reserves the right to modify or discontinue it at any time without notice.

This project is licensed under the [BSD-2-Clause License](LICENSE). If you fork or modify this code, you should not use the name "Boomi" for your version.

## Feedback & Issues

Found a bug or have a feature idea? Email developer-offerings@boomi.com with a clear description, steps to reproduce, and any relevant error messages.

## Claude Code Installation

```bash
/plugin marketplace add OfficialBoomi/boomi-companion
/plugin install bc-marketplace@boomi-companion
```

Or browse and install via `/plugin` interactively.

## Using the Skill From Other Agents

Agents that can load skill folders directly can use `skills/boomi-marketplace`
without the Claude plugin wrapper. Marketplace search works standalone. Recipe
install requires the `boomi-integration` skill because the install script
sources `scripts/boomi-common.sh` for authentication and activity logging.

## Dependencies

- **Search** works standalone — no other skills required.
- **Install** requires the `boomi-integration` skill. The install script sources `boomi-common.sh` from boomi-integration for authentication and activity logging. Folder creation and component pulling also use boomi-integration's tools.

## Skill: boomi-marketplace

Search the Boomi Marketplace catalog and install recipes into a target account.

### Workflow

1. **Search** — Query the public GraphQL API for published recipes matching an app or use case (no authentication required).
2. **Install** — Run the install script to deploy a recipe bundle into a `marketplace-imports` subfolder inside a project folder.
3. **Read** — Use bc-integration's component pulling workflow to fetch the installed process XML and its dependencies locally.

### CLI Tools

**Recipe Install** — Installs a marketplace recipe into a target folder:

```bash
BOOMI_COMMON_SH=<path/to/boomi-common.sh> bash scripts/boomi-marketplace-install.sh --bundle-id <artifactSourceId> --folder-id <numeric_folder_id>
```

Optional: `--target-account-id <ID>` overrides the install target (defaults to `BOOMI_ACCOUNT_ID` from `.env`).

### Reference Docs

| Document | Description |
|----------|-------------|
| [GraphQL API](skills/boomi-marketplace/references/graphql-api.md) | Public catalog search queries |
| [Bundle API](skills/boomi-marketplace/references/bundle-api.md) | Authenticated recipe installation |

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
