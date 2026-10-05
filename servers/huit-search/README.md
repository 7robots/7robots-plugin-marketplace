# HUIT Website Search

MCP server for topic search over the Harvard University IT (HUIT) website, on Cloudflare Workers with Okta OAuth.

## Install

**Claude Code**
```
/plugin marketplace add 7robots/7robots-plugin-marketplace
/plugin install huit-search@7robots-plugin-marketplace
```

**Codex**
```
codex plugin marketplace add 7robots/7robots-plugin-marketplace
```

## Server

- **Endpoint:** `https://huit.mcp.7robots.org/mcp`
- **Transport:** `http`
- **Auth:** `oauth`

## Authentication

This server uses OAuth. Your MCP client will prompt you to authenticate on first use.

---

_Generated from `server.yaml`. Edit that file and open a PR to change this plugin — do not hand-edit generated files._
