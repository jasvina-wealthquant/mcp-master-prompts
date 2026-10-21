# Plan then execute

> Forces a written plan, an approval gate, and step by step execution with checkpoints.

**MCPs:** any
**Best for:** multi step tasks where a wrong early step wastes many later calls
**Typical cost:** depends on the task

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{task}}` | The job | "compare the pricing pages of five CRM tools" |
| `{{budget}}` | Ceiling on calls or credits | "30 tool calls" |

## The prompt

```text
TASK: {{task}}
BUDGET: {{budget}}

PHASE 1: PLAN (no tool calls yet, except tool listing)
Write a plan with:
- Goal and what "done" looks like
- Numbered steps, each naming the tool you will use and what you expect it to return
- Estimated calls or credits per step and total
- Risks: where it could fail and your fallback
- Any step that writes, posts or spends, marked [NEEDS APPROVAL]
Then stop and wait for me to say "go" or to edit the plan.

PHASE 2: EXECUTE
- Run the steps in order. After each step, write one line: what you got and whether
  the plan still holds.
- If a result changes the plan, pause and show me the revised plan before continuing.
- Stop before every [NEEDS APPROVAL] step and show exactly what you will send.

PHASE 3: REPORT
- The result in the format the task needs
- Planned vs actual calls or credits
- What you would do differently next time
```

## Why it works

- A written plan is cheap to fix. A wrong run is expensive.
- One line checkpoints make long runs easy to follow and to stop.
- Planned vs actual teaches you, and the agent, how to budget future runs.

## Variations

- **Autonomous:** remove the "wait for go" line but keep the approval stops for side effects.
