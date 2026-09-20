# gha-mirror-bitbucket

Composite action: push-mirrors the caller repo to Bitbucket Cloud (`git clone --mirror` + `git push --mirror`).
Bitbucket has no pull mirroring and no push-to-create -- the target repository must already exist there.

```yaml
- uses: alderichoarau/gha-mirror-bitbucket@v1
  with:
    bitbucket-token: ${{ secrets.BITBUCKET_MIRROR_TOKEN }}
    bitbucket-workspace: alderic-hoarau
```

`bitbucket-token` must be an **API token with scopes** (Settings -> API tokens with scopes on
Bitbucket, not a plain Atlassian API token or an App Password -- both are retired/unscoped),
granted only `read:repository:bitbucket` and `write:repository:bitbucket`.

`bitbucket-repo` defaults to this repo's own name; set it to mirror into a differently-named
Bitbucket repository instead.

## Versioning

Tags are bare `vN`, immutable, never moved -- native Dependabot `github-actions` updates work.
Release a new version: run **"Tag a new version"** (manual dispatch) -- only after an actual
change to this repo's content. Running it again with nothing new since the last tag is refused
by the workflow (it would just create a duplicate tag pointing at the same commit).
