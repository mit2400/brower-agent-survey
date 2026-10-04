# License / 상용화 주의점 (OSS only)

## 안전군 (상용 부담 낮음)

| 프로젝트 | License | 비고 |
|---|---|---|
| Playwright | Apache-2.0 | package.json 명시. 가장 안전 |
| agent-browser | Apache-2.0 | dependency 확인만 |
| Stagehand | MIT | 매우 낮음 |
| Browser Use | MIT | dependency 확인 |
| Steel | Apache-2.0 | 매우 낮음 |
| UI-TARS / Agent TARS | Apache-2.0 | **model license 별도 확인** |
| Vitest / Testing Library | MIT | 안전 |

## 주의군 (구조 검토 필수)

| 프로젝트 | License | 주의 |
|---|---|---|
| BrowserOS | AGPL-3.0 | 수정·배포시 소스공개 의무. SaaS/내부사용 구조에 따라 검토 |
| Skyvern | AGPL-3.0 | core AGPL + **cloud-only(anti-bot 등)** 존재. 기능 분기 확인 |
| BrowserGym/벤치 데이터 | OSS이나 dataset·env 조건 상이 | benchmark contents 라이선스 별도 확인 |
| 외부 VLM API | 각 제공자 약관 | GPT-4V/Claude 등 API 약관 준수. 비용·데이터 전송 고지 |

## 제외 (기준점 용도)

- **Aside**: Commercial, non-transferable. 도입 제외, 비교 기준점으로만 인용.

## 체크리스트
- [ ] Apache/MIT: 출처 명시로 충분한지 확인
- [ ] AGPL: 수정 배포 계획 있으면 법무/구조 검토
- [ ] 모델: 코드 Apache라도 가중치 라이선스 별도인지 확인
- [ ] 벤치: 인용 결과가 자체보고인지 독립평가인지 표기
