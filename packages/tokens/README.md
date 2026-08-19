# @ruskel/tokens

The two-exposure token layer.

```bash
npm install @ruskel/tokens
```

```css
@import "@ruskel/tokens";
```

Then set an exposure on any subtree:

```html
<body data-exposure="editorial">   <!-- ink on paper — the author voice -->
<div  data-exposure="luminous">    <!-- paper on ink — the product voice -->
```

Nothing else is required. The file maps itself onto the shadcn variable
contract (`--background`, `--primary`, `--ring`, `--chart-1…8`, `--sidebar-*`),
so shadcn components inherit the system without any component edits.

## Layers

| | |
|---|---|
| `--rsk-n-01 … --rsk-n-12` | neutral ramp, warm, shared by both exposures |
| `--rsk-mark-*` | vivid fills, bars, dots, glows, borders. Seen, not read. |
| `--rsk-text-*` | coloured type. Read, so constrained to AA. |
| `--rsk-deep-*` | second depth per band, chart overflow only |
| `--rsk-ground` `--rsk-surface` `--rsk-rule` `--rsk-text` | chrome |

Never use a `text-*` value as a fill or a `mark-*` value as body type. That
swap is the single most common way to make the system look wrong.

## Extending it

Colours are the output of a constraint solve, not hand-picked. Add a hue by
adding an angle and re-running the solver:

```bash
python3 tools/solve.py ring --exposure editorial
python3 tools/solve.py verify
```
