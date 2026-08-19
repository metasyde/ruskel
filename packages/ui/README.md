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
