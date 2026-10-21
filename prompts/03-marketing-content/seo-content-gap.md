# SEO content gap

> Finds the topics competitors rank for that you do not, and turns them into a content plan.

**MCPs:** web search, map and scrape (Firecrawl)
**Best for:** content calendars and blog strategy
**Typical cost:** 15 to 25 calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{our_site}}` | Your domain | "example.com" |
| `{{competitor_sites}}` | 2 to 4 domains | "a.com, b.com" |
| `{{seed_topics}}` | Core topics | "PMS vs mutual funds, tax on PMS, PMS fees" |

## The prompt

```text
1. Map {{our_site}} and each of {{competitor_sites}}. List their blog and guide URLs
   with titles.
2. Cluster all titles into topics.
3. For each seed topic in {{seed_topics}} and each competitor cluster, search the web
   and note the top 5 results and whether we appear.
4. For the top 10 gaps, fetch the best ranking page and note its length, structure,
   and what it covers that we do not.

OUTPUT
1. Topic coverage matrix: Topic | Us | Competitor A | Competitor B | Who ranks
2. Top 10 gaps ranked by relevance to our customers and difficulty to win
3. For each gap: a working title, the search intent, an outline, and what would make
   ours better than what ranks now
4. Existing pages of ours that should be updated rather than replaced
```

## Why it works

- Clustering titles shows strategy, not just page counts.
- "What would make ours better" forces an angle instead of a copy.
