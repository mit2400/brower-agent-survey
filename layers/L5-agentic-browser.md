# L5. Agentic Browser / Product (웹에서 알아서 업무 수행)

## Aside (상용 — 기준점, OSS 아님)

- `Aside Computer Inc.` 상용 브라우저. Terms에 "paid or free plans" 명시, non-transferable license.
- 오픈소스는 `aside-api`(MIT 프록시) 등 주변부에만 존재. 본체 자동화는 proprietary.
- 강점: Online-Mind2Web/BU-Bench/Odyssey 상위 보고, 로컬 메모리, 자격증명 자동입력+민감행동 승인, 개발자 CLI/MCP/REPL.
- 서베이에서의 용도: **성능·UX 기준점**. 직접 도입 대상이 아니라 비교 대상.

## BrowserOS (AGPL-3.0 — Aside OSS replacement 1순위)

- `browseros-ai/BrowserOS`. open-source agentic Chromium 포크.
- AI agent native, MCP agent(Claude Code/Codex), parallel agents, session replay, local execution 강조.
- Chromium + Chrome login import 제공.
- License **AGPL-3.0** (BrowserOS/neo 모두). 배포·수정시 소스공개 의무 → 상용 구조 주의.

## 비교

| | Aside | BrowserOS |
|---|---|---|
| 형태 | AI browser (완성품) | AI browser (OSS) |
| Chromium | ✅ | ✅ |
| Agent native | ✅ | ✅ |
| MCP | 가능/지원 | ✅ |
| local-first | 부분적 | 강함 |
| OSS | ❌ | ✅ AGPL-3.0 |
| 목적 | Consumer/Product | OSS Agent Browser |

## 그 외 상용 (지형 파악용, 도입 제외)

- Comet / Atlas / Dia 등: 폐쇄형이거나 데이터 정책 부담. 서베이에서는 존재만 기록.
- Reddit 등에서 "Aside를 무료 OSS로" 요구가 있으나, 현재 제품급 OSS는 BrowserOS가 최근접.

## BP
- "Aside 대체"를 말할 때는 반드시 L5끼리(Aside vs BrowserOS)로 비교.
- L2/L3 building block(Playwright/agent-browser)을 L5 대체품처럼 서술하지 말 것.
