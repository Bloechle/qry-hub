# $ qry.hub

Single-page launcher for my mini webapps — built with [qry.js](https://github.com/Bloechle/qry), zero other dependencies.

## Structure

```
qry-hub/
├── index.html          ← the hub (cards + live filter)
└── apps/
    └── <name>/index.html
```

## Adding an app

Declare it in the `APPS` array at the top of the script in `index.html`:

```js
{ icon: '🧪', name: 'playground', desc: 'JS sandbox with qry.js', url: 'apps/playground/index.html' }
```

The card, search indexing and layout are generated automatically.

## Run

Open `index.html` in a browser — fully static, no build, no server. qry.js is loaded from the CDN:

```
https://cdn.jsdelivr.net/gh/Bloechle/qry@latest/qry.js
```

## License

MIT
