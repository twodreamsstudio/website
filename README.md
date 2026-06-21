# Two Dreams Labs — Website

Marketing site for **Two Dreams Labs LLC** (DreamCI · Mirage · Bennu).

The deployed site is the single self-contained **`index.html`** (currently **v4** — light/professional palette, responsive). No build step, no dependencies.

## Structure

```
index.html            Deployed site (v4) — self-contained, responsive
versions/
  v2.html             Dark / tech palette (violet + cyan)
  v3.html             Professional light layout (alt structure)
  v4.html             Light professional palette on v2 structure (= index.html)
src/                  Editable source (Design Component files)
  Two Dreams Labs v2.dc.html
  Two Dreams Labs v3.dc.html
  Two Dreams Labs v4.dc.html
  support.js
```

Open any `versions/*.html` directly in a browser — each is fully standalone.

## Deploy on Cloudflare Pages

### From this repo (recommended)
1. Cloudflare → Workers & Pages → **Create** → **Pages** → Connect to Git → select `website`.
2. Build settings:
   - Framework preset: **None**
   - Build command: *(leave empty)*
   - Build output directory: **/** (root)
3. Save and Deploy. Cloudflare serves `index.html` at the root.

### Direct upload (no repo)
Cloudflare → Workers & Pages → **Create** → **Pages** → **Upload assets** → drag `index.html`.

## Push to GitHub (twodreamsstudio/website)

Run from a **clean folder** containing these files (not inside another git repo):

```sh
git init
git add .
git commit -m "Two Dreams Labs website — all versions, deploy v4"
git branch -M main
git remote add origin https://github.com/twodreamsstudio/website.git
git push -u origin main
```

The repo `twodreamsstudio/website` already exists. If `git remote add` says origin
exists, run `git remote set-url origin https://github.com/twodreamsstudio/website.git`.

## Switching the deployed version
To deploy a different version, replace `index.html` with the chosen `versions/*.html`
and push again (Cloudflare auto-redeploys on push).
