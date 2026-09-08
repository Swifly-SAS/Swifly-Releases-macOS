# Release index

One GitHub Release per macOS version, tagged `macos-v{X.Y.Z}`, carrying the signed and
notarized `Swifly-{X.Y.Z}.dmg`. `macos-v1.0.1` → `macos-v1.0.25` were migrated here from
`Swifly-SAS/Swifly-Releases` on 2026-09-08, sha256-verified round-trip; everything after
that is published straight here by `Swifly-MacOS/.github/workflows/release.yml`.

## Ordering caveat — read before consuming this repo

`GET /releases` sorts by `created_at`, which is the **tagged commit's** date, not the
release's own publication time. Every migrated tag points at the same seed commit, so the
25 of them tie and their relative order is arbitrary — the GitHub API returned
`macos-v1.0.9` first on 2026-09-08, and the swifly.me download worker served a July build
because of it.

**Do not take the first element of `/releases` as "the newest".** Use the release marked
`Latest` (`GET /releases/latest`), or sort by `published_at`, or parse the semver out of the
tag. `published_at` is distinct and correct for every release here.
