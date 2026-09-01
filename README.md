# moo-pages

Static page hosting for sharing MOO landing pages, mockups, and one-off reports — **pages.moo.kitchen**.

## Model

- **Individual pages are public** — anyone with the direct link (`pages.moo.kitchen/{slug}/`) can view them. No login.
- **The root listing (`pages.moo.kitchen/`) is private** — gated by Cloudflare Access (Google sign-in), restricted to Pratik. This keeps the directory of everything from being publicly browsable while still letting any single page be shared freely.
- **Nothing is indexed by search engines** — every page ships `X-Robots-Tag: noindex, nofollow` via `_headers`.

Same shape as `recurrco/recurr-pages` (pages.recurr.co), minus its client-side password gate — the root here uses real Cloudflare Access instead.

## Adding a new page

1. `mkdir {slug}/` at the repo root, put a self-contained `index.html` inside (inline styles/scripts or CDN links — no build step).
2. Add a line to the root `index.html`'s page list (see the comment in that file for the exact `<li>` format).
3. Commit and push to `main` — Cloudflare Pages auto-deploys.
4. Share `https://pages.moo.kitchen/{slug}/` directly — no auth needed to view it.

## Infra

- Cloudflare Pages, auto-deploy from `main`.
- Custom domain: `pages.moo.kitchen`.
- Cloudflare Access application scoped to the exact root path (`/`), Google as identity provider.
