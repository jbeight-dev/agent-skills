# Editorial Slide Deck — Design System

`assets/slide-template.html`이 이 문서의 구현체다. 둘이 어긋나면 이 문서를 기준으로 템플릿을 고친다.

## 1. 스타일 키워드

- 에디토리얼 미니멀: 잡지 지면처럼 큰 제목, 넓은 여백, 얇은 구분선
- 장식 최소화: 그림자·그라디언트·아이콘 남용 금지
- 포인트 컬러는 한 슬라이드에 1~2곳만 (키워드, 번호, 핵심 수치)
- 정보 밀도보다 가독성 우선: 한 슬라이드 = 한 메시지

## 2. 폰트

| 용도 | 폰트 | 대체 |
|---|---|---|
| 본문·제목 | `Noto Sans KR` (Google Fonts) | `Apple SD Gothic Neo`, `Malgun Gothic`, `sans-serif` |
| 코드·라벨 | `JetBrains Mono` (Google Fonts) | `SFMono-Regular`, `Menlo`, `Consolas`, `monospace` |

Google Fonts는 외부 요청이다. 오프라인이 필요하면 `<link>`를 지우면 대체 폰트로 렌더링된다.

## 3. 색상 토큰

다크가 기본, 라이트는 `[data-theme="light"]`로 전환한다. 색은 반드시 토큰으로만 쓴다.

```css
:root {
  --bg: #111110;        /* 캔버스 배경 */
  --surface: #1a1a18;   /* 카드, 코드 블록 */
  --line: #2c2c29;      /* 구분선, 테두리 */
  --text: #ededea;      /* 본문 */
  --muted: #9a9a93;     /* 보조 텍스트, 캡션 */
  --accent: #ff5a1f;    /* 브랜드 포인트 컬러 */
  --accent-soft: rgba(255, 90, 31, .12);
  --warn: #f2b33d;      /* 거버넌스/주의 */
}
[data-theme="light"] {
  --bg: #fafaf7;
  --surface: #f0efea;
  --line: #dcdbd4;
  --text: #161614;
  --muted: #6b6b65;
  --accent: #e04a12;
  --accent-soft: rgba(224, 74, 18, .10);
  --warn: #b7791f;
}
```

`--accent`는 브랜드 컬러 자리다. 브랜드가 바뀌면 이 두 값(다크/라이트)만 교체한다.

## 4. 다크/라이트 테마 규칙

- 기본은 다크. `T` 키 또는 우측 하단 버튼으로 전환, 선택값은 `localStorage`에 저장
- 커버 슬라이드는 테마와 무관하게 항상 다크
- 라이트에서 포인트 컬러는 대비를 위해 한 단계 어둡게 (`--accent` 라이트 값)

## 5. 타이포그래피 스케일 (1024×768 기준)

| 요소 | 크기 / 굵기 | 비고 |
|---|---|---|
| 커버 제목 `.cover h1` | 64px / 800 | 행간 1.15, 자간 -0.02em |
| 슬라이드 제목 `h2` | 40px / 700 | 행간 1.25 |
| 소제목 `h3` | 22px / 700 | |
| 본문 `p, li` | 20px / 400 | 행간 1.6 |
| 캡션 `.muted` | 16px / 400 | |
| 라벨 `.eyebrow`, `.tag` | 13px / 600 mono | 대문자, 자간 0.08em |
| 코드 | 15px mono | 행간 1.55 |

본문은 20px 아래로 내리지 않는다. 내용이 넘치면 슬라이드를 나눈다.

## 6. 거버넌스 메시지 `.callout`

규칙·금지사항·보안 주의처럼 반드시 지켜야 할 내용에 사용한다.

- 왼쪽 3px `--warn` 세로선 + `--surface` 배경
- 첫 줄에 굵은 라벨 (`원칙`, `주의`, `금지`)
- 슬라이드당 최대 1개

## 7. 컴포넌트

- **카드 `.card`**: `--surface` 배경, 1px `--line` 테두리, 라운드 10px, 패딩 24px. `.grid-2`/`.grid-3` 안에 배치
- **태그 `.tag`**: mono 라벨, `--accent-soft` 배경 + `--accent` 글자. 상태·분류 표시용
- **예시 값 `.ex`**: 사용자가 바꿔야 하는 값은 `<span class="ex">my-project</span>`로 감싸 점선 밑줄로 구분
- **코드 블록 `pre > code`**: `--surface` 배경, 우측 상단 `복사` 버튼 자동 삽입. 한 블록 12줄 이내
- **표 `table`**: 세로선 없음, 헤더 아래 2px `--text` 선, 행 사이 1px `--line` 선
- **흐름도 `.flow`**: 가로로 놓인 단계 박스 + `→` 화살표. 4단계 이내, 넘으면 두 슬라이드로 분리
- **STEP 라벨 `.eyebrow`**: 제목 위 `STEP 01` 형식, `--accent` 색
- **커버 `.slide.cover`**: 항상 다크, 하단 좌측 정렬 제목, 상단에 소속/날짜 mono 라벨, 포인트 컬러 가로 바 1개

## 8. 슬라이드 전환

- 전환: opacity 0→1 + translateY 12px→0, 350ms `cubic-bezier(.2,.7,.2,1)`
- `prefers-reduced-motion`이면 전환 없음
- 상단 2px 진행 바 (`--accent`), 우측 하단 `03 / 12` 페이지 번호

## 9. 내비게이션

| 입력 | 동작 |
|---|---|
| `→` `Space` `PageDown` / 왼쪽 스와이프 | 다음 |
| `←` `PageUp` / 오른쪽 스와이프 | 이전 |
| `Home` / `End` | 처음 / 끝 |
| `F` | 전체화면 |
| `T` | 테마 전환 |
| URL `#5` | 5번 슬라이드로 이동 (새로고침 유지) |
