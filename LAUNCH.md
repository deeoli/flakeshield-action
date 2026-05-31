# Launch — one manual step

GitHub does not allow `GITHUB_TOKEN` to change user-package visibility (GET works; PATCH returns 404). Flip visibility once as the package owner.

## Option A — GitHub UI (fastest)

1. Open [flakeshield-core package settings](https://github.com/users/deeoli/packages/container/package/flakeshield-core/settings)
2. Under **Danger Zone** → **Change visibility**
3. Select **Public** and confirm

## Option B — CLI

```powershell
gh auth refresh -h github.com -s read:packages,write:packages
gh api --method PATCH /users/deeoli/packages/container/flakeshield-core -f visibility=public
```

## Verify

Anonymous pull should succeed (no auth):

```bash
curl -sI https://ghcr.io/v2/deeoli/flakeshield-core/manifests/0.6.0-beta.1
```

Expect `HTTP/2 200` (not 401).

After this one-time step, all future release tags inherit public visibility.
