# Spreadsheet analyst

> Explores a CSV, spreadsheet or database table and reports trends, outliers and answers, with the method shown.

**MCPs:** filesystem, spreadsheet or SQL server (SQLite, Postgres), optional code execution
**Best for:** quick analysis without opening a BI tool
**Typical cost:** a few reads and queries

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{data}}` | File or table | "leads_q3.csv" |
| `{{question}}` | What to find out | "which channels bring leads that convert" |

## The prompt

```text
Analyse {{data}} to answer: {{question}}

1. Profile the data: rows, columns, types, missing values, date range, obvious errors.
   Show this before analysing.
2. State the method you will use and any cleaning steps.
3. Run the analysis. Show the query or code you used for every number.
4. Check the result: does it hold if you remove outliers, or split by time period?

OUTPUT
- Data profile and quality issues
- Answer in 2 sentences
- Supporting tables (and a chart spec if useful)
- Robustness check
- Caveats and what extra data would help
```

## Why it works

- Profiling first catches broken data before it produces confident nonsense.
- Showing the query makes every number reproducible.
