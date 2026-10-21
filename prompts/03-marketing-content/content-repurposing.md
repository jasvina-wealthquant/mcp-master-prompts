# Content repurposing engine

> Turns one long piece into platform native posts that keep the nuance of the original.

**MCPs:** web scrape (to pull the source article), optional file reader
**Best for:** getting a week of posts out of one article, video or report
**Typical cost:** 1 to 2 calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{source}}` | URL or text | a Substack article URL |
| `{{platforms}}` | Where it goes | "LinkedIn, X thread, Instagram carousel, Reddit" |
| `{{voice}}` | Voice notes | "first person, calm, no hype" |

## The prompt

```text
1. Fetch {{source}} and read it fully.
2. Extract: the core argument in one sentence, the 5 strongest specific points (with
   numbers or examples), the best story or anecdote, and the one caveat the author
   took care to include.
3. Write for each of {{platforms}} in its native format:
   - LinkedIn: 150 to 250 words, a hook in the first line, short paragraphs, 3 to 5 hashtags
   - X: a thread of 5 to 8 posts, each standing alone, hashtags on the last post
   - Instagram carousel: 7 to 9 slides, one idea per slide, under 25 words each,
     plus a caption
   - Reddit: a discussion post with no marketing tone, ending in a genuine question

RULES
- Voice: {{voice}}.
- Keep the caveat. Short form should not be more confident than the source.
- Avoid colon led stat lists, three part slogans, and paired punchlines. Write it the
  way a person would talk.
- Every number must match the source exactly.

OUTPUT
- Each platform's draft under its own heading
- A table checking that every number used appears in the source
```

## Why it works

- Extracting the caveat first is what stops short posts turning into hype.
- The number check table catches rounding drift between versions.
