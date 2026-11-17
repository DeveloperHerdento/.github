# .github (organization defaults)

Contents of the special `.github` repository of the DeveloperHerdento GitHub organization.

| File | What it does |
|---|---|
| `SECURITY.md` | Shown automatically in every repo that has no own security policy |
| `.github/workflows/ci-node.yml` | Reusable CI for Node / TypeScript: lint → format → typecheck → test → build → gitleaks |
| `.github/workflows/ci-python.yml` | Reusable CI for Python: ruff → format → pytest → notebook check → gitleaks |
| `.github/workflows/deploy-vps.yml` | Reusable deploy: build image → GHCR → SSH → compose up → wait healthy → smoke test |

Fixing CI here fixes it for every repo that calls these workflows.

## One-time setup

1. Create a repository named `.github` in the organization and copy these files into it.
2. Replace `__ORG__` and `__SECURITY_EMAIL__`.
3. **Settings → Actions → General → Access:** "Accessible from repositories in the __ORG__ organization".
4. Tag the first release so repos can pin it: `git tag v1 && git push origin v1`.

## Changing a workflow

- Backward-compatible change (new optional input, faster step): merge, then move the tag: `git tag -f v1 && git push -f origin v1`.
- Breaking change (renamed input, new required secret): release it as `v2` and update repos one by one.
