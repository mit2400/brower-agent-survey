# L3. Agent Tool / MCP (LLM에게 browser tool 제공)

> Agent Framework(L4)가 아니라 **LLM ↔ 브라우저 사이의 얇은 어댑터**로 봐야 한다.

## 대안

### Playwright MCP (`microsoft/playwright-mcp`, OSS/Apache 계열)
- Microsoft 제공 MCP server. 구조: `Agent → MCP → Playwright MCP → Playwright → Browser`.
- 2026년 agent ecosystem 표준 인터페이스가 MCP이므로 Playwright 본체와 분리 평가.
- Claude Code/Codex 계열 연동이 목적이면 최우선 후보.

### agent-browser (Apache-2.0, Rust CLI)
- AI agent용 50+ 명령어 CLI. `open → snapshot -i → click @e1 / fill @e2 → screenshot → close`.
- snapshot이 A11y tree + ref(`@e1`) 반환 → **200~400 토큰**으로 DOM 수천 토큰 대체. 토큰 효율 최상.
- MCP server 모드, iOS Simulator 제어, React/Web Vitals, 녹화·스트리밍·프로파일 내장.
- 단, Browser Use/Stagehand급 **Agent Framework가 아니라 tool**로 분류.

### CDP (직접 사용)
- Rust daemon 등에서 CDP 직결. 최고 속도·최소 오버헤드.
- 일반 연구자는 직접 다루지 말고 Playwright/agent-browser経由 권장.

## 역할 정리

| 프로젝트 | 역할 |
|---|---|
| Playwright | automation engine |
| agent-browser | agent CLI/tool |
| Playwright MCP | agent protocol/tool |
| CDP | transport |

## BP
- 빠른 프로토타이핑: `agent-browser` CLI (`npm i -g agent-browser`).
- 에디터 에이전트 연동: Playwright MCP (`mcp.json`).
- 전체 스크린샷 원본 전송 금지. **A11y tree + 크롭 영역** 조합이 비용·정확도 최적.
