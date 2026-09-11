# Gambit releases

Public **binary** releases for [Gambit](https://github.com/Frenzyz/Gambit).
This repository is not the source tree.

Gambit is a local-first supervised agentic browser (`Gambit.app`, bundle id
`app.gambit.browser`). Product name is Gambit. Copyright Vision Algorithms LLC.

## Download

Use the latest GitHub Release asset (same file Sparkle and the marketing site
use):

**https://github.com/Frenzyz/gambit-releases/releases/latest/download/Gambit.dmg**

That build is **beta**. It is not Developer ID signed or notarized unless a
release note says otherwise. If macOS Gatekeeper blocks it, Control-click
Gambit and choose Open.

In-app updates use [Sparkle 2](https://sparkle-project.org/). The feed is:

**https://frenzyz.github.io/gambit-releases/appcast.xml**

(`SUFeedURL` in the app). Raw fallback:
`https://raw.githubusercontent.com/Frenzyz/gambit-releases/main/appcast.xml`.

## Layout

- `appcast.xml` — Sparkle 2 feed (updated when a release is published)
- `notes/` — HTML release notes (`0.1.0.html`, …)
- `.github/workflows/publish-appcast.yml` — regenerates the feed from the
  latest GitHub Release DMG

## Publish a build

From a machine that has `Gambit.dmg` (see `scripts/package-macos-dmg.sh` in
the source repo):

```bash
gh release create v0.1.0 Gambit.dmg \
  --repo Frenzyz/gambit-releases \
  --title "Gambit 0.1.0 beta" \
  --notes-file notes/0.1.0.html
```

Set the Actions secret **`SPARKLE_ED25519_PRIVATE_KEY`** (Ed25519 seed,
one line, never committed) on this repo. The workflow downloads Sparkle’s
`generate_appcast` / `sign_update` and writes `appcast.xml`.

Without Developer ID + notarization, Sparkle will not *install* an update
even if the feed lists one. Testers still use the DMG download above.
