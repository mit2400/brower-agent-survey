# Architecture: DOM vs Vision vs Hybrid

## A. DOM-first

```text
Website → DOM/A11y Tree → LLM → selector → action
```

- 해당: Playwright, agent-browser, Playwright MCP, Browser Use 일부.
- 장점: 정확·토큰효율·빠름·결정적. `getByRole` 같은 사용자관점 로케이터.
- 한계: canvas·custom UI·shadow DOM·이미지UI·화면-DOM 불일치.

## B. Vision-first

```text
Screenshot → VLM → (x,y) → mouse/keyboard
```

- 해당: UI-TARS, Computer Use, BrowserOS/Browser Use 일부.
- 장점: DOM 없어도 가능, 인간과 유사, arbitrary UI.
- 한계: 토큰·연산 비용, 좌표 오차, 느림, 화면 변화 취약.

## C. Hybrid (2026 주목)

```text
Page → ┬→ DOM → DOM reasoning ─┐→ Planner → Action
       └→ Screenshot → Vision ─┘
```

- 해당: Browser Use, Stagehand, Skyvern, Agent TARS, BrowserOS.
- 패턴: `selector 우선 → 실패시 LLM observe → 새 action 캐시 → 다음엔 결정적으로 실행`.

## 실무 함의

- LLM vision 단독(`100% LLM`)보다 `80% deterministic + 20% AI fallback`이 운영에 현실적.
- 토큰 최적화: 전체 스크린샷 금지. **A11y ref(@e1) + 크롭 영역** 병행.
- Xephyr(`DISPLAY=:1`)+스크린샷+외부 VLM 조합은 Computer-use 확장 실험용. 기본 스택은 Playwright/agent-browser 우선.
