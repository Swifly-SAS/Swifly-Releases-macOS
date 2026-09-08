# Swifly-Releases-macOS

Public distribution repo for the **Swifly macOS app**. It holds nothing but release
assets: one GitHub Release per version, tagged `macos-v{X.Y.Z}`, carrying the signed +
notarized `Swifly-{X.Y.Z}.dmg`.

## Why this repo exists

macOS releases used to live in [`Swifly-SAS/Swifly-Releases`](https://github.com/Swifly-SAS/Swifly-Releases),
which is **also the Velopack update feed for Windows**. Velopack's `GithubSource` reads
only `GET /releases?per_page=10&page=1` — a hard-coded, positional window of the 10 most
recent releases, with no pagination and no setting to widen it. macOS releases were
filling that window, and once they pushed the Windows feed off page 1 every Windows
client would have silently read an empty feed and reported itself up to date, forever.

Splitting the macOS assets out keeps that window Windows-only.

## What did NOT move

The **Sparkle appcast stays** at
`https://swifly-sas.github.io/Swifly-Releases/macos/appcast.xml`.

That URL is baked into `SUFeedURL` in the Info.plist of every macOS app already installed,
so it can never change. It is a file on `Swifly-Releases`' GitHub Pages branch — not a
GitHub Release — so it costs zero Velopack slots. The appcast's `<enclosure url>` entries
point here, into this repo. Sparkle's EdDSA signature covers the DMG bytes, not the URL,
so serving the same DMG from a different host is transparent to clients.

## Who publishes here

`Swifly-MacOS/.github/workflows/release.yml`, on a `v*` tag.
See `Swifly-MacOS/docs/Releasing.md`.
