# winjogames.com

Static landing site for Winjo Games. Plain HTML + inline CSS — no build step,
no framework, no JavaScript required to render.

## Pages

| File                    | Path                  |
|-------------------------|-----------------------|
| `index.html`            | `/`                   |
| `games.html`            | `/games.html`         |
| `company.html`          | `/company.html`       |
| `careers.html`          | `/careers.html`       |
| `contact.html`          | `/contact.html`       |
| `terms.html`            | `/terms.html`         |
| `privacy.html`          | `/privacy.html`       |
| `cookies.html`          | `/cookies.html`       |
| `responsible-play.html` | `/responsible-play.html` |
| `404.html`              | unknown paths         |

## Assets

- `img/` — page imagery (hero, key art, game icons)
- `logo.png` — wordmark logo used in the header and footer
- `favicon.ico` — multi-size (16/32/48) for the default `/favicon.ico` request
- `icons/` — PNG favicons (16/32/48/192/512) and `apple-touch-icon.png` (180)
- `og.png` — 1200×630 social share card, referenced by `og:image`
- `site.webmanifest` — PWA manifest pointing at the 192/512 icons

## Origin

Converted from a Claude Design canvas export (`*.dc.html`). The originals
depended on a client-side runtime that loaded React from a CDN and rendered the
page in the browser. That was replaced with the equivalent plain HTML:

- `<helmet>` contents moved into `<head>`; `<x-dc>` wrapper removed
- `support.js` and `image-slot.js` dropped
- `style-hover` / `style-focus` attributes compiled to real CSS (`.wg-p*` rules)
- `<image-slot>` replaced with a plain `<img>`
- internal `*.dc.html` links rewritten to `*.html`
- `<title>`, `<link rel="canonical">` and per-page `og:url` added

Design, copy and layout are unchanged.

## Local preview

    python3 -m http.server 8000

Then open <http://localhost:8000>.

## Deployment

GitHub Pages, serving the repository root of the `main` branch. Any push to
`main` redeploys. `CNAME` pins the custom domain; `.nojekyll` disables Jekyll
preprocessing.

### GoDaddy DNS

Set these four `A` records on the apex (`@`) of `winjogames.com`:

| Type | Name | Value           |
|------|------|-----------------|
| A    | @    | 185.199.108.153 |
| A    | @    | 185.199.109.153 |
| A    | @    | 185.199.110.153 |
| A    | @    | 185.199.111.153 |

**Leave the `www` record alone.** GoDaddy creates a `CNAME www → @` by default and
will not let you delete it while domain forwarding exists. You do not need to:
pointing `www` at the apex resolves to the same four GitHub IPs, and GitHub Pages
routes on the `Host` header, so it serves `www` and redirects it to the apex. A
`CNAME www → yuritselicov-king.github.io` is equivalent, not required.

Delete GoDaddy's default parked-page `A` record if one remains. If the site ever
flaps between GitHub and a GoDaddy parking page, remove the forwarding under
Domain Settings → Forwarding.

Then enable Pages: repo Settings → Pages → Source *Deploy from a branch*, branch
`main`, folder `/ (root)`. The committed `CNAME` file fills in the custom domain.
Once the certificate provisions, tick **Enforce HTTPS** — it covers apex and www.
