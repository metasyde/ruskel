# @ruskel/ui

The component layer — shadcn primitives moulded to the house style.
Contains no raw colours; every value comes from `@ruskel/tokens`.

```bash
npm install @ruskel/tokens @ruskel/ui
```

```css
@import "@ruskel/tokens";
@import "@ruskel/ui";
```

## The seven decisions

Applied together these remove essentially all of the "default shadcn app"
tell without rewriting a single primitive.

1. **Radius 4px**, not 8px — the single largest visual tell
2. **No shadows** — depth is a hairline in editorial, emission in luminous
3. **Density one step tighter** — controls at 26/32/40px
4. **Mono tabular numerals** wherever data appears
5. **Focus is ink**, 2px, offset 2px — no band colour touches chrome
6. **Motion is colour only**, 120ms — no transforms
7. **Uppercase mono labels**, 0.09em tracking

## Classes

`rsk-btn` `rsk-input` `rsk-check` `rsk-switch` `rsk-chip` `rsk-card` `rsk-tabs`
`rsk-table` `rsk-alert` `rsk-dialog` `rsk-tooltip` `rsk-progress` `rsk-meter`
`rsk-skeleton` `rsk-status`

Paste them into the corresponding shadcn component's `cva` variants, or apply
them directly. The token contract does most of the work on its own.

## The one sanctioned pill

A Switch is fully rounded and has to be — the affordance is a knob travelling
along a track, and a square switch reads as two checkboxes. It and the status
dot are the only round things in the system.

## Instrument furniture

Three primitives sharing one mechanic — a 1px hairline, a small radius,
contained content. No shadows, no gradients, no images.

- **`.rsk-hatch`** — a section break with more weight than a rule and less
  than a heading. A 315° diagonal hatch derived from `--rsk-rule-strong`, so
  it flips with the exposure. The angle leans the same way as the dispersion
  mark's refracted rays.
- **`.rsk-tile`** — a framed glyph, 30px. Add `.rsk-tile--band` with a
  `data-band` to tint the frame and colour the glyph.
- **`.rsk-plate`** — a demonstration frame: an outer panel divided into
  cells, each with an optional verdict foot. Use it to show two states side
  by side so the reader compares rather than takes your word for it. Cells
  stack below 640px; the divider follows, because it is drawn per-cell
  rather than on the container.

The verdict follows the status rule — form carries it, and only the
reserved alarm hue appears: a filled 520nm dot for yes, a 700nm ring for no.
