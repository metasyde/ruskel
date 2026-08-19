# Ruskel

**One spectrum, two exposures.** A design system for interfaces that are
either *read* or *operated* — and which should look like the same author
made both.

```
registry.json        the shadcn registry manifest — this file is the registry
packages/tokens      the two-exposure token layer
packages/ui          shadcn primitives, moulded
docs/                the specimen page and the written system
tools/solve.py       the colour solver — the palette is its output
```

---

## The idea

An exposure is not a light/dark theme. A theme recolours a fixed design. An
exposure changes what light is *doing*.

| | Editorial | Luminous |
|---|---|---|
| Ground | paper | ink |
| Voice | author | product |
| Colour behaves as | pigment | light |
| For | site, writing, case studies, proposals | apps, dashboards, demos, client UI |

Editorial **marks** with a band — a rule, a chip, a word. Luminous **emits**
it, with falloff around the source. Ink and paper swap; the spectrum
re-solves for the new ground.

Components never know which exposure they are in. The emission tokens exist
in both and resolve to nothing on paper, so a component writes
`box-shadow: var(--rsk-glow-sm)` unconditionally and simply does not glow in
editorial. A component that needs a `[data-exposure]` override is a bug in
the tokens.

## Use it

Via the shadcn CLI — the repo *is* the registry, so there is nothing hosted
and no build step:

```bash
npx shadcn@latest add metasyde/ruskel/ruskel          # tokens + components
npx shadcn@latest add metasyde/ruskel/ruskel-tokens   # tokens only
```

Or plainly, if you are not using shadcn:

```bash
npm install @ruskel/tokens @ruskel/ui
```

```css
@import "@ruskel/tokens";
@import "@ruskel/ui";
```

```html
<body data-exposure="editorial">
  <section data-exposure="luminous"> <!-- a product plate inside an essay -->
</body>
```

Shadcn components inherit everything through the variable contract. No
component source is edited.

## The rules

1. **A band never appears decoratively.** 590nm is interface, 520nm systems,
   470nm compute, 405nm intelligence. If something is amber it is *about*
   interface. Corollary: chrome carries no band at all — including focus.
2. **Status is not a band.** Health and category are different axes. Status
   carries one hue and otherwise encodes itself in form: hollow = fine,
   ring = watch, filled = critical.
3. **Components don't know their exposure.** Style against token names.
4. **Marks are seen; text is read.** Never swap the two rings.
5. **Mono is metadata, never content.** Labels, figures, timestamps, code.
6. **Numbering must encode order.** Unordered peers get a rule and a label.
7. **Geometry is near-square.** Radii 2/4/6px. No pills except switches and
   status dots.
8. **Spend boldness once per view.** One luminous moment per screen.
9. **Colour is never the only carrier.** The system must survive greyscale.

## The palette is computed, not picked

Every value is the output of a constraint solve, and the solver ships with
the repo. That is what makes the system extendable rather than frozen.

```bash
python3 tools/solve.py ring          # the mark ring per exposure
python3 tools/solve.py separation    # pairwise dE across the six series
python3 tools/solve.py verify        # assert every constraint still holds
```

`verify` re-derives each declared token, checks it against its exposure's
contrast window, confirms no chroma exceeds the sRGB ceiling, and asserts
the categorical series never falls below the separation floor. It exits
non-zero on failure — wire it into CI.

Two constraints worth knowing, because they cost the most to satisfy:

- **The mark ring is per-exposure.** The same hue does not have the same
  impact on both grounds; a shared amber measured 8.8:1 on ink and 1.7:1 on
  paper. Each ground solves its own ring, at maximum chroma within a
  contrast window.
- **Six categorical hues, not eight.** Once the warm arc is reserved for
  warning and critical, eight hues cannot separate — cyan/blue and
  indigo/violet collapse. Six is where every stop sits at its own gamut
  ceiling and nothing collides. Past six, label the series directly.

## Typography

One sans, one mono. Inter at two optical sizes; IBM Plex Mono for metadata and code. No serif at any size. Mono is the highest-risk element in the
system — keeping it strictly to metadata is what stops it becoming a costume.

## Ownership

Maintained by [Metasyde](https://github.com/metasyde), Enric Trillo's
limited company. MIT licensed — free to use in client work, including work
Metasyde does not deliver.

## Status

Design ratified, tokens and component layer complete and verified. Not yet
published to npm; registry manifest needs validating against the current
shadcn schema before it points anywhere.
