# Brand style kit builder

> Researches a brand's existing look and builds a reusable style kit in a generation tool.

**MCPs:** web scrape (Firecrawl branding extraction), creative generation with style kits (Artlist, Higgsfield)
**Best for:** making every future generated image or video look on brand
**Typical cost:** 3 to 5 web calls, style kit creation is usually free

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{brand}}` | Name and site | "WealthQuant, wealthquant.example" |
| `{{mood}}` | Feel in a few words | "calm, trustworthy, muted green" |

## The prompt

```text
Build a style kit for {{brand}}.

1. Fetch the brand's site and social profiles. Extract colors (hex), fonts, logo usage,
   photography style, illustration style, and recurring layout patterns.
2. Summarize the visual identity in 5 rules a designer could follow.
3. Show me the palette, the rules, and the mood ({{mood}}). Wait for my approval.
4. After approval, create a style kit in the generation tool with:
   - the palette
   - written style guidelines (subjects, lighting, composition, what to avoid)
   - 2 to 4 reference images, from the brand's own assets if I provide them
5. Generate one test image with the kit (show the cost first) so we can check it.

OUTPUT
- Palette with hex codes and where each color is used
- Five visual rules
- Do and do not list
- The style kit name, ready to reuse
```

## Why it works

- Extracting from real assets keeps the kit faithful to the brand.
- One priced test image confirms the kit before any batch spend.
