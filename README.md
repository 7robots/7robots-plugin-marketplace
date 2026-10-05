# 7robots plugin marketplace

A plugin marketplace on GitHub. It holds MCP servers and skill plugins.

## Install from this marketplace

**Claude Code**
```
/plugin marketplace add 7robots/7robots-plugin-marketplace
/plugin install <name>@7robots-plugin-marketplace
```

**Codex**
```
codex plugin marketplace add 7robots/7robots-plugin-marketplace
```

For a private repo, each user needs read access to it and working git credentials.

## Layout

```
.claude-plugin/marketplace.json      # Claude catalog
.agents/plugins/marketplace.json     # Codex catalog
servers/<name>/                      # an entry providing an MCP server
plugins/<name>/                      # an entry providing skills only
schema/                              # JSON Schemas the CI gate validates against
```

## Managing entries

Each entry's `server.yaml` is its source of truth; every other file in its
directory and both catalogs are generated from it. Manage entries with
`mcp-studio marketplace add|update|deprecate|reinstate|remove`, which
validates before committing. **Write access to this repo is the access
control:** whoever can push can publish.
