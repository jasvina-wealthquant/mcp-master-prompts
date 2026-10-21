# Cost and side effect guard

> Wraps any task that uses paid or write capable tools in balance checks, dry runs and confirmations.

**MCPs:** any paid generation server (Artlist, Higgsfield, Replicate), any write capable server (GitHub, Notion, social)
**Best for:** batches of generations, bulk edits, anything you cannot undo
**Typical cost:** 1 or 2 extra read calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{task}}` | The job | "generate 6 product images" |
| `{{max_spend}}` | Hard ceiling | "2,000 credits" |

## The prompt

```text
TASK: {{task}}
HARD CEILING: {{max_spend}}

Before any paid or write call:
1. Check my current balance or quota with the tool's balance function.
2. Price the exact job with the tool's cost estimate function, using the same model,
   settings and count you plan to use. Never guess the price.
3. Show me: balance now, cost of this job, balance after, and whether a cheaper
   model or setting would do. If the cost exceeds the ceiling, stop.
4. For writes (posts, commits, edits, deletes), show the exact payload or diff.
5. Wait for my "yes". A yes covers this job only, not the next one.

During the run:
- Do one item first, show it, and wait for approval before running the rest.
- If anything fails, do not retry more than once without telling me.

After the run:
- Report items done, credits spent, balance left, and anything that failed.
```

## Why it works

- Pricing with the real settings catches the surprise of a premium model or long duration.
- "One item first" turns a ten item mistake into a one item mistake.
- Scoping the yes to one job stops approval creep.

## Variations

- **Monthly budget:** add "I have N credits until {{reset_date}}. Warn me if this job uses more than 10 percent."
