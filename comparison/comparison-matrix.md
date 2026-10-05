# 전체 비교표 (계층 × OSS × 라이선스 × 아키텍처)

## 1. 계층별 OSS 지도

| 계층 | 프로젝트 | OSS | License | 역할 한줄 |
|---|---|---|---|---|
| L2 | Playwright | ✅ | Apache-2.0 | 표준 automation engine |
| L2 | Puppeteer | ✅ | Apache-2.0 | Chrome 특화 |
| L2 | Selenium | ✅ | Apache-2.0 | 레거시 호환 |
| L2/L3 | Steel | ✅ | Apache-2.0 | agent용 browser infra/API |
| L3 | Playwright MCP | ✅ | Apache 계열 | MCP 표준 연동 |
| L3 | agent-browser | ✅ | Apache-2.0 | 토큰효율 CLI tool |
| L4 | Browser Use | ✅ | MIT | 대표 agent framework |
| L4 | Stagehand | ✅ | MIT | hybrid (deterministic+AI), v4는 CDP 네이티브 |
| L4 | Skyvern | ✅ | AGPL-3.0 | AI RPA/workflow |
| L4/L5 | Agent TARS | ✅ | Apache-2.0 | browser+computer+MCP |
| L4 | UI-TARS | ✅ | Apache-2.0 | vision GUI agent |
| L5 | BrowserOS | ✅ | AGPL-3.0 | AI-native browser 제품 |
| L5 | Aside | ❌ | Commercial | 비교 기준점 (도입 제외) |
| Bench | BrowserGym | ✅ | OSS | 평가 하네스 |
| Bench | WebArena-Verified | ✅ | OSS(조건확인) | 결정적 평가 |

## 2. 아키텍처 축

| 축 | 대표 | 강점 | 약점 |
|---|---|---|---|
| DOM-first | Playwright/agent-browser/MCP | 정확·빠름·토큰효율·결정적 | canvas/이미지UI/shadowDOM 취약 |
| Vision-first | UI-TARS/Computer Use | DOM 불필요·인간 유사 | 비용·좌표오차·느림 |
| Hybrid | Browser Use/Stagehand/Skyvern/BrowserOS | 신뢰↔범용 균형 | 복잡도↑ |

```text
Reliability ▲
  Playwright(deterministic)
  Stagehand / Browser Use / Skyvern (hybrid)
  UI-TARS (vision)                    ▶ Generality
```

## 3. 목적별 1순위

| 목적 | 선택 |
|---|---|
| Aside 대체 제품 연구 | BrowserOS |
| 범용 agent framework PoC | Browser Use |
| 운영·반복 자동화 | Stagehand 패턴 |
| 정형 업무 대량 처리 | Skyvern (라이선스 주의) |
| 인프라·스케일 | Steel + Playwright |
| 에이전트 연동 | Playwright MCP + agent-browser |
| 특수 UI (canvas/이미지) | UI-TARS 계열 |
| 평가 | BrowserGym + WebArena-Verified (+WorkArena) |
