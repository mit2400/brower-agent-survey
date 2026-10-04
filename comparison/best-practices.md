# Best Practices (BP 모음)

## 1. 계층 분리 BP
- L2(결정적) ↔ L4(AI) ↔ L5(제품)를 섞어 비교하지 말 것.
- Aside 비교는 L5끼리(Aside vs BrowserOS), framework 비교는 L4끼리(Browser Use vs Stagehand vs Skyvern).

## 2. 자동화 BP (Stagehand 패턴)
```text
Known site → selector/DOM (결정적, LLM 호출 금지)
Page changed → LLM observe → new action → cache → 다음엔 결정적 실행
```
- 반복 행동은 반드시 L2에 고정. LLM은 예외·변경에만.

## 3. 토큰·비용 BP
- `snapshot -i` ref 기반 (@e1) 우선. 전체 DOM·원본 스크린샷 전송 금지.
- 접근성 트리 + 크롭 이미지를 함께 전달.
- 측정: `#LLM Calls / in-out tokens / retries`를 성공률과 함께 기록.
- vision LLM은 텍스트 대비 5~10배 비쌈. Full HD 이하·턴제 처리·타임아웃 필수.

## 4. 신뢰성 BP
- Playwright: `storageState` 재사용, `trace: on-first-retry`, auto-wait 신뢰 (인위적 sleep 금지).
- 3회 재시도 룰: 동일 실패 3회 → 중단 + 상태 저장(JSON) + 사용자 알림.
- 실패시 폴백: LLM 실패 → 셀렉터 기반 로직으로 대체.

## 5. 보안·프라이버시 BP
- 비밀번호·카드 등 스크린샷 마스킹. 세션 쿠키 별도 관리.
- 민감 데이터는 로컬 우선(BrowserOS 로컬 실행·암호화 저장 검토).
- 클라우드 LLM 전송시 암호화·최소범위 전송.

## 6. 실험 BP (Phase 2/3)
- Task 7종 고정, Framework 6종 동일 조건 실행.
- 성공률 + `Cost per task = LLM + Vision + Infra + retry` 병기.
- 벤치 인용시 자체보고(예: 특정 WebVoyager 93.9%)를 독립 leaderboard처럼 서술 금지.
