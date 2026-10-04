# L4. Browser Agent Framework (자연어 → 계획 → 실행)

> Aside와 비교할 때 **가장 중요한 계층**. OSS 1순위는 여기 있다.

## 대안

### Browser Use (MIT) — 최우선 framework 후보
- 단순 Playwright wrapper가 아니라 Python lib + CLI + harness + cloud로 확장된 ecosystem. stars 11만+ 규모.
- 구조: `User → LLM → Agent → DOM+Screenshot 융합 → Action → Browser`.
- Aside 관계: **Aside=완성품 vs Browser Use=만들기 위한 OSS framework**. 연구 관점 직접 비교군.

### Stagehand (MIT) — 기업 자동화에 중요한 hybrid reference
- 철학: `act() / observe() / extract()` → 내부적으로 Playwright.
- `await stagehand.act("click the login button")` 형태. AI+deterministic 혼합, 반복 행동 캐싱/self-healing으로 LLM 재호출 절감.
- 아키텍처 패턴으로 중요: `selector 우선 → 실패시 LLM observe → 새 action 캐시`.

### Skyvern (AGPL-3.0) — AI RPA/workflow
- Browser Use가 "agent가 브라우저 사용"이면 Skyvern은 **"업무 workflow 자동화"** (로그인→검색→인보이스 추출→PDF→ERP 업로드).
- DOM 의존 낮추고 LLM+vision으로 UI 인식. core=AGPL, anti-bot 등 일부는 cloud-only → 상용 시 주의.

### Agent TARS / UI-TARS (Apache-2.0)
- UI-TARS: vision GUI agent. `Screenshot → VLM → (x,y) → mouse/keyboard`. DOM 없이 동작.
- Agent TARS: Browser+computer+MCP 방향. L4/L5 경계.
- Playwright식 `DOM→selector→click`과 정반대 축이므로 반드시 대비 실험.

### Midscene (참고군)
- 자연어 기반 UI 자동화. L4 보조 후보로 목록 유지.

## 비교

| | Browser Use | Stagehand | Skyvern | Agent TARS/UI-TARS |
|---|---|---|---|---|
| 지향 | 범용 agent | hybrid 자동화 | RPA workflow | vision computer-use |
| License | MIT ✅ | MIT ✅ | AGPL ⚠️ | Apache-2.0 ✅ |
| DOM 의존 | 중간(hybrid) | 낮음(캐시) | 낮음 | 없음(vision) |
| 기업 적합 | 높음 | **가장 높음** | 높음(워크플로우) | 특수 UI에 강함 |
| 학습 곡선 | 중간 | 낮음 | 중간 | 높음(VLM) |

## BP
- 신규 연구·PoC 1순위: Browser Use.
- 운영·반복 작업: Stagehand 패턴(결정적 우선, AI는 fallback).
- 정형 업무 대량 처리: Skyvern (라이선스 검토 필수).
