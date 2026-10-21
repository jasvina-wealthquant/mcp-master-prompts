# Sector rotation scan

> Shows which sectors are gaining or losing strength against the broad market, using live index data.

**MCPs:** market data (Zerodha Kite historical data, Polygon), web search for drivers
**Best for:** weekly or monthly market reviews
**Typical cost:** 1 history call per sector index plus a few web calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{benchmark}}` | Broad index | "Nifty 50" |
| `{{sectors}}` | Sector indices | "Nifty Bank, IT, Pharma, Auto, FMCG, Metal, Realty, Energy" |

## The prompt

```text
1. Search the instruments to get exact symbols for {{benchmark}} and each of {{sectors}}.
2. Pull daily history for 6 months for each.
3. For each sector compute: 1 week, 1 month, 3 month, 6 month return; the same for
   the benchmark; and the difference (sector return minus benchmark return).
4. Compute a relative strength line (sector price divided by benchmark price) and say
   whether it is rising, flat or falling over the last 4 weeks.
5. Put each sector in one of four boxes:
   LEADING    beating the market and the lead is growing
   WEAKENING  beating the market but the lead is shrinking
   LAGGING    trailing the market and falling further behind
   IMPROVING  trailing the market but catching up
6. For the two biggest movers each way, search the news for the likely driver.

OUTPUT
- Table: Sector | 1W | 1M | 3M | 6M | vs benchmark (3M) | Trend | Box
- The four boxes, listed
- Drivers for the biggest movers, with sources
- One paragraph in plain language on what the market is rewarding right now
Footer: "Market data as of {{timestamp}}. Research, not advice."
```

## Why it works

- All numbers are computed from fetched history, so nothing is recalled.
- Four plain boxes explain rotation without technical jargon.
