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

Assets live in `img/`; the logo is `logo.png` (also used as the favicon).

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

Set these records on `winjogames.com`:

| Type  | Name | Value                          |
|-------|------|--------------------------------|
| A     | @    | 185.199.108.153                |
| A     | @    | 185.199.109.153                |
| A     | @    | 185.199.110.153                |
| A     | @    | 185.199.111.153                |
| CNAME | www  | yuritselicov-king.github.io    |

Delete GoDaddy's default parked-page A record and any conflicting `www` record
first. After DNS propagates, enable **Enforce HTTPS** in the repo's
Settings → Pages.

## Known gaps

- `og:image` points at `https://winjogames.com/og.png`, which does not exist
  yet. Social shares will have no preview image until a 1200×630 asset is added
  at the site root.
- There is no `404.html`, so unknown paths fall through to GitHub's generic
  404 page.
