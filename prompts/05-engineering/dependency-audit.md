# Dependency and library audit

> Checks a project's dependencies for outdated versions, known issues and maintenance risk, using live data.

**MCPs:** filesystem (read manifests), web search including developer and code indexes (Firecrawl developer search), GitHub
**Best for:** quarterly maintenance, before a release
**Typical cost:** 1 to 3 calls per key dependency

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{project}}` | Path | "./" |

## The prompt

```text
Audit dependencies in {{project}}.

1. Read the manifest and lockfile. List direct dependencies with current versions.
2. For each direct dependency, look up the latest version, release date, and repository
   activity (last commit, open issues, whether it is archived).
3. Search for known security advisories and breaking change notes between our
   version and the latest.
4. Search issue trackers for bugs that match how we use the library.

OUTPUT
- Table: Package | Ours | Latest | Behind by | Advisories | Maintenance (active / slow / abandoned)
- Urgent: anything with a security advisory affecting our version
- Upgrade plan in safe order, with breaking changes noted per step
- Packages to replace, with alternatives
All versions and dates must come from lookups made now.
```

## Why it works

- Live lookups avoid the stale "latest version" an agent remembers.
- A safe upgrade order turns the audit into a plan.
