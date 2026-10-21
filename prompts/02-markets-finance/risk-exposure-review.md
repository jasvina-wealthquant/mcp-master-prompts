# Risk and exposure review

> Stress tests holdings against specific scenarios using live prices and real history.

**MCPs:** broker (holdings, positions), market data (historical), web search
**Best for:** before an event (budget, rate decision, election) or after a sharp fall
**Typical cost:** 5 to 15 calls

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{scenarios}}` | What to test | "market falls 10 percent; IT sector falls 15 percent; rupee weakens 5 percent" |

## The prompt

```text
ROLE: Read only risk reviewer. No orders of any kind.

1. Fetch holdings and positions. Compute weights.
2. Pull 1 year daily history for each holding and the benchmark. For each holding
   compute how much it typically moves when the benchmark moves (beta, explained in
   plain words), its worst single day, and its largest peak to trough fall.
3. For each scenario in {{scenarios}}, estimate the impact on each holding and the
   whole portfolio. Show the method in one line per scenario.
4. Search the news for any holding with a scheduled event in the next 30 days
   (results, record dates, regulatory decisions).

OUTPUT
1. Risk snapshot: portfolio beta, worst day in the last year, largest fall
2. Scenario table: Scenario | Estimated portfolio impact (money and percent) | Top 3 contributors
3. Holdings that carry the most risk relative to their weight
4. Upcoming events by holding
5. Limits of this analysis (history is not a forecast, correlations change in a crisis)
Footer: "Estimates from historical data. Not investment advice."
```

## Why it works

- Scenario maths is shown, so you can check it rather than trust it.
- The limits section is required, because stress tests are often over read.
