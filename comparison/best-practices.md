# Best Practices (통합 BP — 세부조사 반영)

> 6개 도제(Browser Use/Stagehand/Skyvern/BrowserOS/UI-TARS/Benchmarks) 수집 결과를 종합.
> 핵심 원칙: **결정적 자동화를 우선하고, AI는 예외·변경에만.**

## 1. 계층 분리 BP

- L2(결정적) ↔ L4(AI) ↔ L5(제품)를 섞어 비교하지 말 것.
- Aside 비교는 L5끼리(Aside vs BrowserOS), framework 비교는 L4끼리(Browser Use vs Stagehand vs Skyvern).
- `Playwright + agent-browser + Vitest`는 Aside 대체품이 아니라 **building blocks**.

## 2. 결정적 우선 BP (Stagehand 패턴 — v4 정정 반영)

```text
Known site → selector/DOM (결정적, LLM 호출 금지)
Page changed → LLM observe → new action → cache → 다음엔 결정적 실행
```

- **정정**: Stagehand v4는 Playwright 위가 아니라 **Chrome extension + CDP "understudy" 레이어**. v1–v3만 Playwright fork.
- **정정**: "80% deterministic + 20% AI"는 Stagehand 공식 주장이 아님. 실제 주장은 "2x faster, ~80% more token efficient"(self-reported).
- **정정**: v4에서 `agent()` 제거. 대체는 code mode(권장) 또는 tool calling.
- 반복 행동은 반드시 L2에 고정. LLM은 예외·변경에만.

## 3. 토큰·비용 BP

- `snapshot -i` ref 기반(@e1) 우선. 전체 DOM·원본 스크린샷 전송 금지.
- 접근성 트리 + 크롭 이미지를 함께 전달.
- 측정: `#LLM Calls / in-out tokens / retries`를 성공률과 함께 기록.
- vision LLM은 텍스트 대비 5~10배 비쌈. Full HD 이하·턴제 처리·타임아웃 필수.
- Browser Use: DOM+screenshot 하이브리드로 토큰 절감. Stagehand: 캐시 히트 시 LLM 0회.

## 4. 신뢰성 BP

- Playwright: `storageState` 재사용, `trace: on-first-retry`, auto-wait 신뢰(인위적 sleep 금지).
- 3회 재시도 룰: 동일 실패 3회 → 중단 + 상태 저장(JSON) + 사용자 알림.
- 실패시 폴백: LLM 실패 → 셀렉터 기반 로직으로 대체.
- Browser Use: 스텝 기반 재시도 + 히스토리 자기교정 + max_steps 제한.
- Skyvern: Run 상태(`failed`/`terminated`/`timed_out`) 기반 분류 + Validation/Conditional 블록 + HITL.

## 5. 보안·프라이버시 BP

- 비밀번호·카드 등 스크린샷 마스킹. 세션 쿠키 별도 관리.
- 민감 데이터는 로컬 우선(BrowserOS 로컬 실행·암호화 저장).
- 클라우드 LLM 전송시 암호화·최소범위 전송.
- Skyvern: anti-bot/CAPTCHA는 cloud-only. OSS 셀프호스팅은 CAPTCHA 시 30초 일시정지 후 수동 개입.
- BrowserOS: 세션/스크린샷/히스토리 로컬 전용. LLM은 로컬(Ollama) 또는 BYO API 키 선택.

## 6. 실험 BP (Phase 2/3)

- Task 7종 고정, Framework 6종 동일 조건 실행.
- 성공률 + `Cost per task = LLM + Vision + Infra + retry` 병기.
- 벤치 인용시 자체보고(예: 특정 WebVoyager 93.9%)를 독립 leaderboard처럼 서술 금지.
- BrowserGym + WebArena-Verified를 평가 중심축으로.

## 7. 라이선스 BP

- Apache-2.0/MIT: 출처 명시로 충분. Playwright/agent-browser/Stagehand/Browser Use/Steel/UI-TARS.
- AGPL-3.0: 수정 배포시 소스공개 의무. BrowserOS/Skyvern. SaaS/내부사용 구조 검토 필수.
- 모델 가중치: 코드 Apache라도 가중치 라이선스 별도 확인. UI-TARS-1.5-7B는 Apache-2.0, UI-TARS-2는 비공개.
- 외부 VLM API: 각 제공자 약관 준수. 비용·데이터 전송 고지.

## 8. 아키텍처 선택 BP

| 상황 | 선택 |
|---|---|
| 범용 agent PoC | Browser Use (MIT) |
| 운영·반복 자동화 | Stagehand 패턴 (결정적 우선) |
| 정형 업무 대량 처리 | Skyvern (AGPL 주의) |
| Aside 대체 제품 | BrowserOS (AGPL) |
| 특수 UI (canvas/이미지) | UI-TARS 계열 (vision) |
| 인프라·스케일 | Steel + Playwright |
| 에이전트 연동 | Playwright MCP + agent-browser |
