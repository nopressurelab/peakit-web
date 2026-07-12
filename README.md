# peakit-web

Marketing site for [peakit.io](https://peakit.io) — the alpine planning app.

Static, one-page: hero + feature grid + data-source attribution + privacy
policy at `/privacy`. Deployed to GitHub Pages via GitHub Actions on every
push to `main`, served at the custom domain [peakit.io](https://peakit.io).

## Layout

    /
    ├── index.html                        Landing page
    ├── privacy.html                      Privacy policy
    ├── logo.svg                          Inline SVG logo (also used for favicon)
    ├── logo.png                          Same, rasterised (drop in when ready)
    ├── apple-touch-icon.png              iOS home-screen icon (drop in)
    ├── CNAME                             Custom domain for GitHub Pages
    ├── .nojekyll                         Serve files as-is (skip Jekyll)
    ├── .well-known/
    │   └── apple-app-site-association    Universal Links config
    └── .github/workflows/pages-deploy.yml

## Local preview

Just open `index.html` in a browser, or run a static server:

```
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy

The GitHub Action at `.github/workflows/pages-deploy.yml` builds and deploys
to GitHub Pages on every push to `main`. No secrets are required — it uses
the repo's built-in `GITHUB_TOKEN`.

One-time setup in the repo settings:

1. **Settings → Pages → Build and deployment → Source:** *GitHub Actions*.
2. **Settings → Pages → Custom domain:** `peakit.io` (the `CNAME` file
   already pins this; the setting enables the "Enforce HTTPS" checkbox once
   the certificate is issued).
3. Point DNS at GitHub Pages:
   - Apex `peakit.io` → four `A` records: `185.199.108.153`,
     `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
     (and/or the matching `AAAA` records for IPv6).
   - `www.peakit.io` → `CNAME` to `nopressurelab.github.io`.

## Universal Links

`.well-known/apple-app-site-association` currently references
`TEAMID.live.nopressurelab.peakit`. Replace `TEAMID` with the 10-character
Apple Developer team ID from App Store Connect before shipping.

## Assets still to add

- `logo.png` — 1024×256 raster of `logo.svg` for platforms that don't render inline SVG.
- `apple-touch-icon.png` — 180×180 png (peakit app icon).

The site works without them (SVG favicon is the default) but is more polished
when they exist.
