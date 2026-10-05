# Kagi News

Today's news from Kagi News, in four sections: World, Science, United States and Boston. Kagi rebuilds the feeds once each morning, so this is a daily edition rather than a live wire. Start with kagi_list_stories to see what is in today's edition — it returns headlines only and is cheap. Then kagi_get_story for the ones that matter: each body runs 4-15KB, so reading all 32 at once would spend most of a context on articles nobody asked about.

## Install

**Claude Code**
```
/plugin marketplace add 7robots/7robots-plugin-marketplace
/plugin install kagi-news@7robots-plugin-marketplace
```

**Codex**
```
codex plugin marketplace add 7robots/7robots-plugin-marketplace
```

## Server

- **Endpoint:** `https://news.mcp.7robots.org/mcp`
- **Transport:** `http`
- **Auth:** `oauth`

## Authentication

This server uses OAuth. Your MCP client will prompt you to authenticate on first use.

---

_Generated from `server.yaml`. Edit that file and open a PR to change this plugin — do not hand-edit generated files._
