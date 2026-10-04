# Benchmarks (에이전트 평가 계층 — 별도 장으로 취급)

> "어떤 툴이 좋은가"가 아니라 **"실제 웹 task를 얼마나 잘 수행하는가"**를 잰다.

## BrowserGym (OSS) — 평가 ecosystem 본체
- 단일 벤치가 아니라 MiniWoB / WebArena / VisualWebArena / WorkArena / AssistantBench / WebLINX / OpenApps / TimeWarp 등을 묶는 Gym 환경.
- 서베이 실험 하네스로 최우선.

## WebArena-Verified (OSS, 조건 확인)
- 기존 WebArena의 재현성 문제(LLM judge "대충 성공")를 개선: 수동 검증 task + reference answer + deterministic evaluator + 258 hard subset.
- 2026년형 평가 중심축으로 권장.

## WorkArena (OSS)
- ServiceNow 기반 지식노동 29 task. `search/create/update/workflow/multi-step` 기업 SaaS 영역.
- RPA/enterprise 목적이면 WebArena보다 중요.

## WebVoyager
- 실사이트 task 수행 평가. vision vs DOM 비교 논쟁이 활발 (예: 순수 vision 93.9% 자체 보고 — 독립 leaderboard 아님, 인용 주의).

## VisualWebArena / WebLINX / AssistantBench
- 시각 의존 task / 대화형 내비게이션 / 어시스턴트 종합으로 분할 인용.

## OSWorld (+ OpenAI CUA 보고)
- Browser를 넘어 Computer-use로 확장될 때 사용. CUA 보고 예: OSWorld 38.1% / WebArena 58.1% / WebVoyager 87.0%.
- UI-TARS Desktop/Agent TARS와 함께 `Browser → Computer` 확장 장에 배치.

## 실험 설계 권장

```text
Task 7종 × Framework 6종(Playwright/Browser Use/Stagehand/Skyvern/BrowserOS/UI-TARS)
측정: Success / Step Success / Time / #LLM Calls / Tokens(in/out) / Retries / Recovery / Cost per task
```

- 성공률만 보지 말고 **Cost per task = LLM + Vision + Infra + retry**를 병기.
