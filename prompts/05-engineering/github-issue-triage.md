# GitHub issue triage

> Sorts an issue backlog into duplicates, bugs, features and stale items, with suggested labels.

**MCPs:** GitHub (list issues, read comments, search code; write only after approval)
**Best for:** weekly backlog grooming
**Typical cost:** 1 list call plus 1 to 2 reads per issue

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{repo}}` | owner/name | "acme/app" |
| `{{filter}}` | Which issues | "open, unlabeled, last 60 days" |

## The prompt

```text
Triage issues in {{repo}} matching: {{filter}}.

For each issue:
1. Read the body and comments.
2. Search existing issues for duplicates. Search the code for the area it mentions.
3. Classify: BUG (with reproduction steps or not), FEATURE, QUESTION, DUPLICATE (of #),
   STALE (no activity in 60 days and unclear), or NEEDS INFO.
4. Estimate severity for bugs (blocks users / degrades / cosmetic) and name the likely
   code area with a file link.

OUTPUT
- Table: # | Title | Type | Severity | Area | Suggested labels | Suggested action
- Duplicate groups
- Top 5 to fix first, with reasoning
- Draft replies for NEEDS INFO issues

Do not label, comment, close or assign anything. Show me the list of proposed
changes and wait. Apply only the ones I approve.
```

## Why it works

- Duplicate search before classifying shrinks the backlog fast.
- Proposed changes in one list make approval quick and safe.
