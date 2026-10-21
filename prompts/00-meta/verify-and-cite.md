# Verify and cite

> A second pass that checks a draft claim by claim against live sources and marks what holds.

**MCPs:** web search and scrape (Firecrawl, Brave, Exa), plus any data source the draft relies on
**Best for:** before publishing a report, post or client note
**Typical cost:** 1 to 3 calls per claim

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{draft}}` | The text to check | a blog draft |

## The prompt

```text
You are a fact checker. Check the draft below. Do not rewrite it yet.

STEP 1: Extract every checkable claim: numbers, dates, names, quotes, rankings,
"first/largest/only" statements, and cause and effect claims. Number them.

STEP 2: For each claim, use your tools to find the best primary source (official
filing, company page, government data, original paper) and one independent source.
Fetch the page; do not rely on search snippets for numbers.

STEP 3: Give each claim a verdict:
  VERIFIED     two sources agree with the draft
  PARTLY       right direction, wrong detail (say which detail)
  OUTDATED     was true, newer data differs (give the new figure and date)
  UNSUPPORTED  no good source found
  WRONG        sources contradict it

OUTPUT
- Table: # | Claim | Verdict | Correct version | Sources (with dates)
- Count by verdict
- The draft with only the minimal edits needed, changes in **bold**
- Claims I should cut if I cannot source them myself

DRAFT:
{{draft}}
```

## Why it works

- Extracting claims first stops the agent skimming past the ones it finds dull.
- Fetching full pages for numbers avoids the classic stale snippet error.
- The OUTDATED verdict catches the most common real world mistake.

## Variations

- **Quote check:** only extract quotes and find the original recording or transcript.
