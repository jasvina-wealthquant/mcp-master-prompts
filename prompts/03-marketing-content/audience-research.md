# Audience research

> Finds what a target audience actually asks, worries about and says, in their own words.

**MCPs:** web search and scrape (Firecrawl), optional Reddit or forum search
**Best for:** messaging, content planning, ad copy
**Typical cost:** 12 to 20 calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{audience}}` | Who | "salaried professionals in India with 50 lakh plus to invest" |
| `{{category}}` | What you sell | "portfolio management services" |

## The prompt

```text
Research how {{audience}} think and talk about {{category}}.

1. Search forums, Reddit, Q&A sites, review sites, YouTube comments and news comment
   sections for discussions from the last 12 months. Use the words a customer would
   use, not industry terms.
2. Fetch the 10 to 15 richest threads. Read the replies, not just the post.
3. Collect verbatim quotes. Tag each: question, fear, desire, objection, misconception,
   or praise.

OUTPUT
1. Top 10 questions they ask, in their words, ranked by how often they appear
2. Fears and objections, each with 2 real quotes and links
3. What they want, in their words
4. Words and phrases they use (and industry jargon they never use)
5. Misconceptions worth correcting
6. 10 content ideas, each answering a real question, with the source thread
```

## Why it works

- Customer words beat marketer words for search, ads and headlines.
- Reading replies surfaces the objections the original poster did not think of.
