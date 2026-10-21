# Music and sound brief

> Finds licensed tracks and sound effects for a video, or writes a brief for generated music.

**MCPs:** music and sound catalog search plus music generation (Artlist)
**Best for:** scoring reels, ads and explainers
**Typical cost:** catalog search is usually free; generation is priced first

## Inputs

| Placeholder | What to put there | Example |
| --- | --- | --- |
| `{{video}}` | Description, length, cut points | "30s explainer, cuts at 0:08, 0:17, 0:24" |
| `{{mood}}` | Feel | "hopeful, light, no vocals" |

## The prompt

```text
1. Describe the music need for {{video}}: mood ({{mood}}), tempo range, instruments,
   vocals or none, energy curve that matches the cut points.
2. Search the music catalog with 3 different queries. Shortlist 5 tracks with title,
   artist, length, BPM and why each fits.
3. For the top 2, look up similar tracks and shorter versions or cut downs.
4. Search sound effects for each cut point (whoosh, click, rise) and shortlist 2 each.
5. Only if nothing fits, write a generation prompt for custom music, price it, and ask.

OUTPUT
- Music brief
- Track shortlist table
- Sound effects per cut point
- Recommendation with reasoning
```

## Why it works

- Licensed catalog first is cheaper and often better than generation.
- Matching energy to cut points makes the edit feel deliberate.
