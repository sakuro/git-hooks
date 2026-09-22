# AGENTS.md

## Purpose

This repository defines Pkl files that are imported as global
[hk](https://hk.jdx.dev/) hooks, configured by
[sakuro/dotfiles](https://github.com/sakuro/dotfiles). It contains no
application code of its own — only Pkl configuration.

## Release

Push a `vX.Y.Z` tag to `main` to trigger `.github/workflows/release.yml`,
which packages the Pkl project and creates a GitHub Release:

```sh
git tag -a vX.Y.Z -m "Release vX.Y.Z"
git push origin vX.Y.Z
```
