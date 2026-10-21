# Weekly market wrap

> A Friday wrap of index moves, sector leaders, big stock movers and the news behind them.

**MCPs:** market data (Zerodha Kite), web and news search (Firecrawl)
**Best for:** a weekly newsletter or social series. Run after market close.
**Typical cost:** 10 to 15 market data calls, 6 to 10 web calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{market}}` | Market and indices | "India: Nifty 50, Sensex, Nifty Midcap 100, Nifty Smallcap 100" |
| `{{week}}` | Dates | "13 to 17 Oct 2026" |
| `{{watchlist}}` | Stocks to scan for big movers | "Nifty 50 constituents" |

## The prompt

```text
Write the weekly market wrap for {{market}}, week of {{week}}.

DATA
1. Pull daily closes for each index for the week plus the previous Friday.
   Compute weekly change and the best and worst day.
2. Pull the same for main sector indices. Rank by weekly change.
3. Pull quotes for {{watchlist}}. List the 5 biggest gainers and 5 biggest losers.
4. Search news for the week: central bank, inflation or jobs data, foreign fund flows,
   global cues, big results, policy moves.
5. Match each major move to its likely driver, with a source. If no driver is clear,
   say so.

OUTPUT
1. The week in one line
2. Index table: Index | Close | Weekly change | Best day | Worst day
3. Sector leaders and laggards
4. Biggest stock movers with one line on why
5. What drove the week (3 to 5 points, sourced)
6. Calendar for next week: data releases, results, events
7. Optional drafts: a 280 character post, a 120 word LinkedIn post
Footer: "Data as of market close {{date}}. Not investment advice."
```

## Why it works

- Matching every move to a sourced driver separates explanation from guesswork.
- A fixed structure means readers learn where to look each week.
