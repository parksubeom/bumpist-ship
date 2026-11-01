# Releasing bumpist-ship

Callers use our workflows by tag, for example `parksubeom/bumpist-ship/.github/workflows/ci.yml@v0`.
There are two kinds of tags.

| Kind | Example | Moves? |
| --- | --- | --- |
| Fixed | `v0.1.0` | Never |
| Moving | `v0` (later `v1`) | Only onto a new fixed tag |

## Rules

1. **A fixed tag (`vX.Y.Z`) never moves.** Do not re-point or delete it. Callers that pin `@vX.Y.Z` must always get the same code.
2. **Only a moving tag (`v0`, later `v1`) moves, and only onto a new fixed tag.** This is the one case where a tag force push is allowed:

   ```bash
   git tag -f v0 <sha> && git push -f origin v0
   ```

   `<sha>` is the commit of the new fixed tag (`git rev-parse vX.Y.Z^{commit}`).
3. **Move the moving tag only when a release changes the workflows.** If behaviour is the same (for example a `.gitattributes`-only change), do not move it.
4. When the phase 2 `release.yml` arrives, it automates this procedure.

## Steps

```bash
git switch main && git pull --ff-only          # main is protected; changes land through PRs
git tag -a vX.Y.Z -m "bumpist-ship vX.Y.Z"     # new fixed tag on the release commit
git push origin vX.Y.Z

# Did the workflows change since the commit v0 points to?
git diff --stat v0 vX.Y.Z -- .github/workflows

# Only if they did:
git tag -f v0 "$(git rev-parse vX.Y.Z^{commit})" && git push -f origin v0
```

## Current state

| Tag | Commit |
| --- | --- |
| `v0.1.0` | `15a9922` (phase 0 bootstrap) |
| `v0` | `15a9922` |

## 한국어 요약

- 고정 태그(`vX.Y.Z`)는 절대 옮기지 않습니다.
- 이동 태그(`v0`, 이후 `v1`)는 새 고정 태그로만 옮깁니다. 태그 force push는 이때만 허용합니다: `git tag -f v0 <sha> && git push -f origin v0`
- 워크플로가 바뀐 릴리스에서만 이동 태그를 옮깁니다. `.gitattributes`처럼 동작이 같은 변경이면 옮기지 않습니다.
- 2단계에서 `release.yml`이 생기면 이 절차를 자동화합니다.
