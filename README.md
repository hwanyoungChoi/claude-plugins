# cony-plugins

개인 Claude Code 플러그인 마켓플레이스.

## 설치

### 마켓플레이스 등록 (1회)

```bash
# HTTPS
/plugin marketplace add https://github.com/hwanyoungChoi/claude-plugins.git

# 또는 SSH
/plugin marketplace add git@github.com:hwanyoungChoi/claude-plugins.git
```

### 플러그인 설치

```bash
/plugin install development@cony-plugins
```

### 업데이트

```bash
/plugin marketplace update cony-plugins
```

## 팀 자동 등록 (선택)

프로젝트 레포의 `.claude/settings.json`에 다음을 추가하면 저장소를 clone하기만 해도 마켓플레이스가 자동 등록됩니다.

```json
{
  "extraKnownMarketplaces": {
    "superbin-plugins": {
      "source": {
        "source": "git",
        "url": "https://github.com/hwanyoungChoi/claude-plugins.git"
      }
    }
  }
}
```

## 현재 플러그인

| 플러그인        | 설명             | 스킬 수 |
| --------------- | ---------------- | ------- |
| `development`   | 개발용 플러그인  | 3       |

### `development` — 개발용 플러그인

| 스킬                                                       | 설명                                                                                                  |
| ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| [`code-review-fe`](./development/skills/code-review-fe/SKILL.md) | 프론트엔드(React/Next.js/TS) staged 변경사항을 FE 컨벤션 기준으로 셀프 리뷰 (디렉토리·react-query·네이밍·queryKey·hooks 안티패턴 검출) |
| [`commit-message`](./development/skills/commit-message/SKILL.md) | git 변경사항을 분석해 영문 prefix + 한글 본문 형식의 커밋 메시지 추천 (feat/fix/chore/refactor/docs)   |
| [`spec-review`](./development/skills/spec-review/SKILL.md)       | 기획서(PDF·이미지·텍스트·URL)를 개발자 관점에서 1차 검토 — 할일/리스크/기술검토/타직군 협조 4분류 정리  |

## 신규 플러그인 추가

1. 루트에 새 디렉토리 생성: `./{plugin-name}/`
2. `{plugin-name}/.claude-plugin/plugin.json` 작성
3. `{plugin-name}/skills/{skill-name}/SKILL.md` 작성
4. `.claude-plugin/marketplace.json` 의 `plugins` 배열에 항목 추가
5. 버전 태그 + PR

## 디렉토리 구조

```
claude-plugins/
├── .claude-plugin/
│   └── marketplace.json         # 카탈로그
├── development/
│   ├── .claude-plugin/
│   │   └── plugin.json
│   └── skills/
│       ├── code-review-fe/
│       │   └── SKILL.md
│       ├── commit-message/
│       │   └── SKILL.md
│       └── spec-review/
│           └── SKILL.md
└── README.md
```
