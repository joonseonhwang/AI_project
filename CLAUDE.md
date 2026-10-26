# CLAUDE.md

메뉴 룰렛 웹앱 "오늘 뭐 먹지". 모든 코드(HTML/CSS/JS)가 `index.html` 한 파일에 있다.

## 원칙
- 빌드 도구, 패키지 매니저, 프레임워크를 추가하지 않는다. 파일 하나로 브라우저에서 바로 열려야 한다.
- 외부 리소스는 Google Fonts뿐이다. 새 라이브러리가 꼭 필요하면 먼저 물어본다.
- UI 문구는 한국어로 쓴다. 코드 식별자와 주석은 영어로 쓴다.

## 코드 규칙
- 색은 `:root`의 CSS 변수로만 정의한다. 다크 모드는 `@media (prefers-color-scheme: dark)`의 `:root:not([data-theme="light"])`와 `:root[data-theme="dark"]` 두 곳에 함께 넣는다.
- 룰렛 캔버스는 `cssVar()`로 CSS 변수를 읽어 그린다. 캔버스에 새 색을 하드코딩하지 말고 변수를 추가한다.
- 상태는 `localStorage` 키 `whattoeat.v1`에 저장된다. 상태 구조를 바꾸면 기존 저장값도 계속 읽히게 하거나 키 버전을 올린다. storage 접근은 항상 try/catch로 감싼다.
- 룰렛이 도는 중(`spinning`)에는 메뉴 목록을 바꾸는 동작을 막는다. 당첨 인덱스가 어긋난다.
- 모바일 우선: 본문 최대 너비 460px, 좌우 여백 16px, 가로 스크롤 없음. `prefers-reduced-motion`을 존중한다.

## 검증
테스트 스위트는 없다. UI를 바꾼 뒤에는 Playwright로 `index.html`을 열어 확인한다.
- 375px 너비에서 라이트/다크 모드 스크린샷을 찍어 깨진 곳이 없는지 본다.
- 룰렛을 돌려 결과와 "최근 결과" 기록이 갱신되는지 확인한다.
- 콘솔 에러가 없어야 한다.

## Git
- 커밋 메시지는 영어 명령형으로 쓴다 (예: `Add dark mode toggle`).
- `main`에 직접 푸시하지 않는다. 브랜치에서 작업하고 PR로 합친다.
- 기능이 바뀌면 `README.md`의 기능 목록도 함께 고친다.
