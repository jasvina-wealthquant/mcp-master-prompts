# Meeting notes to actions

> Turns a transcript or rough notes into decisions, owners, deadlines and follow up drafts.

**MCPs:** filesystem or docs (Google Drive, Notion), optional task tracker (write after approval)
**Best for:** right after a meeting
**Typical cost:** 1 to 3 calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{notes}}` | File or pasted text | "call-2026-10-21.txt" |

## The prompt

```text
Read {{notes}}.

OUTPUT
1. Decisions made (who decided, word for word where possible)
2. Action items: Task | Owner | Deadline | Source line
   If owner or deadline is unclear, write "unassigned" or "no date". Do not invent.
3. Open questions and disagreements left unresolved
4. A follow up message summarizing the above in under 150 words

If a task tracker is connected, show the tasks you would create and wait for my yes.
```

## Why it works

- Linking each action to a source line makes disputes quick to settle.
- Refusing to invent owners avoids assigning work to the wrong person.
