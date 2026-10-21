# Codebase onboarding

> Produces a working map of an unfamiliar codebase: structure, data flow, how to run it, and where to start.

**MCPs:** filesystem or GitHub (read files, list trees), optional web search for unfamiliar libraries
**Best for:** day one on a new repo, or before a large change
**Typical cost:** 15 to 40 read calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{repo}}` | Path or owner/name | "acme/billing-service" |
| `{{goal}}` | What you need to do in it | "add a new payment provider" |

## The prompt

```text
Onboard me to {{repo}}. My goal: {{goal}}.

1. List the top level tree and read: README, any CONTRIBUTING or CLAUDE.md, the
   package or build file, CI config, and environment examples.
2. Identify the entry points (main, server start, CLI, handlers).
3. Trace one real request or job end to end through the code. Cite file:line at each hop.
4. Find where {{goal}} would touch: the modules, their tests, and any similar existing
   feature to copy from.
5. Read the git log for those files to see who changes them and how often.

OUTPUT
1. What this repo does, in 3 sentences
2. Architecture sketch (text diagram) with main modules and data flow
3. How to install, run, and test it (exact commands from the repo)
4. The traced request, hop by hop, with file:line links
5. Plan for {{goal}}: files to change, the pattern to follow, tests to add, risks
6. Things that confused you or look inconsistent
Do not edit any file.
```

## Why it works

- Tracing one real path teaches more than reading folders.
- Finding a similar existing feature gives the safest pattern to copy.
