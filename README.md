# The Whole Woman Score — update channel

This public repo is the **live-update channel** for The Whole Woman Score
Android app. It contains only the app's public web bundle — the same build
that is already published on the web — so nothing private lives here. The
app source and Play packaging live in the private repo
`ToooMuchMoxie/whole-woman-score-app`.

## How it works

- Installed apps fetch `manifest.json` from this repo's `main` branch:
  `{ "version": "1.0.0", "bundleUrl": "<zip url>", "sha256": "<hex>" }`
- If the version is newer than the bundle an app is running, the app
  downloads the zip from `bundles/`, verifies its SHA-256 against the
  manifest, extracts `index.html`, and runs it on the next launch.
- Any failure (offline, bad hash, corrupt zip) is silent — the app keeps
  running its current bundle.

## Publishing a new bundle

Do not edit `manifest.json` or `bundles/` by hand. Instead:

1. Put the new, version-stamped app HTML at `bundle-src/index.html`
   (stamp it with `scripts/inject-updater.js` from the app repo).
2. Set `VERSION` to the new version (e.g. `1.1.0`).
3. Push to `main`. The `Publish web bundle` workflow zips the bundle,
   rewrites `manifest.json`, and commits both back here.

Full instructions: `UPDATE-GUIDE.md` in the app repo.
