# animepedia-content

Public content bundle repo for the [AnimePedia](https://github.com/jdevsappstudio-github/AnimePediaApp)
Android app. Holds the versioned `content.json` catalog bundle (animes, characters, quotes, sounds
metadata), served to the app via **jsDelivr** CDN. Audio files live on Cloudflare R2, not here —
this repo is JSON only.

## Why this repo is public

jsDelivr only serves public GitHub repos. The main app repo stays private; this repo exists solely
to host the catalog bundle. This is a deliberate, low-cost interim solution — see
`docs/DECISIONS.md` in the app repo ("content-bundle-host" decision) for the full reasoning and the
planned migration to a dedicated content API later.

## Versioning

- Each published bundle is a commit to `content.json` on `main`.
- The app fetches a **commit-SHA-pinned** jsDelivr URL (immutable, no cache-purge needed):
  `https://cdn.jsdelivr.net/gh/jdevsappstudio-github/animepedia-content@<commit-sha>/content.json`
- Firebase Remote Config holds the current `content_bundle_url` (+ `content_version`) pointer; bumping
  it to a new commit SHA is how a release ships.
- `content_version` inside the JSON itself is a monotonically increasing integer, independent of the
  git SHA, used for the app's local Room cache comparison.

## Schema

See `BUILD-SPEC.md` §2.3 in the app repo for the authoritative `content.json` shape.
