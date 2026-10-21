# Pricing and changelog tracker

> Captures competitors' pricing and product changes in a fixed format you can diff week to week.

**MCPs:** web scrape (Firecrawl), optional change monitoring (Firecrawl monitor)
**Best for:** recurring competitive intelligence
**Typical cost:** 2 calls per site

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{urls}}` | Pricing and changelog URLs | list of URLs |
| `{{last_snapshot}}` | Last run's output (optional) | paste the previous table |

## The prompt

```text
For each URL in {{urls}}:
1. Fetch the page fresh (no cached copy).
2. Extract into JSON: product, plan name, price, billing period, currency, key limits,
   features included, any trial or discount, date fetched.
3. For changelog pages, extract entries from the last 30 days: date, title, one line summary.

If a previous snapshot is provided, compare:
{{last_snapshot}}

OUTPUT
- Current pricing table
- Changes since last snapshot: added, removed, price up, price down, limit changed
- Product changes in the last 30 days
- One paragraph: what these changes suggest about each company's strategy
- The raw JSON, so it can be saved as next week's snapshot
```

## Why it works

- A fixed JSON shape makes week to week diffing reliable.
- Asking for strategy reading turns data into a talking point.

## Variations

- **Automated:** set a change monitor on each URL and run this prompt only when it fires.
