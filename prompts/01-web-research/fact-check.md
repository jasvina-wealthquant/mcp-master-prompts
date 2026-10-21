# Fact check a claim

> Traces a single claim back to its origin and gives a clear verdict with evidence.

**MCPs:** web search and scrape (Firecrawl, Brave, Exa)
**Best for:** viral stats, forwarded messages, quotes in a draft
**Typical cost:** 5 to 12 calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{claim}}` | The exact claim | "90% of retail traders lose money in F&O" |

## The prompt

```text
CLAIM: "{{claim}}"

1. Restate the claim precisely: who, what number, what period, what place.
2. Search for the claim in several phrasings. Find the earliest appearance you can.
3. Trace it back to the original source (study, filing, official data, speech).
   Fetch that source and read the relevant section.
4. Check whether the original actually says what the claim says. Look for changes
   in number, period, population or wording along the way.
5. Find the latest figure on the same question from an authoritative source.

VERDICT (pick one): TRUE / MOSTLY TRUE / MISLEADING / OUTDATED / FALSE / UNPROVEN

OUTPUT
- Verdict and one sentence why
- The original source: title, publisher, date, link, and the exact supporting line
- How the claim drifted from the original (if it did)
- The most current figure, with source and date
- A corrected version of the claim I can safely use
```

## Why it works

- Precise restating exposes vague claims before any search.
- Tracing to the origin catches the drift that most viral stats go through.
- The corrected version gives you something usable, not just a no.
