# Budgeted image batch

> Generates a consistent set of images in one batch, inside a credit ceiling.

**MCPs:** creative generation with batch and cost tools (Artlist, Higgsfield)
**Best for:** carousels, blog headers, product shot sets
**Typical cost:** priced before the run

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{set}}` | What the images are | "8 slide Instagram carousel on how SIPs compound" |
| `{{style}}` | Style or style kit name | "our brand kit" |
| `{{ceiling}}` | Credit limit | "1,500 credits" |

## The prompt

```text
1. Write one prompt per image for {{set}}. Keep subject, palette, lighting, framing and
   text placement consistent. Use {{style}}.
2. Check my balance. Price the whole batch with the cost tool.
3. Show the prompts, the price, and the balance after. If over {{ceiling}}, propose a
   cheaper model or fewer images.
4. After approval, generate image 1 alone. Show it.
5. After approval of image 1, submit the rest as one batch.
6. Review each result for text errors, off brand colors and broken anatomy. List any
   that need a redo, with a fixed prompt, and price the redo before running it.

OUTPUT
- Prompt list
- Cost and balance before and after
- Final image links in order
- Redo list (if any)
```

## Why it works

- One batch call is faster and easier to track than many single calls.
- Reviewing for text and anatomy errors catches the usual AI image failures.
