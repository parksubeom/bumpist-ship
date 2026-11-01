# bumpist-ship

프론트엔드 프로젝트용 재사용 GitHub Actions 워크플로와 기계가 읽는 품질 보고서(C5)입니다. Bumpist Suite의 배포·CI/CD 층이지만, 다른 저장소 없이 단독으로 쓸 수 있습니다.

> **상태: v0 (0단계).** 지금은 `ci.yml`만 동작합니다. `db`·`deploy-vercel`·`e2e`·`visual-qa`·`storybook`·`review`·`release`는 1~2단계에서 추가됩니다.

사용법은 [영문 README](./README.md)의 예시 그대로입니다. `package.json`에 `typecheck`·`lint`·`test`·`build`·`check:schemas` 스크립트가 있으면 순서대로 실행하고, 결과를 C5 형식으로 남깁니다.
