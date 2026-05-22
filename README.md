# Tuner

A PWA chromatic-style tuner for guitar, bass, and ukulele. Standard and common alternate tunings ship built in; custom tunings can be added in the UI. Pitch detection runs entirely in the browser via the Web Audio API (YIN algorithm).

## Files

- `index.html` — the whole app (CSS and JS are inlined so the site is one HTTP request)
- `manifest.webmanifest` — PWA manifest
- `sw.js` — service worker (network-first for HTML, cache-first for everything else)
- `icon.svg` — app icon
- `.nojekyll` — tells GitHub Pages not to run Jekyll on the repo

## Local development

```sh
python3 -m http.server 8080
```

Then open <http://localhost:8080>. `localhost` is a secure context, so the mic API works without HTTPS.

## Deploy to GitHub Pages — branch method (recommended)

1. Create a new repo on GitHub and push this directory to it:
   ```sh
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin git@github.com:<user>/<repo>.git
   git push -u origin main
   ```
2. In the repo on GitHub → **Settings → Pages**:
   - Source: **Deploy from a branch**
   - Branch: **main** / **root**
3. Wait ~30 s for the first publish. The site URL is `https://<user>.github.io/<repo>/`.

GitHub Pages serves over HTTPS, which is required for the mic API.

## Deploy to GitHub Pages — Actions workflow (optional)

A workflow is included at `.github/workflows/pages.yml`. To use it instead of branch deploy:

1. Push the repo as above.
2. In **Settings → Pages**, change Source to **GitHub Actions**.
3. Pushes to `main` will trigger the workflow and publish the site.

Delete `.github/workflows/pages.yml` if you're sticking with the branch method.

## Notes on caching

The service worker uses a versioned cache (`tuner-vN` in `sw.js`). Bump the version whenever you ship changes so existing visitors get the new code on their next reload. The HTML is fetched network-first, so most code edits show up without a version bump anyway.
