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
repository, opened by `github-actions[bot]` or the Kitden release app, that change only
`Formula/kitden.rb`, and it fails unless the published bottle `root_url` ends with
`kitden-X.Y.Z`.

One-time setup for the tap owner: install the Kitden release app on this repository, then set
the variables `RELEASE_APP_CLIENT_ID` and `RELEASE_APP_BOT` (for example `kitden-release[bot]`)
and the secret `RELEASE_APP_PRIVATE_KEY`. The daily bump workflow uses the app token so its pull
requests start the tests; without the variable it falls back to `GITHUB_TOKEN`, and those pull
requests need a manual test run.
