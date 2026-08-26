# My Plugins

이 저장소는 특정 코딩 에이전트에 종속되지 않는 재사용 가능한 개발 스킬 모음이다.

## 사용 원칙

- 실제 작업 지침은 `plugins/*/skills/*/SKILL.md`에 있다. 에이전트가 플러그인 형식을 지원하지 않으면 해당 파일을 직접 읽고 따른다.
- 각 스킬의 YAML front matter의 `name`과 `description`은 에이전트의 자동 발견과 사람의 탐색 모두에 사용된다. 변경 시 둘 다 정확히 유지한다.
- Claude Code와 Codex의 매니페스트는 배포용 어댑터다. 스킬 본문에는 특정 제품의 명령어나 경로를 불필요하게 넣지 않는다.

## 호환성 레이어

| 대상 | 진입점 |
| --- | --- |
| Claude Code | `.claude-plugin/marketplace.json`, `plugins/*/.claude-plugin/plugin.json` |
| Codex | `.agents/plugins/marketplace.json`, `plugins/*/.codex-plugin/plugin.json` |
| 기타 에이전트 | 이 파일과 각 `SKILL.md`를 직접 읽어 적용 |
