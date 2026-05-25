---
name: commit-message
description: 현재 git 저장소의 변경사항(staged/unstaged)을 분석해 영문 prefix + 한글 본문 형식의 커밋 메시지를 추천. 사용자가 "커밋 메시지 추천해줘", "커밋명 추천", "commit-message" 등으로 호출 시 활성화. Prefix는 feat/fix/chore/refactor/docs 중 선택.
---

# Commit Message Suggester

현재 작업 중인 git 저장소의 변경사항을 분석해서, 사내 컨벤션에 맞는 커밋 메시지(영문 prefix + 한글 본문)를 추천한다.

## 트리거

다음 입력 시 활성화:

- `commit-message`
- 자연어: "커밋 메시지 추천해줘", "커밋명 추천", "이거 어떻게 커밋해?"

## 동작 절차

### 1. 변경사항 수집

```bash
# 1) 저장소 상태 확인
git status

# 2) staged 우선
git diff --staged

# 3) staged가 비어있으면 unstaged 확인
git diff
```

**판단 규칙**:

- staged 변경이 있으면 → **그것만** 분석 대상으로 삼음
- staged 비어있고 unstaged만 있으면 → unstaged + untracked 파일 목록 분석
- 변경이 전혀 없으면 → "변경사항 없음" 안내 후 종료
- 현재 디렉토리가 git 저장소가 아니면 → 안내 후 종료

### 2. Prefix 선택

| Prefix        | 사용 시점                                                  |
| ------------- | ---------------------------------------------------------- |
| **feat:**     | 새 기능/파일/컴포넌트/엔드포인트/스킬 추가, 새 사용자 기능 |
| **fix:**      | 버그 수정, 예외 처리 보완, 잘못된 동작 교정                |
| **refactor:** | 동작은 동일하나 코드 구조/네이밍/분리 개선                 |
| **docs:**     | README, CLAUDE.md, 주석, 가이드 문서만 변경                |
| **chore:**    | 설정 파일, 빌드 스크립트, 의존성, .gitignore 등 기타       |

**판단 우선순위** (위에서부터):

1. \*.md 또는 주석만 변경 → `docs:`
2. package.json / 설정 파일 / 빌드 스크립트만 변경 → `chore:`
3. 새 기능 파일/함수/엔드포인트/스킬 추가가 주된 변경 → `feat:`
4. 기존 코드의 _잘못된 동작_ 교정 시그널 (조건문 수정, null 처리 추가 등) → `fix:`
5. 동작 동일하고 구조만 변경 (extract function, 파일 분리 등) → `refactor:`

**모호하면** 가장 가까운 것 선택하되, 대안 후보도 함께 제시.

### 3. 본문 작성 (한글)

규칙:

- **50자 이내** 권장 (헤더 한 줄)
- 시제: 현재형 ("추가", "수정", "정리", "분리", "변경")
- *어떻게*보다 _무엇을_ 위주
- 영문 식별자(함수명, 변수명, 라이브러리명 등)는 그대로 유지
- 한 줄 요약. 부연 설명 필요하면 빈 줄 + 본문 추가 (선택)

**좋은 예**:

- `feat: useSettlementDetail 훅 추가 및 MonthlyContainer 연결`
- `fix: closedAt 시간 UTC 변환 처리`
- `refactor: constants.ts에서 type 분리`
- `docs: README에 마켓플레이스 등록 절차 추가`
- `chore: husky pre-commit 훅 설정 추가`

**피해야 할 표현**:

- "여러 가지 변경", "기타 수정" (구체성 부족)
- "버그 픽스", "리팩토링" (한글 본문에 영문 카테고리 중복)

### 4. 출력 형식

가장 적합한 후보 + 대안 1~2개 제시:

```
변경사항 요약:
- {핵심 변경 1줄}
- {핵심 변경 1줄}

추천 커밋 메시지:

1. feat: useSettlementDetail 훅 추가 및 MonthlyContainer 연결
2. feat: 포인트 정산 상세 조회 API 연동

실행:
git commit -m "feat: useSettlementDetail 훅 추가 및 MonthlyContainer 연결"
```

## 예외 케이스

| 상황                              | 처리                                                                 |
| --------------------------------- | -------------------------------------------------------------------- |
| 변경이 *복수 prefix*에 걸침       | "분할 커밋 권장" 안내 + 각 그룹별 메시지 후보 제시                   |
| 단순 공백/포맷팅만                | `chore:` 사용 권장 (사내 prefix 목록에 style이 없으므로)             |
| 변경량이 매우 큼 (500줄+)         | 분할 커밋 강하게 권장. 그래도 한 번에 가겠다면 가장 _주된_ 변경 기준 |
| 자동 생성 파일 변경 (lockfile 등) | `chore:` 우선                                                        |

## 클립보드 복사 (선택)

사용자가 `--copy` 또는 "클립보드에 복사" 요청 시:

```bash
printf "feat: ..." | pbcopy
```

macOS 기준. 다른 OS는 환경에 맞춰 처리.
