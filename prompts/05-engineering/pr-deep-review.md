# PR deep review

> A correctness focused pull request review that reads surrounding code, not just the diff.

**MCPs:** GitHub (read PR, diff, files, checks), filesystem
**Best for:** non trivial PRs
**Typical cost:** 10 to 25 reads

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{pr}}` | PR link or number | "acme/app#482" |

## The prompt

```text
Review {{pr}}.

1. Read the PR description, linked issue, the full diff, and CI results.
2. For each changed function, read its callers and the full file around it.
3. Look for: logic errors, missed edge cases (empty, null, zero, very large, concurrent),
   error handling gaps, security issues (input validation, secrets, injection, auth),
   breaking changes to public interfaces, missing or weak tests, and performance traps.
4. For every finding, describe a concrete input or state that causes the failure. If you
   cannot, drop it or mark it as a question.

OUTPUT
- Summary: what the PR does and whether it does it
- Findings, most severe first: file:line | issue | failure scenario | suggested fix
- Questions for the author
- Verdict: approve / approve with nits / request changes

Do not post comments. I will decide what to post.
```

## Why it works

- Requiring a failure scenario removes vague, style only feedback.
- Reading callers catches the bugs a diff only review misses.
