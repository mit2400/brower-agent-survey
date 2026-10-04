# Browser / Computer Agent Survey (OSS 중심, 2026-10 기준)

> Aside(상용, L5)를 직접 쓰지 않고 OSS로 대체·재구현하기 위한 지형 정리.
> 핵심 질문: **"AI Agent가 웹을 안정적으로 조작하기 위해 DOM, A11y Tree, Screenshot, Vision, Browser State를 어떻게 조합하는가?"**

## 5계층 + Benchmark

```text
L5 Agentic Browser / Product : Aside(상용) / BrowserOS(OSS)
L4 Browser Agent Framework   : Browser Use / Stagehand / Skyvern / Agent TARS / Midscene
L3 Agent Tool / MCP          : Playwright MCP / agent-browser / CDP
L2 Browser Automation        : Playwright / Puppeteer / Selenium / Steel
L1 Browser / Runtime         : Chromium / Firefox / WebKit / CDP / WebDriver
+  Benchmark                 : BrowserGym / WebArena-Verified / WorkArena / WebVoyager / OSWorld
```

## 폴더 구조

```text
browser-agent-survey/
├── README.md                    # 이 파일. 전체 지도
├── layers/
│   ├── L1-runtime.md            # 브라우저·런타임·프로토콜
│   ├── L2-automation.md         # Playwright/Puppeteer/Selenium/Steel
│   ├── L3-agent-tool.md         # Playwright MCP / agent-browser / CDP
│   ├── L4-agent-framework.md    # Browser Use / Stagehand / Skyvern / Agent TARS
│   └── L5-agentic-browser.md    # Aside(상용 기준점) / BrowserOS
├── benchmarks/
│   └── benchmarks.md            # BrowserGym / WebArena-Verified / WorkArena / WebVoyager / OSWorld
└── comparison/
    ├── comparison-matrix.md     # 전체 비교표 (계층×라이선스×아키텍처)
    ├── architecture.md          # DOM-first vs Vision-first vs Hybrid
    ├── best-practices.md        # BP: deterministic 80% + AI 20%
    └── license.md               # OSS 라이선스·상용화 주의점
```

## 한눈에 보는 결론

| 목적 | 1순위 OSS |
|---|---|
| Aside 대체 제품 | **BrowserOS** (AGPL-3.0, AI-native Chromium) |
| Agent Framework | **Browser Use** (MIT) → **Stagehand** (MIT) → **Skyvern** (AGPL) |
| Automation Engine | **Playwright** (Apache-2.0) |
| Agent 연동 | **Playwright MCP** + **agent-browser** (Apache-2.0) |
| Infra/Scaling | **Steel** (Apache-2.0) |
| Vision/Computer Use | **UI-TARS / Agent TARS** (Apache-2.0) |
| 평가 | **BrowserGym + WebArena-Verified** 중심 |

## Category 주의

- `Playwright + agent-browser + Vitest`는 Aside 대체품이 아니라 **Aside를 만들 수 있는 building blocks**다.
- 올바른 비교: `Aside ≈ BrowserOS ≈ Browser Use + Runtime + Agent UI`.

## 다음 단계 (Phase 1→3)

1. **Phase 1**: 6개 심층 - Playwright / Browser Use / Stagehand / Skyvern / BrowserOS / UI-TARS
2. **Phase 2**: 동일 task 7종으로 실행 비교 (검색·로그인·쇼핑몰 필터·SPA modal·Canvas·DOM변경·multi-step)
3. **Phase 3**: Success / Time / #LLM Calls / Tokens / Retries / Cost per task 측정
