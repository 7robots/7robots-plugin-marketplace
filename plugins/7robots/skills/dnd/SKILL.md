---
name: dnd
description: "Manage Dungeons & Dragons characters stored in Cloudflare D1. Tools are the 7robots portal tools prefixed dnd_."
---

# DnD Characters MCP Server

This server provides CRUD tools for managing D&D characters stored in a Cloudflare D1 table.

## Data Model

Each character is returned with these PascalCase fields:

```json
{
  "_id": "24-character hex id",
  "Name": "Character name",
  "Class": "Ranger | Wizard | Rogue | Cleric | ...",
  "Species": "Human | Elf | Dragonborn | Halfling | ...",
  "Level": 1,
  "Alignment": "Lawful Good | Neutral | Chaotic Neutral | ..."
}
```

Tool parameters are lowercase (`name`, `character_class`, `species`, `level`, `alignment`); the server maps them to the returned PascalCase fields. `Level` is an integer 1-20. There are no ability scores and no background field — the data is intentionally lean.

## Available Tools

| Tool | Purpose |
|------|---------|
| `dnd_list_characters` | List/filter characters with pagination |
| `dnd_get_character` | Get one character by id |
| `dnd_search_characters` | Search characters by name |
| `dnd_create_character` | Create a new character |
| `dnd_update_character` | Update fields on an existing character |
| `dnd_delete_character` | Permanently delete a character |
| `dnd_get_collection_stats` | Aggregate stats (class/species distribution, level range) |

## Query Tips

- **Filtering**: `dnd_list_characters` supports `character_class`, `species`, `min_level`, and `max_level` filters. `character_class` and `species` are case-insensitive substring matches.
- **Pagination**: use `limit` and `offset` on `dnd_list_characters`. The response includes `has_more` and `next_offset`.
- **Search**: `dnd_search_characters` does a case-insensitive *literal* substring match on the name — it is not a regular expression, so `%`, `_` and `.` match themselves.
- **Response format**: all read/stat tools accept `response_format` as `"json"` (default) or `"markdown"`.
- **Ids**: get/update/delete tools require a 24-character hex id — get one from `dnd_list_characters` or `dnd_search_characters` first. Ids are case-insensitive.
- **Creating**: `name`, `character_class`, and `species` are required; `level` defaults to 1; `alignment` is optional.
- **Partial updates**: `dnd_update_character` only modifies the fields you provide; omitted fields stay unchanged.
