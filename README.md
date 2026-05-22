# Tuner

A PWA chromatic-style tuner for guitar, bass, and ukulele. Standard and common alternate tunings ship built in; custom tunings can be added in the UI. Pitch detection runs entirely in the browser via the Web Audio API (YIN algorithm).

## Files

- `index.html` — the whole app (CSS and JS are inlined so the site is one HTTP request)
- `manifest.webmanifest` — PWA manifest
- `sw.js` — service worker (network-first for HTML, cache-first for everything else)
- `icon.svg`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` — app icons
- `.nojekyll` — tells GitHub Pages not to run Jekyll on the repo

## Local development

```sh
python3 -m http.server 8080
```

Then open <http://localhost:8080>. `localhost` is a secure context, so the mic API works without HTTPS.

## Notes on caching

The service worker uses a versioned cache (`tuner-vN` in `sw.js`). Bump the version whenever you ship changes so existing visitors get the new code on their next reload. The HTML is fetched network-first, so most code edits show up without a version bump anyway.
