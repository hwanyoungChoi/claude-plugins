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
/plugin install hello-world@cony-plugins
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

| 플러그인      | 설명                          | 버전  |
| ------------- | ----------------------------- | ----- |
| `hello-world` | 마켓플레이스 셋업 검증용 샘플 | 0.1.0 |

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
├── hello-world/
│   ├── .claude-plugin/
│   │   └── plugin.json
│   └── skills/
│       └── hello-world/
│           └── SKILL.md
└── README.md
```
