# @ruskel/registry

The shadcn custom registry manifest.

## Build

```bash
npm run registry:build     # shadcn build packages/registry/registry.json --output packages/registry/dist
```

Note the command is `shadcn build`, not `shadcn registry:build` — the latter
does not exist.

## Install (once the packages are published)

```bash
npx shadcn@latest add https://<host>/r/ruskel.json          # tokens + components
npx shadcn@latest add https://<host>/r/ruskel-tokens.json   # tokens only
```

## Two things learned the hard way

**Items resolve through npm, not by copying files.** An earlier version
shipped the stylesheets as `registry:file` entries with a `target`, plus a
`css` block containing a relative `@import`. It builds cleanly and installs
*broken*: `target` is resolved from the project root, but the `@import` is
written verbatim into the consumer's stylesheet, which sits at an arbitrary
depth. `app/globals.css` receiving `@import "./styles/ruskel-tokens.css"`
looks for `app/styles/…`, which does not exist. No literal relative path is
correct for every project layout, so the CSS comes from the npm package and
resolution is the bundler's problem.

**Bare `registryDependencies` point at shadcn's registry, not this one.**
`"registryDependencies": ["ruskel-tokens"]` makes the CLI fetch
`ui.shadcn.com/r/styles/…/ruskel-tokens.json` and fail. Cross-referencing
items in a custom registry needs a full URL or a configured namespace, so
instead `@ruskel/ui` imports `@ruskel/tokens` itself and each item stands
alone.

## Verified

- Manifest validates against the current `registry.json` / `registry-item.json`
  schemas (shadcn CLI 4.18.0)
- `shadcn build` produces both items with the expected `dependencies` and
  `css` blocks
- `shadcn add` from a built item was exercised against a scratch project: the
  CLI creates files and injects the `@import` into the project stylesheet
  correctly

## Not yet verified

End-to-end install of the current manifest, because it depends on
`@ruskel/tokens` and `@ruskel/ui` existing on npm. Until they are published,
`shadcn add` fails at the `npm install` step with a 404. Re-run the scratch
install after the first publish.
