# Image Generator

When using the generate_image tool, you MUST include the full image URL in your response to the user. The URL is the most important part of the response - without it, the user cannot view the generated image. Always format it as a clickable link.

When working with tool results, write down any important information you might need later in your response, as the original tool result may be cleared later.

## Install

**Claude Code**
```
/plugin marketplace add 7robots/7robots-plugin-marketplace
/plugin install image-generator@7robots-plugin-marketplace
```

**Codex**
```
codex plugin marketplace add 7robots/7robots-plugin-marketplace
```

## Server

- **Endpoint:** `https://images.mcp.7robots.org/mcp`
- **Transport:** `http`
- **Auth:** `oauth`

## Authentication

This server uses OAuth. Your MCP client will prompt you to authenticate on first use.

---

_Generated from `server.yaml`. Edit that file and open a PR to change this plugin — do not hand-edit generated files._
