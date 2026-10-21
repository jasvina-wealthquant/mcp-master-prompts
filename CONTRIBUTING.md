# Contributing

Thanks for helping make agents better at using their tools.

## Adding a prompt

1. Copy [PROMPT_TEMPLATE.md](PROMPT_TEMPLATE.md) into the right folder under `prompts/`.
2. Name the file in lowercase words joined by hyphens, for example `churn-analysis.md`.
3. Fill every section. The prompt block must include a tool plan, evidence rules, guardrails and an output contract.
4. Name tool **types** with example servers, not one vendor's function names.
5. Test it at least twice against a real MCP server and note in the PR which servers and client you used.
6. Add a line to the catalog in [README.md](README.md) and bump the prompt count badge.

## Quality checklist

- [ ] Any number that can change is fetched live, not recalled
- [ ] Important claims need two sources
- [ ] Every write, post, order or paid generation has a confirm step
- [ ] There is a budget or call ceiling
- [ ] The output has a fixed structure and ends with open questions
- [ ] No API keys, personal data or account numbers anywhere

## Finance prompts

Prompts in `02-markets-finance/` must stay read only. They must never place, modify or cancel orders, and their output must say it is research, not advice.

## Style

Plain English. Short sentences. Explain any acronym the first time it appears.
