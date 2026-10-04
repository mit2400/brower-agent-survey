# L2. Browser Automation (deterministic 엔진)

> `selector → click/fill/navigate`. LLM 없이도 동작하는 확정적 계층.

## 대안

### Playwright (Apache-2.0) — 표준 엔진
- Chromium/Firefox/WebKit 단일 API. TypeScript/Python/.NET/Java.
- 핵심: **auto-wait + web-first assertion + BrowserContext 격리 + Trace Viewer + 병렬/샤딩**.
- 로케이터: `getByRole/getByLabel/getByPlaceholder/getByTestId` — 사용자 관점, CSS 깨짐에 강함.
- `npx playwright test` / Library(`npm i playwright`) / CLI(`@playwright/cli`) / MCP(`@playwright/mcp`)로 분리 사용.
- BP: 인증 state 저장 후 재사용(`storageState`), `trace: on-first-retry`.

### Puppeteer (Apache-2.0) — Chrome 특화
- Google 유지. Chrome 전용 스크래핑·PDF·스크린샷에 가볍다.
- 크로스 브라우저 필요하면 Playwright가 정답.

### Selenium + WebDriver — 레거시/엔터프라이즈
- 언어 지원 폭이 가장 넓다. 기존 자산이 있으면 유지.
- 신규 AI agent 스택에서는 Playwright 우선.

### Steel (Apache-2.0) — Agent용 browser infrastructure
- 제품이 아니라 **"agent에게 browser를 API로 제공"**하는 계층.
- Docker/self-hosting/session/remote browser/scaling 고려시 중요.
- 구조: `AI Agent → Steel API → Browser session → Chromium`.

## 특징 비교

| | Playwright | Puppeteer | Selenium | Steel |
|---|---|---|---|---|
| 크로스 브라우저 | ✅ 3종 | ❌ Chromium | ✅ | ✅(Chromium 세션) |
| auto-wait | ✅ 핵심 | 부분 | ❌ | 엔진 의존 |
| Trace/디버그 | ✅ Trace Viewer | 기본 | 약함 | 세션 관점 |
| Agent 친화 | MCP/CLI 별도 | 낮음 | 낮음 | ✅ API 우선 |
| License | Apache-2.0 | Apache-2.0 | Apache-2.0 | Apache-2.0 |

## BP
- 반복 가능한 행동은 L2에 고정하고 LLM을 호출하지 마라 (비용·속도·신뢰성).
- L2가 흔들리는 지점(Canvas, shadow DOM, 이미지 UI)에서만 L4 AI fallback을 탄다.
