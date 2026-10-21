# Campaign post mortem

> A structured, evidence based review of a finished campaign with lessons you can reuse.

**MCPs:** file reader or spreadsheet (exported metrics), web scrape (live posts and landing pages), optional analytics dashboard via browser
**Best for:** after every campaign
**Typical cost:** 5 to 10 calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{campaign}}` | Name, goal, dates | "Diwali investor webinar, goal 500 signups, 1 to 20 Oct" |
| `{{data}}` | Metrics file path or pasted table | "metrics.csv" |
| `{{assets}}` | URLs of posts, ads, landing page | list |

## The prompt

```text
Run a post mortem on {{campaign}}.

1. Read {{data}}. Compute results vs goal, cost per result, and performance by
   channel and by creative.
2. Fetch each URL in {{assets}} and record the hook, offer, visual, and call to action.
3. Line up the creative features against performance. Look for patterns, and say how
   confident you are given the sample size.

OUTPUT
1. Result vs goal, in one line
2. Channel table: Channel | Spend | Results | Cost per result | Share of results
3. Best and worst creative, with what differed between them
4. What worked, what did not, and what we cannot tell from this data
5. Five specific changes for the next campaign
6. Data we should collect next time
```

## Why it works

- Separating "what we cannot tell" stops small samples from becoming rules.
- Asking for missing data improves the next post mortem.
