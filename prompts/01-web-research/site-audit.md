# SEO and site audit

> A prioritized SEO and content audit of a website built from real crawled pages.

**MCPs:** web map and crawl (Firecrawl), scrape, optional browser automation
**Best for:** before a redesign, or a quarterly health check
**Typical cost:** 1 map call plus 15 to 30 page fetches

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{site}}` | Root URL | "https://example.com" |
| `{{keywords}}` | Terms you want to rank for | "portfolio management service, PMS India" |

## The prompt

```text
Audit {{site}} for search and content quality. Target keywords: {{keywords}}.

1. Map the site and list all URLs. Group them by section.
2. Pick a sample: home, top 5 commercial pages, 5 blog posts, and any page that
   matches a target keyword. Fetch each one.
3. For each page record: title tag and length, meta description and length, H1,
   heading outline, word count, internal links out, images without alt text,
   canonical tag, obvious thin or duplicate content.
4. Search each target keyword and note who ranks in the top 5 and whether {{site}} appears.
5. Check robots.txt and the sitemap.

OUTPUT
1. Health score out of 100 with a one line reason
2. Issues table: Issue | Pages affected | Severity (high/med/low) | Fix
3. Keyword view: Keyword | Our best page | Who ranks top 3 | Gap
4. Top 10 fixes ordered by impact divided by effort
5. Content ideas: 5 pages we should create, each tied to a keyword gap
```

## Why it works

- Sampling by page type finds template level problems that fix many pages at once.
- Impact over effort ordering gives a to do list, not a lecture.
