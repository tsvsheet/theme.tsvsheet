# theme.tsvsheet

The shared **tsvsheet visual system** as a [Hugo Module](https://gohugo.io/hugo-modules/) — the chrome (base shell, header/footer), palette, and fonts that give [tsvsheet.com](https://tsvsheet.com) its look. Sites consume it **by version** so the look stays uniform across the main site and its docs sites with no duplicated templates.

## What's inside

- [`layouts/_default/baseof.html`](layouts/_default/baseof.html) — the HTML shell: `<head>` (meta, Open Graph, fonts preload, concatenated `fonts.css` + `main.css`), the `main` block, and the theme-toggle + copy-command scripts.
- [`layouts/partials/site-bar.html`](layouts/partials/site-bar.html), [`layouts/partials/site-foot.html`](layouts/partials/site-foot.html) — the header and footer. Nav targets are built from the `mainSite` param (below).
- [`assets/css/main.css`](assets/css/main.css), [`assets/css/fonts.css`](assets/css/fonts.css) — the ledger-paper / pine palette (light + dark), typography, and the `@font-face` declarations for IBM Plex.
- [`static/`](static/) — IBM Plex Mono/Sans `woff2`, `favicon.svg`/`favicon.ico`/`apple-touch-icon.png`, and `og.png`.

## Using it in a site

Add the module import to the consuming site's Hugo config and pin it in `go.mod`:

```json
{
  "module": {
    "imports": [{ "path": "github.com/tsvsheet/theme.tsvsheet" }]
  }
}
```

```
require github.com/tsvsheet/theme.tsvsheet v0.1.0
```

Then `hugo mod get github.com/tsvsheet/theme.tsvsheet@v0.1.0` to lock it. Hugo overlays the module's files **under** the site's own, so a site overrides any single file by placing its own at the same path — a docs site keeps its content layouts while inheriting this chrome.

### The `mainSite` param

The header and footer nav point at the main site. On tsvsheet.com itself leave it empty (self-relative); on a docs site set it so the chrome links **back** to the main site:

```json
{ "params": { "mainSite": "https://tsvsheet.com" } }
```

| `mainSite` | Nav link resolves to |
| --- | --- |
| `""` (default) | `/playground/` — self-relative, for tsvsheet.com |
| `"https://tsvsheet.com"` | `https://tsvsheet.com/playground/` — for docs sites |

## Consumers

- [www.tsvsheet.com](https://github.com/tsvsheet/www.tsvsheet.com) — the main site.
- [docs.tsvsheet.examples](https://github.com/tsvsheet/docs.tsvsheet.examples) — the worked-examples site.

## Versioning

Tagged releases (`vMAJOR.MINOR.PATCH`). A change to the chrome is adopted by each consumer with a single `require`-line bump, keeping the look uniform and the adoption explicit.

## License

[MIT](LICENSE).
