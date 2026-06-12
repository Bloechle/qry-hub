# $ qry.hub

Single-page launcher for my mini webapps — built with [qry.js](https://github.com/Bloechle/qry). The hub page itself has zero other dependencies; individual apps may pull in the wider qry stack or their own libraries.

**Live → [bloechle.github.io/qry-hub](https://bloechle.github.io/qry-hub/)**

## Structure

```
qry-hub/
├── index.html          ← the hub (categorized cards + live filter)
├── favicon.svg
├── theme.css           ← legacy inline theme (see Theming)
├── qry-hub-theme.css   ← qry-ui token override (see Theming)
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

Three regimes coexist — when adding a new app, prefer the **qry stack** one:

| Regime | Pages | How it works |
|---|---|---|
| **qry stack** (current) | namecards · adaptlive · consentform · pdfsign · paintpad · typstlive | Link `qry-ui.css` (CDN) + `../../../qry-hub-theme.css`, which re-points the qry-ui tokens at the hub palette and adds the `body.hub-app` dotted background + `$ app.name` terminal header. Load order: Shoelace themes → qry-ui.css → qry-hub-theme.css. App styles go in the page's own `<style>`, marked `/* ─── App: <name> (shared theme: …) ─── */`. |
| **Legacy inline** | `index.html` · algolive · trigolive | `theme.css` copied verbatim into the page's `<style>` between the `THEME` / `END THEME` banners, so the page stays a single self-contained file. To change the look: edit `theme.css`, then re-paste the block into each of these three pages. They also load the theme fonts (JetBrains Mono + Inter) via the Google Fonts `<link>` documented at the top of `theme.css`. |
| **Own identity** | examtimer · dodgerun · snake · singularity | Fully self-styled; no shared theme. |

The hub apps that use the qry stack are light-only by design: they load only
Shoelace's `light.css` and never call `theme.init()`.

## Run

Open `index.html` in a browser — fully static, no build, no server. qry.js is loaded from the CDN:

```
https://cdn.jsdelivr.net/gh/Bloechle/qry@1.1.0/qry.js
```

## License

MIT
