# Research to publish pipeline

> One prompt that chains research, fact checking, writing, visuals and a publish ready package.

**MCPs:** web search and scrape (Firecrawl), creative generation (Artlist or Higgsfield), optional docs or CMS (write after approval)
**Best for:** producing a sourced article with images in one session
**Typical cost:** 20 to 40 web calls plus priced generations

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{topic}}` | Article subject | "Why most investors underperform their own funds" |
| `{{audience}}` | Reader | "first time investors" |
| `{{channels}}` | Where it goes | "Substack, LinkedIn, X" |

## The prompt

```text
Run this pipeline. Pause at each GATE.

STAGE 1: RESEARCH
Follow the deep research method: sub questions, two searches each, fetch the best
8 to 12 primary sources. Output a research memo with citations.
GATE 1: show me the memo and the angle you propose.

STAGE 2: DRAFT
Write the article for {{audience}}: a hook from a real example, the argument, evidence,
the counterpoint, and a practical close. Plain language, no jargon.

STAGE 3: VERIFY
Extract every claim and check it against the sources. Fix or cut anything that is not
verified. Show the claim table.
GATE 2: show me the verified draft.

STAGE 4: VISUALS
Propose a header image and 2 to 3 supporting visuals. Write prompts. Price them.
GATE 3: approve prompts and cost. Then generate, first one alone.

STAGE 5: PACKAGE
Adapt for {{channels}} with hashtags or tags for each. Keep every caveat.
Output: final article, platform drafts, image links, sources list.
Do not publish anything. I will post it.
```

## Why it works

- Gates put your judgement at the three points where mistakes are expensive.
- Verification sits between drafting and visuals, so images never illustrate a wrong claim.
