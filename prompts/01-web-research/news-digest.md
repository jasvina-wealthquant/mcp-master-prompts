# News digest on a topic

> A deduplicated, ranked digest of what actually happened on a topic over a set period.

**MCPs:** web or news search (Firecrawl search with news source, Brave News), scrape
**Best for:** daily or weekly briefings
**Typical cost:** 8 to 15 calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{topic}}` | Subject | "SEBI regulation for investment advisers" |
| `{{period}}` | Window | "last 7 days" |
| `{{reader}}` | Who reads it | "a PMS marketing team" |

## The prompt

```text
Build a news digest on {{topic}} for {{period}}, written for {{reader}}.

1. Run at least 4 news searches with different angles (official, industry, market
   impact, criticism). Keep only items inside {{period}}.
2. Group articles that report the same event. Keep the most original source for each
   event (the regulator, the company, the first outlet to report).
3. Fetch the primary source for the top events and confirm the key facts.
4. Rank events by impact on {{reader}}, not by how many outlets covered them.

OUTPUT
- Headline of the week (one sentence)
- Top events (max 7): what happened, why it matters to {{reader}}, source and date
- Smaller items worth knowing (bullets)
- What to watch next
- Note any event where reports conflict
```

## Why it works

- Grouping by event kills the duplicate coverage that bloats most digests.
- Ranking by impact on the reader makes it a briefing, not a feed.
