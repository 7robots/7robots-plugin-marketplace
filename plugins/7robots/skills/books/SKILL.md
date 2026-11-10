---
name: books
description: "MCP server for managing Micro.blog book collections \u2014 bookshelves, books, and reading goals. Tools are the 7robots portal tools prefixed books_."
---

# Micro.blog Bookshelf Database

MCP server for managing Micro.blog book collections. Use these tools to manage bookshelves, add/remove books, and track reading goals.

## Data Model

- **Bookshelves** contain books. Each bookshelf has an `id` and a `name`.
- **Books** belong to a bookshelf. Each book has an `id`, `title`, `author`, optional `isbn`, and optional `cover_url`.
- **Reading Goals** track yearly reading targets with a `goal_id`, `value` (target), and `progress` (current count).

## Available Tools

### Bookshelf Management

| Tool | Description |
|------|-------------|
| `books_get_bookshelves` | List all bookshelves |
| `books_get_bookshelf_books(bookshelf_id)` | List books in a bookshelf |
| `books_add_bookshelf(name)` | Create a new bookshelf |
| `books_rename_bookshelf(bookshelf_id, name)` | Rename an existing bookshelf |

### Book Management

| Tool | Description |
|------|-------------|
| `books_add_book(title, author, bookshelf_id, isbn?, cover_url?)` | Add a book to a bookshelf |
| `books_move_book(book_id, bookshelf_id)` | Move a book to a different bookshelf |
| `books_remove_book(bookshelf_id, book_id)` | Remove a book from a bookshelf |
| `books_change_book_cover(bookshelf_id, book_id, cover_url)` | Update a book's cover image |

### Reading Goals

| Tool | Description |
|------|-------------|
| `books_get_reading_goals` | List all reading goals |
| `books_get_goal_progress(goal_id)` | Get progress toward a specific goal |
| `books_update_reading_goal(goal_id, value, progress?)` | Update a goal's target or progress |

## Query Tips

- Always call `books_get_bookshelves` first to discover available bookshelf IDs before operating on books.
- Use `books_get_bookshelf_books` to find a book's ID before moving, removing, or updating its cover.
- When adding a book, `isbn` and `cover_url` are optional — provide them if available for richer metadata.
- Reading goals are typically yearly. Use `books_get_reading_goals` to find the goal ID, then `books_update_reading_goal` to adjust the target or log progress.
