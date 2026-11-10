---
name: news
description: "Today's news from Kagi News in four sections \u2014 World, Science, United States and Boston. Tools are the 7robots portal tools prefixed news_."
---

# Kagi News

Today's edition of [Kagi News](https://news.kagi.com/), as MCP tools. Four
sections, in Kagi's own reading order: **World**, **Science**, **United States**,
**Boston**.

## What this is, and is not

A **daily edition**, not a live wire. Kagi rebuilds its feeds once each morning
around 08:00 Eastern; this server caches that edition and serves it until the next
one is due. Asking again an hour later returns the same stories. It is not a
search engine over the news archive — only today's edition exists here.

Each story is a *cluster*: Kagi has already gathered several outlets' coverage of
one event and written a summary, a Highlights list, a Perspectives section giving
differing views, and a Sources list with links. That structure survives into the
text this server returns, and the Perspectives section is usually the most
valuable part — it is where the disagreement is.

## Using it

Start with `news_list_stories`. It returns headlines only — id, title, section,
sub-topic, time, link — and is cheap enough to call speculatively. Optionally pass
`section` to limit it to one of `world`, `science`, `usa`, `boston`.

Then `news_get_story` with an id from that list, for each story worth reading.
**Do not fetch every story.** Today's edition is 32 stories and 239KB of article
text; bodies run 4-15KB each. Listing everything costs a couple of KB, reading
everything costs most of a context window.

`news_search_stories` matches a phrase against titles and sub-topics — for
finding a story you half-remember, not for research across the article text. It
says so in its own output, because "no matches" and "bodies are not searched" are
different facts.

`news_refresh` discards the cache so the next read re-fetches. It is the only tool
here that causes traffic to Kagi. You rarely need it: the cache expires on its own, and Kagi only rebuilds
once a day.

## Reading the results

Story **ids change every morning**, because they carry Kagi's own cluster id for
the day. An id from yesterday will not resolve, and the error says so rather than
reporting the story missing.

When a section's feed cannot be fetched, `sections_unavailable` appears in the
result naming it. An absent section is always reported — the alternative is a
caller believing the news was thin that day.
