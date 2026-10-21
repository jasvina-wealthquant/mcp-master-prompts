# Market signal to content pipeline

> Spots a notable market move with live data, explains it with sourced news, and drafts compliant educational content.

**MCPs:** market data (Zerodha Kite), web and news search (Firecrawl), optional creative generation
**Best for:** timely, educational market content for a regulated financial brand
**Typical cost:** 10 to 20 market data calls, 6 to 12 web calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{universe}}` | What to scan | "Nifty 50 constituents and sector indices" |
| `{{rules}}` | Compliance rules | "educational only, no buy or sell calls, no return promises, include disclaimer" |

## The prompt

```text
STAGE 1: SCAN (read only, no orders ever)
Pull today's quotes and 3 month history for {{universe}}. Flag unusual moves:
a daily move over 2x its average absolute daily move, a new 52 week high or low,
or volume over 2x the 20 day average. Rank the top 5.

STAGE 2: EXPLAIN
For each flagged move, search news from the last 3 days. Find the most likely driver
from a primary source (exchange filing, company release, regulator). If none is clear,
say "no clear driver" and drop it from content.

STAGE 3: PICK
Choose the one move that best teaches a general investor something lasting
(how results move prices, what a rate decision does, why sectors rotate).
Explain your pick.

STAGE 4: DRAFT
Write a short educational post (LinkedIn 150 words, X 3 posts) that uses the move as
an example of the lesson. Follow {{rules}}. No price targets, no "should buy/sell".
End with the disclaimer.

STAGE 5: CHECK
List every number used with its source and timestamp. Check the draft against
{{rules}} line by line and report pass or fail for each rule.

OUTPUT: scan table, drivers with sources, chosen lesson, drafts, compliance check.
```

## Why it works

- The scan is rule based and fetched, so the story starts from data, not a hunch.
- Dropping moves with no clear driver avoids inventing explanations.
- A line by line compliance check is built in, not left to memory.
