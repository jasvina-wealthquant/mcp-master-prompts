# Tool discovery and capability map

> Makes the agent study its own MCP tools and produce a capability map before real work starts.

**MCPs:** any (run it after connecting new servers)
**Best for:** the first session after adding a server, or when an agent keeps picking the wrong tool
**Typical cost:** 0 to 5 harmless read calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{upcoming_work}}` | What you plan to use the tools for | "weekly stock research and social posts" |

## The prompt

```text
Before we do any real work, map your tools.

1. List every MCP server and tool you can call. Group them by server.
2. For each tool give: what it does in one line, required inputs, what it returns,
   whether it is READ ONLY, WRITES, or SPENDS CREDITS/MONEY.
3. Where it is safe and free, make one tiny test call per server (for example a
   search for "test", a profile read, a balance check) to confirm it works. Do not
   call anything that writes or spends.
4. Map the tools to this upcoming work: {{upcoming_work}}.
   For each job, name the best tool, a backup tool, and any gap where no tool fits.

OUTPUT
- Table: Server | Tool | Purpose | Inputs | Returns | Risk (read / write / spend)
- Table: Job | Best tool | Backup | Gap
- Connection problems found during testing
- Three suggestions for servers that would fill the gaps
```

## Why it works

- Agents choose better when they have just read the tool list closely.
- The risk column becomes the agent's own reminder of what needs your approval.
- The gap list tells you which server to add next.

## Variations

- **Team handover:** ask it to save the map as `TOOLS.md` in the project so the next session loads it.
