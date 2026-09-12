# Gambit releases

Public **binary** releases for [Gambit](https://github.com/Frenzyz/Gambit).
This repository is not the source tree.

Gambit is a local-first supervised agentic browser (`Gambit.app`, bundle id
`app.gambit.browser`). Product name is Gambit. Copyright Vision Algorithms LLC.

## Download

Use the latest GitHub Release asset (same file Sparkle and the marketing site
use):

**https://github.com/Frenzyz/gambit-releases/releases/latest/download/Gambit.dmg**

That build is an Apple-notarized **beta** (macOS 13+ Apple silicon). WebKit
is the default engine; Google Docs, Sheets, and Slides open in Chromium.

In-app updates use [Sparkle 2](https://sparkle-project.org/). The feed is:

**https://frenzyz.github.io/gambit-releases/appcast.xml**

(`SUFeedURL` in the app). Raw fallback:
`https://raw.githubusercontent.com/Frenzyz/gambit-releases/main/appcast.xml`.

## Layout

- `appcast.xml` — Sparkle 2 feed (written by the local publish script)
- `notes/` — HTML release notes (`0.1.0.html`, …)

There is no GitHub Actions workflow for notarization or the appcast.

## Publish a build

On a Mac, from the Gambit source checkout:

1. `cp .env.example .env` and fill it locally (never commit it)
2. Run `packaging/macos/make-dmg.sh`, then `packaging/macos/notarize.sh`
3. Run `packaging/macos/publish-update.sh` with `--releases-dir` pointing at
   this clone and optional `--gh-release` / `--push`

See `packaging/macos/README.md` in Frenzyz/Gambit. `gh release` runs on the
laptop. Do not add Actions secrets for Apple or Sparkle.

0.1.0 is Developer ID signed and stapled. Sparkle can install it.
