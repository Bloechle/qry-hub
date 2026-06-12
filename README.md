# $ qry.hub

Single-page launcher for my mini webapps — built with [qry.js](https://github.com/Bloechle/qry-js) and themed by the qry stack (`qry-ui.css` + `qry-hub-theme.css`); individual apps may pull in Shoelace widgets or their own libraries on top.

**Live → [bloechle.github.io/qry-hub](https://bloechle.github.io/qry-hub/)**

## Structure

```
qry-hub/
├── index.html          ← the hub (categorized cards + live filter)
├── favicon.svg
├── qry-hub-theme.css   ← qry-ui token override + hub signature (see Theming)
└── apps/
    ├── edu/            algolive · trigolive · namecards · examtimer
    ├── game/           snake · dodgerun · singularity
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

Two regimes — when adding a new app, prefer the **qry stack** one:

| Regime | Pages | How it works |
|---|---|---|
| **qry stack** (default) | `index.html` · algolive · trigolive · namecards · adaptlive · consentform · pdfsign · paintpad · typstlive | Link `qry-ui.css` (CDN) + `qry-hub-theme.css` (`../../../qry-hub-theme.css` from an app, three levels deep), which re-points the qry-ui tokens at the hub palette and adds the `body.hub-app` dotted background + `$ app.name` terminal header. Pages that use Shoelace widgets load it first — order: Shoelace `light.css` + autoloader → qry-ui.css → qry-hub-theme.css; widget-less pages (the hub itself, trigolive) skip Shoelace entirely. App styles go in the page's own `<style>`, marked `/* ─── App: <name> (shared theme: …) ─── */`, using `--qry-*` tokens only. `qry-hub-theme.css` also ships two shared hub components — the `.note` caption and the compact `.metric` strip (`#metrics` grid) used by algolive, trigolive and adaptlive. |
| **Own identity** | examtimer · dodgerun · snake · singularity | Fully self-styled; no shared theme. |

The qry-stack pages are light-only by design: they load only Shoelace's
`light.css` (when they need Shoelace at all) and never call `theme.init()`.
To change the hub look, edit `qry-hub-theme.css` — every qry-stack page picks
it up on reload; there is nothing to re-paste.

## Run

Open `index.html` in a browser — fully static, no build, no server. qry.js is loaded from the CDN:

```
https://cdn.jsdelivr.net/gh/Bloechle/qry-js@1.1.0/qry.js
```

## License

MIT
