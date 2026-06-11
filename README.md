# $ qry.hub

Single-page launcher for my mini webapps — built with [qry.js](https://github.com/Bloechle/qry), zero other dependencies.

**Live → [bloechle.github.io/qry-hub](https://bloechle.github.io/qry-hub/)**

## Structure

```
qry-hub/
├── index.html          ← the hub (categorized cards + live filter)
├── theme.css           ← reference theme (copied inline, never linked)
└── apps/
    ├── edu/            algolive · trigolive · namecards · examtimer
    ├── game/           snake · dodgerun
    ├── lab/            adaptlive · consentform
    └── tools/          pdfsign · typstlive · paintpad
        └── <name>/index.html
```

## Adding an app

Drop it in `apps/<cat>/<name>/`, then declare it in the `APPS` array at the
top of the script in `index.html` with its category:

```js
{ cat: 'tools', icon: '🧪', name: 'playground', desc: 'JS sandbox with qry.js', url: 'apps/tools/playground/index.html' }
```

The card, search indexing (name, description and category) and layout are
generated automatically. Note: app pages sit three levels deep, so relative
references like the favicon use `../../../favicon.svg`.

## Adding a category

Add a line to the `CATS` array (order in the array = order on the page):

```js
{ key: 'music', icon: '🎵', label: 'music' }
```

Sections without apps are skipped automatically.

## Theming

`theme.css` is the canonical source of the shared "terminal" look (tokens,
`$ prompt` header, panel, controls, note, metrics). It is **not linked at
runtime**: each opted-in page copies it verbatim into its `<style>`, between
the `THEME` / `END THEME` markers, so every page stays a single
self-contained file.

- To change the look: edit `theme.css`, then re-paste the block into each
  opted-in page (`index.html` and every app except `examtimer`/`dodgerun`).
- Opted-in pages load the theme fonts (JetBrains Mono + Inter) via the
  Google Fonts `<link>` documented at the top of `theme.css`.
- App-specific styles go *after* the `END THEME` marker and may override
  theme rules (e.g. `#panel { --panel-w: 920px; }`).
- Apps with their own identity (`examtimer`, `dodgerun`) simply don't
  embed the theme.

## Run

Open `index.html` in a browser — fully static, no build, no server. qry.js is loaded from the CDN:

```
https://cdn.jsdelivr.net/gh/Bloechle/qry@1.0.0/qry.js
```

## License

MIT
