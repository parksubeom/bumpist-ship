# bumpist-ship

Reusable GitHub Actions workflows and a machine-readable quality report for frontend projects.
Part of the [Bumpist Suite](https://github.com/parksubeom), but usable on its own in any repository.

> **Status: v0 (phase 0).** `ci.yml` works today. `db`, `deploy-vercel`, `e2e`, `visual-qa`, `storybook`, `review`, and `release` arrive in phase 1–2.

## Use it in 1 minute

```yaml
# .github/workflows/ci.yml in your repository
name: ci
on: [pull_request, push]
jobs:
  ci:
    uses: parksubeom/bumpist-ship/.github/workflows/ci.yml@v0
```

`ci.yml` installs with pnpm, then runs `typecheck`, `lint`, `test`, `build` and `check:schemas` **if your package.json has them**, and uploads a quality-report fragment (contract C5).

## What's in here

| Path | What |
| --- | --- |
| `.github/workflows/ci.yml` | Reusable CI gate |
| `schemas/quality/v0.json` | Contract C5 — quality report |
| `renovate/default.json` | Shared Renovate preset (`extends: ["github>parksubeom/bumpist-ship//renovate/default"]`) |
| `scripts/dev-workspace.sh` | Clones all five Bumpist repos side by side and links their packages for local development |

## Versioning

`@v0` moves with every v0 release; pin `@v0.x.y` if you need a fixed version.

[한국어 README](./README.ko.md) · MIT
