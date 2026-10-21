# The 10 principles of MCP prompting

These are the rules every prompt in this repo is built on. Use them to adapt the prompts or write your own.

## 1. Discover before you act

An agent that has not listed its tools will guess. Ask it to inventory the tools it has, note what each one returns, and pick a plan from that inventory. This takes one turn and saves many.

## 2. Name the tool type, then allow substitutes

Write "use the web search tool (for example Firecrawl search)" rather than a hard coded function name. The prompt keeps working when someone swaps servers.

## 3. Live data beats memory

Any number that can change (a price, a star count, a version, a date) must come from a tool call in this session. Tell the agent to label anything it could not fetch as "not verified".

## 4. Breadth first, then depth

Search wide with cheap calls (search results, snippets, file listings). Then spend the expensive calls (full scrapes, long reads, generations) only on the few items that matter.

## 5. Two sources for every important claim

One source is an anecdote. Ask for at least two independent sources on any claim that drives a conclusion, and ask the agent to say so when it could only find one.

## 6. Make conflicts visible

When sources disagree, the agent should show both and explain which it trusts and why. Hiding a conflict is worse than not finding the answer.

## 7. Gate every side effect

Reads are free. Writes, posts, orders, generations and anything that spends credits need a written preview and an explicit "yes" from the user. Put this rule in the prompt, every time.

## 8. Budget the run

Give a ceiling on tool calls, credits or time. Ask the agent to report what it spent. This stops runaway loops and makes runs comparable.

## 9. Fix the output contract

Specify the sections, their order, and the format. A fixed shape makes results easy to scan, compare week to week, and feed into the next prompt in a chain.

## 10. End with what is still unknown

Every analysis has gaps. A short "open questions" or "what would change my mind" section keeps the reader honest and points to the next run.

---

### A reusable skeleton

```text
ROLE: You are {{role}}. Your goal is {{goal}}. Done means {{definition of done}}.

TOOLS: First list the tools you have that can {{capability}}. Plan which to use.
  Step 1: {{cheap, wide call}}
  Step 2: {{targeted, deeper call}}
  If a tool fails or returns nothing, {{fallback}}.

EVIDENCE: Every number comes from a tool call in this session, with its source and time.
  Important claims need two independent sources. Show conflicts.

GUARDRAILS: Do not {{side effect}} without showing me a preview and getting a yes.
  Stay under {{budget}}. Report what you used.

OUTPUT:
  1. {{section}}
  2. {{section}}
  3. Open questions
```
