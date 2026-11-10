---
name: huit
description: "Topic search over the Harvard University IT (HUIT) website, with page excerpts and clickable links. Tools are the 7robots portal tools prefixed huit_."
---

# huit-search

Topic search over **www.huit.harvard.edu**, the Harvard University Information
Technology site. Answers questions about Harvard IT services, tools, policies,
news, events, and staff — and always gives you a link back to the source page.

## Where the data comes from

The index is built **live** from the site's LLM sitemap,
`https://www.huit.harvard.edu/sitemap-llm` — a flat markdown list of roughly
300 entries, one per page. Every page has a markdown twin at `<url>.md`; the
server fetches those for content and strips the `.md` to produce the
human-facing link it returns to you.

The sitemap is re-fetched through Cloudflare's edge cache (~15 minutes for the
sitemap, ~24 hours for page bodies), so results track the live site. Every tool
takes `fresh: true` to bypass the cache when you need to confirm a change made
minutes ago.

### Live vs snapshot — read the provenance line

The site's bot protection sometimes refuses this server. When it does, the tools
fall back to a **bundled snapshot** of the same content rather than failing.

**Every tool response states which source answered.** Check it before you answer
a question whose truth depends on currency:

- `Source: live retrieval from …` — current, trust it.
- `Source: BUNDLED SNAPSHOT captured <date>` — content as of that date. Tell
  the user the data may be out of date whenever the answer turns on a deadline,
  a retention period, a price, an eligibility rule, or a "current" policy. Recent
  news and upcoming events are the least trustworthy in this mode.

Do not silently present snapshot content as the live state of the site.

## Content types

Each entry carries a `section`, derived from the first path segment:

| section | what it is | rough size |
| --- | --- | --- |
| `page` | services, tools, and policies — the bulk of the useful content (`/vpn`, `/okta`, `/microsoft-365`) | ~190 |
| `event` | IT Stakeholders Forums, Tech Talks, office hours | ~59 |
| `news` | announcements, security advisories, Digital Digest issues | ~42 |
| `resource`, `people`, `ai` | resource listings, HUIT staff bios, AI-specific pages | a handful each |

## Tools

- **`huit_search(query, limit, section, include_content, max_chars, fresh)`** —
  start here. Returns ranked pages, each with a clickable link and the passage
  of the page that best matches your query.
- **`huit_get_page(page, max_chars, fresh)`** — full text of one page. Takes a
  full URL or a bare path (`vpn`, `/okta`, `news/2026/05/canvas-cyber-incident`).
- **`huit_list_pages(section, contains, limit, offset, fresh)`** — browse the
  index without scoring. Use it to enumerate a section or when a search comes
  back empty.

## How search actually works — and how to query it well

Two passes. First all ~300 titles and slugs are scored against your keywords;
then the top handful of candidates have their **full page text** fetched and
re-scored, which is what lets a query find a page whose title never mentions
your term.

It is **keyword matching, not semantic search**. That has direct consequences
for how you should query:

- **Use distinctive nouns, not sentences.** `zoom recording retention` works;
  `how long does Harvard keep my Zoom recordings?` dilutes the signal with
  words that match everything.
- **Try synonyms before giving up.** The site says "Harvard Phone", not "VoIP";
  "HarvardKey", not "SSO"; "Kiteworks", not "secure file transfer". A single
  empty result means the words were wrong at least as often as it means the
  content is missing.
- **Drop the `section` filter when unsure.** Many service pages you would
  expect under `news` live under `page`.
- **`include_content: "none"` is much faster** — use it when you only need to
  find the right page, then follow up with `huit_get_page`.
- **Widen, then narrow.** `huit_list_pages(contains: "zoom")` is often the
  fastest way to see everything on a topic.

## Reporting results

Always give the user the link. The `pageUrl` in every result is the real
human-facing page and is safe to hand over directly.

Excerpts are extracted from the page body around the best keyword match — they
are context, not necessarily the complete answer. When a question turns on a
detail (eligibility, a retention period, a dollar figure), call
`huit_get_page` and read the whole page before answering.

## Limits worth knowing

- Only public www.huit.harvard.edu content that appears in the sitemap is
  reachable. Pages behind HarvardKey, ServiceNow articles, and anything not
  listed in the sitemap are not indexed.
- The site is fronted by bot protection; if a page fetch fails, the result still
  includes the title and link so you can hand the user the URL.
- Content is generated from the site's markdown twins, so tables and complex
  layouts flatten into prose. If an excerpt reads oddly, fetch the page.
