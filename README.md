# Karrot UI Clone — Pure HTML & CSS

당근 모바일 앱 UI를 **JavaScript 없이 순수 HTML5 + CSS3만으로** 재현한 학습용 클론입니다.

> 학습용 비공식 프로젝트입니다. 당근(Daangn)과 무관하며 상업적으로 사용하지 않습니다.
> 색·간격·반경 토큰은 SEED Design(Apache-2.0)을 참고했고, 로고·이미지는 모두 직접 그린 SVG입니다.

## 실행

`index.html`을 브라우저로 열면 됩니다. 빌드나 설치가 필요 없습니다.

- 모바일(≤480px): 네이티브 앱처럼 전체 화면
- 데스크톱: 가운데 iPhone 프레임(390×844) + 왼쪽 프로젝트 안내 카드

## 화면

| 파일 | 화면 | 주요 인터랙션 |
| --- | --- | --- |
| `index.html` | 홈 피드 | 동네 선택 팝오버, 카테고리 필터 칩, 글쓰기 퀵 메뉴 |
| `detail.html` | 상품 상세 | scroll-snap 캐러셀, 스크롤 연동 헤더, 매너온도, 찜 하트 팝 |
| `chat.html` | 채팅 목록 | 판매/구매/안 읽음 필터, 닫히는 배너 |
| `neighborhood.html` | 동네생활 | 주제 필터, 공감 토글 |

## 순수 CSS 기법

`:checked` · `:has()` · radio 필터 · `scroll-snap` · `scroll-timeline` / `animation-timeline` · `<details>` · `@keyframes` · CSS Variables

## 구조

```
css/tokens.css      디자인 토큰 (색·간격·반경·타이포·그림자·모션·z-index)
css/reset.css       리셋, 터치 하이라이트 제거, 스크롤바
css/shell.css       반응형 쉘 (디바이스 프레임)
css/components.css  재사용 컴포넌트 (BEM)
css/pages.css       페이지별 레이아웃과 상태 규칙
assets/             매물·게시글 SVG 일러스트
CLAUDE.md           디자인 규칙과 금지 사항
```
