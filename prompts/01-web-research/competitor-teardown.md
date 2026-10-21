# Competitor teardown

> A side by side breakdown of competitors' positioning, pricing, features, content and recent moves.

**MCPs:** web search and scrape (Firecrawl), optional browser automation for logged in or script heavy pages
**Best for:** quarterly competitive reviews, pitch prep, positioning work
**Typical cost:** 5 to 8 calls per competitor

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{us}}` | Your product, one line | "an AI driven portfolio management service" |
| `{{competitors}}` | Names or URLs | "Competitor A, Competitor B, Competitor C" |

## The prompt

```text
ROLE: You are a product marketing strategist.
OUR PRODUCT: {{us}}
COMPETITORS: {{competitors}}

For each competitor:
1. Map their site and fetch: home page, pricing, product or features page, about page,
   and their two most recent blog posts or announcements.
2. Search news and social for their last 90 days: launches, funding, hires, complaints.
3. Extract: one line positioning (in their words), target customer, pricing model and
   tiers, top 5 features, proof points (numbers, logos, awards), calls to action,
   tone of voice.

Then compare.

EVIDENCE RULES
- Quote positioning lines word for word with the page URL.
- Prices must come from the pricing page fetched today. Note the date.
- If something is hidden behind a login or a demo request, say so. Do not guess.

OUTPUT
1. Comparison table: Competitor | Positioning | Target | Pricing | Top features | Proof
2. Messaging map: the claims everyone makes vs claims only one makes
3. Recent moves timeline (last 90 days)
4. Where we can win: 3 gaps or weak spots, with evidence
5. Where we are exposed: 3 places they beat us
6. Open questions
```

## Why it works

- Word for word positioning shows how crowded a claim really is.
- The "claims everyone makes" list is where differentiation work starts.
- Separating "win" from "exposed" keeps the review honest.

## Variations

- **Content only:** compare blog topics, posting frequency and social engagement.
- **Monthly watch:** pair with the [pricing tracker](pricing-tracker.md).
