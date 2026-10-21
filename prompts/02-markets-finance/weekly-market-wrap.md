# Weekly market wrap

> A Friday wrap of index and sector moves, the news behind them, next week's calendar, and ready to post drafts plus a set of notebook style images.

**MCPs:** market data (Zerodha Kite historical data and LTP), web and news search (Firecrawl), filesystem, optional headless browser to render images
**Best for:** a weekly newsletter or social series. Run on Friday after market close.
**Typical cost:** about 15 market data calls, 6 to 10 web calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{indices}}` | Broad indices plus a volatility index | "Nifty 50, Nifty Bank, Nifty Midcap 100, Nifty Smallcap 100, India VIX" |
| `{{sectors}}` | Sector indices | "IT, Auto, Pharma, FMCG, Metal, Realty, PSU Bank" |
| `{{week}}` | The Friday date | "16 Oct 2026" |
| `{{reader}}` | Who it is for | "everyday investors, no jargon" |
| `{{last_wrap}}` | Last week's output file (optional) | "wraps/2026-10-09.json" |

## The prompt

```text
Build the weekly market wrap for the week ending {{week}}, for {{reader}}.

STEP 1: CHECK THE SESSION
Call the market data tool for the Nifty 50 LTP. If it fails, ask me to log in again
and wait. Broker sessions expire daily.

STEP 2: DATA (run these calls in parallel)
- Daily candles for about 12 calendar days for every index in {{indices}} and every
  sector in {{sectors}}. If an instrument token fails, look it up with instrument
  search or drop that sector and say so.
- Weekly change = this Friday's close against the LAST TRADING DAY before this week.
  Watch for holidays: that is not always last Friday.
- Daily change for each day of the week, plus best and worst day.
- Nifty 50 daily candles for about 6 weeks, for the month trend and any 52 week
  high or low.
- If it is before market close, label every figure "intraday as of HH:MM".

STEP 3: WHY IT MOVED
Search the week's news: central bank, foreign fund flows, crude oil, global yields,
results season, the biggest index movers. Write 2 or 3 plain paragraphs. Cite 2 or 3
sources. Never invent a cause. If the reason is unclear, say so.

STEP 4: NEXT WEEK
Search for next week's data releases, policy meetings and major results dates.
Never guess a date. Only list what a source confirms.

STEP 5: DRAFTS
- LinkedIn: 150 to 220 words, warm and human, ends on a genuine question, 4 to 6 hashtags
- X: one sharp observation and a question, 2 to 4 hashtags
- Instagram carousel: 5 or 6 slides of one or two short sentences each, plus a caption
  ending "For education only. Not investment advice." and hashtags
Write like a person. No colon led stat lists, no three part slogans, no internal
jargon. Explain any market term in a few words.

STEP 6: NOTEBOOK IMAGES (optional)
Render 4 portrait pages (1080 x 1620, at 2x) in a calm notebook style:
1 the big picture, 2 why it moved, 3 sector by sector, 4 what to watch plus a short
glossary of terms that came up this week and the disclaimer.
After rendering, look at every image. Fix clipped labels, overlapping text and empty
gaps, then render again.

COMPLIANCE
Use index and sector data only. Never use personal holdings, client data or any
fund's performance. No buy or sell calls on named stocks.

OUTPUT
- wraps/{{week}}.json with all numbers, sources and drafts (same shape as {{last_wrap}})
- wraps/{{week}}.html, a page with the tables, charts and drafts
- The notebook images, if made
- A 3 line summary of the week for me, and any figure that rests on a single source
```

## Why it works

- **Holiday aware weekly change.** The most common wrap error is comparing to a Friday that was a market holiday.
- **One JSON per week.** Saving data and drafts in a fixed shape makes the next week faster and lets you chart trends across months.
- **Never guess a date.** The calendar section is where agents most often make things up.
- **Look at the images.** Rendered charts often clip labels. Asking the agent to inspect its own output catches that before you post.

## Variations

- **US market:** swap in S&P 500, Nasdaq 100, Russell 2000, VIX and the SPDR sector funds.
- **Daily close note:** cut to one day, two drafts, no images.
