# PDF to insights

> Reads a long PDF (report, filing, policy) and returns structured findings with page references.

**MCPs:** file parser (Firecrawl parse, filesystem PDF reader), optional web search for context
**Best for:** annual reports, regulatory circulars, research papers
**Typical cost:** 1 to 3 parse calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{file}}` | Path or URL | "annual-report-2026.pdf" |
| `{{questions}}` | What you need | "revenue mix, debt, risks, management outlook" |

## The prompt

```text
Read {{file}} in full.

1. Give the document's type, issuer, date and length.
2. Answer each of: {{questions}}. Quote the supporting passage and give the page number.
3. Pull every table with financial or statistical data into clean markdown tables.
4. List anything surprising, changed from earlier versions (if stated), or buried in
   footnotes.
5. If a question is not answered in the document, say "not in document". Do not fill
   the gap from memory.

OUTPUT
- Document card
- Answers with quotes and page numbers
- Extracted tables
- Notable footnotes and surprises
- A plain language summary in 150 words
```

## Why it works

- Page numbers make every answer checkable in seconds.
- "Not in document" stops the agent filling gaps from memory.
