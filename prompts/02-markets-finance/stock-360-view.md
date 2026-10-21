# Stock 360 view

> A complete, plain language view of one listed company: business, numbers, price action, news and risks.

**MCPs:** broker or market data (Zerodha Kite, Alpaca, Polygon), web search and scrape (Firecrawl)
**Best for:** deciding whether a stock deserves deeper work, or writing about it for a general audience
**Typical cost:** 4 to 6 market data calls, 10 to 20 web calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{company}}` | Name and ticker | "Tata Motors (NSE: TATAMOTORS)" |
| `{{reader}}` | Who reads it | "a first time investor" |

## The prompt

```text
ROLE: You are an equity research analyst writing for {{reader}}. This is research,
not a recommendation. Never place or suggest placing an order.

COMPANY: {{company}}

TOOL PLAN
1. Market data tool: search the instrument to get the exact symbol. Pull the latest
   quote and daily price history for 1 year. Compute: 52 week high and low, distance
   from each, 1 month / 3 month / 1 year return, and average daily volume vs the last
   5 days.
2. Pull the same history for the main index (for example Nifty 50) and compare returns.
3. Web: fetch the latest quarterly results, the latest investor presentation, and the
   most recent earnings call transcript or summary.
4. Web: search news from the last 90 days. Keep items about results, management,
   orders, regulation, debt, or major holders buying or selling.
5. Web: identify 2 or 3 listed peers and fetch their headline numbers for comparison.

EVIDENCE RULES
- Prices come from the market data tool with a timestamp. Financials come from
  company filings or exchange disclosures, with the quarter they refer to.
- Explain every ratio in plain words the first time ("price to earnings: how many
  years of current profit you pay for the share").
- Pick ratios that fit the business type: lending businesses by asset quality and
  return on assets, manufacturers by margins and debt, platforms by growth and cash burn.

OUTPUT
1. The business in 3 sentences: what it sells, to whom, how it makes money
2. Numbers that matter: table of revenue, profit, margin, debt, and 2 sector specific
   measures across the last 4 quarters, with peers
3. Price action: returns vs index, where it sits in its 52 week range, volume trend
4. What changed recently: the 3 to 5 news items that matter and why
5. What management is saying: key points from the latest call
6. The bull case and the bear case, 3 points each, all evidence based
7. Risks to watch
8. Open questions
Footer: "Research only, not investment advice. Data as of {{timestamp}}."
```

## Why it works

- Live prices and filed financials come from different tools, and the prompt keeps them apart.
- Business type specific ratios avoid judging a bank like a factory.
- A forced bear case is the best protection against narrative bias.

## Variations

- **Social post:** add "then write a 150 word plain language summary with no ratios in it".
- **Peer table only:** skip sections 4 to 7.
