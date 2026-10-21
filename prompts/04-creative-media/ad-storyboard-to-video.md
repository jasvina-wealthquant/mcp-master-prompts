# Ad storyboard to video

> Goes from a product brief to a shot by shot storyboard, then to priced, approved video clips.

**MCPs:** web scrape (product page), creative generation for image and video (Artlist, Higgsfield, Replicate), optional music and voice
**Best for:** short social ads, 15 to 30 seconds
**Typical cost:** varies; always priced before generation

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{product}}` | URL or description | product page URL |
| `{{length}}` | Duration and format | "20 seconds, 9:16 vertical" |
| `{{budget}}` | Credit ceiling | "8,000 credits" |

## The prompt

```text
1. Fetch {{product}}. Pull the product name, the 3 main benefits, the audience, and
   any proof points.
2. Write a storyboard for {{length}}: 4 to 6 shots. For each shot give the visual,
   camera move, on screen text, voice over line, and duration. Hook in the first 2 seconds.
3. Write the voice over script and time it at about 2.5 words per second.
4. Recommend a model for each shot and price the full job (keyframes, clips, voice,
   music) with the tool's cost function. Compare to {{budget}}.
5. Stop and show me the storyboard and the price.
6. After approval: generate keyframe images first, show them, and only then animate
   the approved frames into clips.

OUTPUT
- Storyboard table
- Script with timings
- Cost breakdown and balance after
- Links to final assets
```

## Why it works

- Keyframes first means you approve the look before paying for motion.
- Timing the script prevents the classic voice over that runs long.
