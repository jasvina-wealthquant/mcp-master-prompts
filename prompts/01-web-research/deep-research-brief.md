# Deep research brief

> A cited, multi angle research brief on any topic, built from live web sources.

**MCPs:** web search and scrape (Firecrawl, Brave Search, Exa)
**Best for:** getting up to speed on a market, technology or policy in one sitting
**Typical cost:** 15 to 30 tool calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{topic}}` | The question | "How is AI changing wealth management in India?" |
| `{{reader}}` | Who it is for | "a founder deciding where to invest product effort" |
| `{{recency}}` | How fresh sources must be | "last 12 months" |

## The prompt

```text
ROLE: You are a research lead preparing a brief for {{reader}}.
QUESTION: {{topic}}

TOOL PLAN
1. Break the question into 4 to 6 sub questions (market size, key players, recent
   events, regulation, risks, contrarian views). Show them.
2. For each sub question run 2 searches with different wording. Prefer results from
   {{recency}}. Note the 3 most credible results per sub question.
3. Fetch the full text of the best 8 to 12 sources. Favour primary sources: official
   data, filings, regulator pages, company announcements, research papers.
4. Look for at least one credible source that disagrees with the majority view.
5. If a page will not load, try a search for the same document elsewhere before
   dropping it.

EVIDENCE RULES
- Every key number gets a citation [publisher, date] and the year it refers to.
- Separate facts, forecasts and opinions. Label forecasts with who made them.
- Flag any source older than {{recency}}.

OUTPUT
1. Bottom line: 3 sentences a busy reader can act on
2. Key findings: 5 to 8 findings, each with evidence and citation
3. The players: table of the main companies or bodies and what they are doing
4. What the skeptics say
5. What to watch in the next 6 months
6. Open questions
7. Sources: numbered list with title, publisher, date, URL
```

## Why it works

- Sub questions stop the research from collapsing onto whatever ranks first.
- Two phrasings per sub question surface sources one query would miss.
- A required skeptics section breaks the echo of press release coverage.

## Variations

- **One page:** cut to bottom line, 5 findings and sources.
- **Academic:** require peer reviewed sources and add a methods note per finding.
