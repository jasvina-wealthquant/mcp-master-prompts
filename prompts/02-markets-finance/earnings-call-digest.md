# Earnings call digest

> Turns a long earnings call into what changed, what management promised, and what they avoided.

**MCPs:** web search and scrape (Firecrawl), file reader for a local transcript PDF
**Best for:** results season
**Typical cost:** 3 to 8 calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{company}}` | Company and quarter | "Infosys Q2 FY27" |
| `{{transcript}}` | URL or file path (optional) | a PDF path |

## The prompt

```text
Digest the earnings call for {{company}}.

1. Get the transcript from {{transcript}}, or search the company's investor relations
   page and exchange filings for it. Also fetch the previous quarter's transcript.
2. Read both in full.

EXTRACT
- Headline numbers mentioned on the call, with comparison to the same quarter last year
- Guidance: any target for growth, margin or capital spending, and whether it went up,
  down or stayed the same vs last quarter
- Promises from last quarter and whether this call shows they were met
- Analyst questions: the 5 most pressed topics and how directly management answered
- Tone shift: phrases that sound more cautious or more confident than last quarter,
  quoted word for word
- New topics that were not discussed last quarter

OUTPUT
1. Three line summary
2. Guidance table: Item | Last quarter | This quarter | Change
3. Promises scorecard: Promise | Kept / Partly / Not yet / Dropped
4. Hardest questions and the quality of each answer (direct / partial / dodged)
5. Notable quotes with speaker names
6. What to watch next quarter
```

## Why it works

- Comparing with last quarter is where the real signal is. A single call means little.
- The promises scorecard and the dodged answers tell you more than the headline numbers.
