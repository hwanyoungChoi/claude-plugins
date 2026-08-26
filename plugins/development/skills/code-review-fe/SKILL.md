---
name: code-review-fe
description:
  프론트엔드(React/Next.js/TypeScript) staged 변경사항을 FE 컨벤션 기준으로 셀프 리뷰. 디렉토리 위치·API
  호출(react-query)·네이밍·queryKey·hooks 안티패턴 등을 references/CONVENTIONS.md 기준으로 검출.
---

## 동작

1. git diff --staged 수집
2. `references/CONVENTIONS.md`를 읽어 *판단 기준*으로 삼는다
3. 위반/모호한 부분 찾아 보고:
   - 디렉토리 위치 부적절
   - API 호출 안티패턴 (axios 직접 호출, queryKey 문자열 등)
   - 네이밍 컨벤션 위반
   - 안티패턴 (CONVENTIONS.md에 명시된 것)
4. 추가로 *컨벤션 외*에도 잠재 버그/성능/타입 안전성 짚기

## 참고

- references/CONVENTIONS.md
