# my-plugins

개발 작업에 재사용하는 범용 에이전트 스킬 모음입니다. 핵심 지침은 표준 `SKILL.md`로 관리하며, Claude Code와 Codex는 각각의 플러그인 매니페스트로 설치할 수 있습니다. 그 밖의 에이전트는 [AGENTS.md](./AGENTS.md)와 원하는 `SKILL.md`를 직접 읽어 사용할 수 있습니다.

## 지원 방식

| 환경 | 사용 방법 |
| --- | --- |
| Claude Code | Claude 마켓플레이스로 등록·설치 |
| Codex | Codex 마켓플레이스로 등록·설치 |
| 기타 에이전트 | `AGENTS.md` 및 `plugins/*/skills/*/SKILL.md`를 작업 지침으로 읽기 |

## 설치

레포 이름을 GitHub에서 `my-plugins`로 변경한 뒤 아래 URL을 사용하세요.

### Claude Code

```bash
/plugin marketplace add https://github.com/hwanyoungChoi/my-plugins.git
/plugin install development@my-plugins
```

업데이트:

```bash
/plugin marketplace update my-plugins
```

### Codex

```bash
codex plugin marketplace add https://github.com/hwanyoungChoi/my-plugins.git
codex plugin add development@my-plugins
```

플러그인 변경 후에는 다시 설치하고 새 task에서 사용하세요.

### 기타 에이전트

저장소를 clone하거나 스킬 디렉터리를 프로젝트에 포함한 뒤, 에이전트가 다음 파일을 컨텍스트로 읽게 하면 됩니다.

```text
AGENTS.md
plugins/development/skills/<skill-name>/SKILL.md
```

## 카탈로그

### `development` — 개발 워크플로우

| 스킬 | 설명 |
| --- | --- |
| [`code-review-fe`](./plugins/development/skills/code-review-fe/SKILL.md) | 프론트엔드(React/Next.js/TypeScript) staged 변경사항을 FE 컨벤션 기준으로 검토 |
| [`commit-message`](./plugins/development/skills/commit-message/SKILL.md) | Git 변경사항을 분석해 영문 prefix + 한글 본문 형식의 커밋 메시지 추천 |
| [`spec-review`](./plugins/development/skills/spec-review/SKILL.md) | 기획서(PDF·이미지·텍스트·URL)를 개발 관점에서 1차 검토 |

## 새 플러그인 추가

1. `plugins/{plugin-name}/skills/{skill-name}/SKILL.md`를 만든다.
2. Claude Code용 `plugins/{plugin-name}/.claude-plugin/plugin.json`을 만든다.
3. Codex용 `plugins/{plugin-name}/.codex-plugin/plugin.json`을 만든다.
4. `.claude-plugin/marketplace.json`과 `.agents/plugins/marketplace.json`에 같은 플러그인을 등록한다.
5. `AGENTS.md`와 이 문서의 카탈로그를 갱신한다.

## 디렉터리 구조

```text
my-plugins/
├── AGENTS.md                         # 에이전트 공통 안내
├── .agents/plugins/marketplace.json  # Codex 카탈로그
├── .claude-plugin/marketplace.json   # Claude Code 카탈로그
└── plugins/
    └── development/
        ├── .claude-plugin/plugin.json
        ├── .codex-plugin/plugin.json
        └── skills/
            ├── code-review-fe/SKILL.md
            ├── commit-message/SKILL.md
            └── spec-review/SKILL.md
```
