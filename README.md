# Homebrew tap for Kitden

[Kitden](https://github.com/KonstantinStarovoytov/kitden) shows what Claude Code, Codex and
Cursor load, and changes it with a preview, a backup and Undo.

## Install

```bash
brew install konstantinstarovoytov/tap/kitden
```

Then run `kitden`. Update with `brew upgrade kitden`.

Homebrew builds Kitden and its Python dependencies from source. The first install takes a
few minutes.

## How the formula is updated

A workflow checks PyPI once a day and opens a pull request with the new version and its
resources. Kitden's release flow opens the same kind of pull request.

Never press the Merge button on a bump. Once `brew test-bot` passes on a `bump-kitden-X.Y.Z`
pull request, the `auto-pull` workflow runs `publish.yml` (`brew pr-pull`), which publishes
the bottles and pushes the formula to main. It accepts only pull requests from this
repository, opened by `github-actions[bot]`, the tap's own app (Kitden Kettle) or the Kitden release app
(Kitden Beacon), that
change only `Formula/kitden.rb`, and it fails unless the published bottle `root_url` ends with
`kitden-X.Y.Z`. Once a test run has passed on a `bump-kitden-` pull request, any rejected check
makes the `auto-pull` run red on purpose. A red run for a bump that a newer commit or version
superseded is expected; look at the newest bump instead.

One-time setup for the tap owner:

1. Create a GitHub App for this tap only, Kitden Kettle (`kitden-kettle`), with the repository
   permissions Contents and Pull requests (read and write), and install it on this repository
   only. Do not use the Kitden release app here: `brew bump` runs code from outside this
   repository, and the release app's key can tag Kitden, which publishes to PyPI. That key is
   stored only in Kitden's `release` environment.
2. Set the variables `TAP_APP_CLIENT_ID` (the tap app's client ID), `TAP_APP_BOT` (its bot
   login, `kitden-kettle[bot]`) and `RELEASE_APP_BOT` (the Kitden release app's
   bot login, `kitden-beacon[bot]`), and the secret `TAP_APP_PRIVATE_KEY` (the tap
   app's private key).
3. Install the Kitden release app, Kitden Beacon, on this repository too, so Kitden's publish job can open its
   pull request here.

The daily bump workflow uses the tap app's token so its pull requests start the tests; without
`TAP_APP_CLIENT_ID` it falls back to `GITHUB_TOKEN`, and those pull requests need a manual test
run.
