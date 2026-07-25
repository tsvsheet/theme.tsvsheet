# theme.tsvsheet

Shared **Hugo Module** holding the tsvsheet visual system — the chrome (`layouts/_default/baseof.html`, `layouts/partials/site-{bar,foot}.html`), palette + typography (`assets/css/{main,fonts}.css`), and brand assets (`static/`). It is consumed **by version** by [www.tsvsheet.com](https://github.com/tsvsheet/www.tsvsheet.com) and [docs.tsvsheet.examples](https://github.com/tsvsheet/docs.tsvsheet.examples); it is the single source of truth for that look.

## Rules

- **This is the only home for the shared chrome.** Never copy these templates or CSS into a consuming repo — a consumer imports the module and overrides a single file only when it must diverge. Duplication here is drift.
- **Public means world-class.** This repo is public; every file must be clean, uniform, and correct. Nothing half-built lands here.
- **Nav is parameterized, never hardcoded per site.** Header/footer links resolve through the `mainSite` param (empty = self-relative for tsvsheet.com, `https://tsvsheet.com` for docs sites). Do not fork the partials per consumer.
- **A change is a release.** Edit the chrome here, tag a new `vMAJOR.MINOR.PATCH`, then bump each consumer's `require` line. Breaking visual changes are still minor per owner policy.
- **Verify against real consumers.** The test for a change is that both consuming sites build (`hugo --minify`) and render correctly — there is no synthetic gate that substitutes for that.
