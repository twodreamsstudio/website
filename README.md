# Two Dreams Labs — Website

Marketing site for **Two Dreams Labs LLC** (DreamCI · Mirage · Bennu).

The deployed site is **`index.html`** (currently **v4** — light/professional palette, responsive)
plus **`support.js`** (the dc-runtime). No build step. `support.js` loads React 18 from the
unpkg CDN at runtime, finds the `<x-dc>` template in the page and mounts it.

## Structure

```
index.html            Deployed site (v4) — loads ./support.js
support.js            dc-runtime (renders the <x-dc> template, pulls React from unpkg)
versions/
  v2.html             Dark / tech palette (violet + cyan)   — loads ../support.js
  v3.html             Professional light layout (alt)        — loads ../support.js
  v4.html             Light professional palette (= index.html)
src/                  Editable source (Design Component files), each loads ./support.js
  Two Dreams Labs v2.dc.html
  Two Dreams Labs v3.dc.html
  Two Dreams Labs v4.dc.html
  support.js
```

`index.html` and `src/index` need their sibling `support.js`; the `versions/*.html` reference
`../support.js` (the copy at the repo root). Open any of them in a browser — they render the
full site as long as `support.js` is reachable and the page has internet access (for the CDN React).

> Note: an earlier version shipped a single pre-bundled `index.html` (~256 KiB). That file got
> truncated at the 256 KiB transfer limit during import and failed with **"Error: missing bundle
> data"**. The current source-based setup avoids any bundle and renders reliably.

## Deploy on Cloudflare Pages

### From this repo (recommended)
1. Cloudflare → Workers & Pages → **Create** → **Pages** → Connect to Git → select `website`.
2. Build settings:
   - Framework preset: **None**
   - Build command: *(leave empty)*
   - Build output directory: **/** (root)
   - Production branch: **main**
3. Save and Deploy. Cloudflare serves `index.html` (which loads `support.js`) at the root.

### Direct upload (no repo)
Cloudflare → Workers & Pages → **Create** → **Pages** → **Upload assets** → drag **both**
`index.html` **and** `support.js` (same folder).

## Push to GitHub (twodreamsstudio/website)

```sh
git add .
git commit -m "Two Dreams Labs website"
git push
```

Remote `origin` → `https://github.com/twodreamsstudio/website.git`.

## Switching the deployed version
Copy the chosen version's source over `index.html` (keep the `./support.js` reference) and push:

```sh
cp "src/Two Dreams Labs v2.dc.html" index.html   # e.g. publish v2 (dark)
git commit -am "deploy: v2" && git push
```
