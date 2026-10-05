# D&D Characters

MCP server for managing Dungeons & Dragons characters in Cloudflare D1. Use these tools to list, search, create, update, and delete characters. Each character has a name, class, species, level (1-20), and alignment. Characters are addressed by their 24-character hex character id; get an id from dnd_list_characters or dnd_search_characters before calling get/update/delete.

## Install

**Claude Code**
```
/plugin marketplace add 7robots/7robots-plugin-marketplace
/plugin install dnd-characters@7robots-plugin-marketplace
```

**Codex**
```
codex plugin marketplace add 7robots/7robots-plugin-marketplace
```

## Server

- **Endpoint:** `https://dnd.mcp.7robots.org/mcp`
- **Transport:** `http`
- **Auth:** `oauth`

## Authentication

This server uses OAuth. Your MCP client will prompt you to authenticate on first use.

---

_Generated from `server.yaml`. Edit that file and open a PR to change this plugin — do not hand-edit generated files._
