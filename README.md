# GitHub Action: pipx

GitHub Action that installs Python commands using [pipx](https://pipx.pypa.io/).

Everything that pip(x) downloads is
[cached](https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows).

This action is a simpler (50-ish lines) alternative to
[threeal/pipx-install-action](https://github.com/threeal/pipx-install-action),
with a slightly different caching behaviour:

* pipx-install-action caches the installed pipx environments, but lets the
  caches go stale—one needs to explicitly specify a package version to avoid
  using a stale cache

* gh-pipx (this one) caches only pip's cache, so the latest versions requested
  are installed; the cache only speeds up downloads of pip metadata and wheels

## Usage

```yaml
jobs:
  somejob:
    steps:
      # …
      - uses: liskin/gh-pipx@v1
        with:
          packages: >-
            ruff
            'isort[colors]'
            'mypy >= 1.0'
      # …
```

### Parameters

* `packages`
    * Space-separated list of package specifications to install
    * (Required)
* `cache-date-format`
    * Date format string used as cache key (new cache will be created whenever
      the output date changes)
    * (Default: `%Y-%m`)
