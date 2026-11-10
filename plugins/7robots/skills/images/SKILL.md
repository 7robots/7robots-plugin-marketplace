---
name: images
description: "Generate images from text prompts using OpenAI's GPT image generation. Tools are the 7robots portal tools prefixed images_."
---

# GPT Image Generator

MCP server for generating images from natural language prompts using OpenAI's image generation API (GPT Image 2.5). Images are stored in Cloudflare R2 and a public URL is returned.

## Available Tools

| Tool | Purpose |
|------|---------|
| `images_generate_image` | Generate an image from a text prompt |

## Tool Details

### images_generate_image

**Parameters:**
- `prompt` (str, required): Description of the image to generate
- `model` (str, optional): `"gpt-image-2.5-flare"` (default; faster, everyday generation) or `"gpt-image-2.5-sunburst"` (precision-oriented). Same per-token price.

**Returns:** A bare public R2 URL to the generated image.

## Limits

Each caller may generate a few images a minute and 40 per UTC day; a refusal
names the limit hit and when it resets.

## Critical: Always Return the Image URL

When you call `images_generate_image`, the tool returns a URL (e.g., `https://pub-xxx.r2.dev/generated_images/uuid.png`). You **MUST** include this full URL in your response to the user. Without it, the user has no way to view the image they requested.

- Copy the exact URL from the tool result and include it as a clickable markdown link in your reply.
- Do this **every time** — never summarize the result as "I generated an image" without the URL.
- Write down the URL immediately when you receive it, as tool results may be cleared from context later.
- If the tool returns an error instead of a URL, show the error message to the user.

## Other Notes

- The tool returns only the bare URL — there is no other content to summarize.
- The URL is always a public `https://` R2 URL.
