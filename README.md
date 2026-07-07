# peakit-web

Marketing site for [peakit.io](https://peakit.io) — the alpine planning app.

Static, one-page: hero + feature grid + data-source attribution + privacy
policy at `/privacy`. Deployed to Netlify via GitHub Actions on every push
to `main`.

## Layout

    /
    ├── index.html                        Landing page
    ├── privacy.html                      Privacy policy
    ├── logo.svg                          Inline SVG logo (also used for favicon)
    ├── logo.png                          Same, rasterised (drop in when ready)
    ├── apple-touch-icon.png              iOS home-screen icon (drop in)
    ├── _headers                          Netlify security/cache headers
    ├── netlify.toml                      Netlify build config
    ├── .well-known/
    │   └── apple-app-site-association    Universal Links config
    └── .github/workflows/netlify-deploy.yml

## Local preview

Just open `index.html` in a browser, or run a static server:

```
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy

The GitHub Action at `.github/workflows/netlify-deploy.yml` deploys
production on push to `main` and a preview URL for each pull request. Two
repo secrets are required:

- `NETLIFY_AUTH_TOKEN`
- `NETLIFY_SITE_ID`

Both are set once in the peakit-web repo settings → Secrets.

## Universal Links

`.well-known/apple-app-site-association` currently references
`TEAMID.live.nopressurelab.peakit`. Replace `TEAMID` with the 10-character
Apple Developer team ID from App Store Connect before shipping.

## Assets still to add

- `logo.png` — 1024×256 raster of `logo.svg` for platforms that don't render inline SVG.
- `apple-touch-icon.png` — 180×180 png (peakit app icon).

The site works without them (SVG favicon is the default) but is more polished
when they exist.
