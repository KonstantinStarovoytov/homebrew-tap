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
resources. Merging it publishes the new formula.
