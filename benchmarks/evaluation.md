# Evaluation (외부 평가 관점)

> "어떤 툴이 좋은가"가 아니라 **"실제 웹 task를 얼마나 잘 수행하는가"**를 잰다.
> 모든 수치는 출처를 구분한다: **self-reported(자체보고)** vs **independent(독립평가)**.

## 1. 벤치마크 선택 가이드

| 질문 | 벤치마크 | 이유 |
|---|---|---|
| 범용 웹 에이전트 능력 | WebArena-Verified | deterministic evaluator, LLM-judge 제거 |
| 기업 SaaS 업무 자동화 | WorkArena | ServiceNow 기반 지식노동 29 task |
| 실사이트 브라우징 | WebVoyager | 15개 실사이트, 단 LLM-judge 약점 |
| 시각 의존 UI | VisualWebArena | DOM 없이 시각 판단 필요 |
| 데스크톱/컴퓨터 사용 | OSWorld | 브라우저 넘어 OS 전체 |
| 종합 하네스 | BrowserGym | 위 전부를 묶는 Gym 환경 |

## 2. BrowserGym (평가 하네스)

- 단일 벤치가 아니라 MiniWoB/WebArena/VisualWebArena/WorkArena/AssistantBench/WebLINX/OpenApps/TimeWarp 등을 묶는 Gym 환경.
- 실험 하네스로 최우선. `pip install browsergym` 후 `gym.make("browsergym/webarena")`.
- 메트릭: task success rate (0/1), step success rate (부분 점수).

## 3. WebArena-Verified (2026 중심축)

- 기존 WebArena의 LLM-judge "대충 성공" 문제를 개선: 수동 검증 task + reference answer + deterministic evaluator + 258 hard subset.
- 재현성과 결정적 평가를 강화한 2026년형 평가 환경.
- 실행: `git clone` → Docker 환경 → `python run.py`.
- 주의: benchmark contents 라이선스 별도 확인.

## 4. WorkArena (기업 업무)

- ServiceNow 기반 29개 browser-based knowledge-work task.
- `search/create/update/workflow/multi-step` 영역. RPA/enterprise 목적이면 WebArena보다 중요.
- BrowserGym과 연결.

## 5. WebVoyager

- 실사이트 task 수행 평가. 단 **GPT-4V judge** 사용 → 비결정적, 프롬프트 의존.
- 순수 vision vs DOM 비교 논쟁 활발. 자체보고 수치(예: 특정 프로젝트 93.9%)는 독립 leaderboard 아님.

## 6. OSWorld (Computer Use)

- 브라우저를 넘어 OS 전체 제어 평가. OpenAI CUA 보고 예: OSWorld 38.1% / WebArena 58.1% / WebVoyager 87.0%.
- UI-TARS Desktop/Agent TARS와 함께 `Browser → Computer` 확장 장에 배치.

## 7. 측정 지표 (성공률만 보지 말 것)

```text
Success Rate          # 최종 성공 여부
Step Success Rate     # 중간 단계 성공률
Task Completion Time  # 완료 시간
# LLM Calls           # 호출 횟수
Input/Output Tokens   # 토큰 사용량
Browser Actions       # 브라우저 액션 수
Retries               # 재시도
Failure Recovery Rate # 실패 복구율
DOM vs Vision 의존도   # 아키텍처 축
Human Intervention    # 사람 개입
Cost per task         # LLM + Vision + Infra + retry 합산
```

## 8. 출처 구분 원칙

| 구분 | 정의 | 예시 |
|---|---|---|
| self-reported | 프로젝트 팀이 자체 설정으로 발표 | Browser Use README, Skyvern 블로그, Stagehand evals |
| independent | 제3자가 동일 프로토콜로 평가 | BrowserGym leaderboard, WebArena-Verified 논문 |
| vendor-modified | 벤치마크를 수정 후 보고 | Skyvern WebVoyager (날짜 현대화, 8 task 제거) |

> 비교표 작성 시 반드시 "출처 구분" 컬럼을 둘 것. 자체보고 수치를 독립평가처럼 인용 금지.
