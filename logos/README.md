# CAIRN logo assets

Visual identity for the CAIRN methodology: three stones in increasing size along a faint trail line, evoking the cairn metaphor (a stack of stones marking the path for the next traveller).

## Files

| File | Size (px) | Purpose |
|---|---|---|
| `cairn-icon.svg` | 67 × 67 | Icon mark on light backgrounds (favicon, avatar) |
| `cairn-icon-dark.svg` | 67 × 67 | Icon mark on dark backgrounds |
| `cairn-logo-light.svg` | 340 × 80 | Full lockup on light backgrounds |
| `cairn-logo-light-md.svg` | 176 × 40 | Medium lockup on light backgrounds |
| `cairn-logo-light-sm.svg` | 106 × 24 | Small lockup on light backgrounds (inline use) |
| `cairn-logo-dark.svg` | 340 × 80 | Full lockup on dark backgrounds |
| `cairn-logo-dark-md.svg` | 176 × 40 | Medium lockup on dark backgrounds |
| `cairn-logo-dark-sm.svg` | 106 × 24 | Small lockup on dark backgrounds (inline use) |

## How to use them in markdown with theme switching

GitHub, GitLab, and most modern markdown renderers honour the `<picture>` element with `prefers-color-scheme`, so the right logo appears in either theme:

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="logos/cairn-logo-dark.svg">
  <img alt="CAIRN" src="logos/cairn-logo-light.svg" width="340">
</picture>
```

Adjust the file (`-md`, `-sm`, or `cairn-icon`) and the `width` attribute to fit the context.

## Colour palette

| Role | Light theme | Dark theme |
|---|---|---|
| Largest stone | `#7a4d18` | `#f0d4a8` |
| Middle stone | `#c17f3a` | `#e2ab65` |
| Smallest stone | `#e2ab65` | `#c17f3a` |
| Wordmark | `#1e1208` | `#faf6ef` |
| Trail line | `rgba(122,77,24,0.14)` | `rgba(240,212,168,0.18)` |

The progression from earthen brown to warm sand mirrors the trail-marker idea: grounded at the base, lifting toward the sky.

## Attribution

The logos are released under the same [CC BY 4.0](../LICENSE.md) licence as the methodology. If you adapt CAIRN for your team and want to use the mark, please credit Abdullah Siddique.
