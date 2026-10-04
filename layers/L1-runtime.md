# L1. Browser / Runtime

> Agent가 올라타는 바닥층. 여기서 직접 자동화하지 않는다.

## 구성 요소

| 요소 | 내용 | 비고 |
|---|---|---|
| Chromium / Chrome | 가장 표준적인 자동화 대상 | Playwright는 Chrome for Testing 사용 |
| Firefox / WebKit | Playwright가 단일 API로 구동 | Cypress는 Chromium 중심 |
| CDP (Chrome DevTools Protocol) | `agent-browser`, Playwright, Steel 모두 이 위에서 동작 | Rust daemon도 CDP 직결 |
| WebDriver | Selenium 계열. 레거시·엔터프라이즈 호환용 | 신규는 CDP 우선 |

## OSS 관점 포인트

- 런타임 자체는 전부 OSS(Chromium/Firefox/WebKit).
- 차별점은 런타임이 아니라 **위 계층이 CDP를 어떻게 추상화하는가**에 있다.
- Xephyr 가상 디스플레이(`DISPLAY=:1`)는 L1 밖에 있는 OS 격리 수단. 레거시 데스크톱 앱까지 제어 범위를 넓힐 때만 사용.

## 선택 가이드

| 상황 | 선택 |
|---|---|
| 크로스 브라우저 필요 | Playwright가 관리하는 Chromium/Firefox/WebKit |
| Chrome 전용·최고 속도 | Chrome for Testing + CDP 직결 (`agent-browser`) |
| 레거시 호환 | WebDriver/Selenium 유지 |
