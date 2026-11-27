# Karrot UI Clone — 프로젝트 규칙

당근 모바일 앱 UI를 **순수 HTML5 + CSS3만으로** 재현하는 학습용 클론이다.
당근(Daangn)과 무관한 비공식·비상업 프로젝트이며, 당근 로고 원본 파일은 쓰지 않는다(당근 심볼은 직접 그린 SVG).

## 1. 절대 규칙 (금지 사항)

| 금지 | 이유 / 대안 |
| --- | --- |
| `<script>`, `on*=""` 인라인 핸들러, `javascript:` URL | Zero-JS가 이 프로젝트의 정체성. 상태는 `:checked` + `:has()`로 표현 |
| 외부 이미지 URL (`http(s)://…png/jpg`) | 깨지면 감점. 썸네일은 `assets/` 로컬 SVG, 아이콘은 인라인 `<symbol>` 스프라이트 |
| CSS 프레임워크·라이브러리 | 외부 리소스는 Pretendard 웹폰트 CDN 하나만 허용 |
| 컴포넌트 CSS에 raw hex 하드코딩 | 반드시 `tokens.css`의 **역할 토큰**(`--bg-*`, `--fg-*`, `--stroke-*`)을 쓴다. 예외: SVG 일러스트 내부 |
| 브랜드 주황을 넓게 칠하기 | SEED 지침: "Brand 컬러는 꼭 필요한 곳에만" → CTA·FAB·활성 탭·읽지 않음 뱃지·찜 하트에만 쓴다. 필터 칩 선택은 neutral-inverted |
| 마지막 항목 뒤 Divider | SEED 지침. 리스트는 `clip-path: inset(0 0 1px 0)`로 마지막 구분선을 잘라낸다(필터로 숨겨진 항목이 있어도 동작) |
| Badge를 클릭 요소로 사용 | SEED 지침. 뱃지는 항상 `<span>` |
| 임의의 그림자 값 | `--shadow-s1~s3` 세 단계만 쓴다 (FAB의 브랜드 글로우는 `--shadow-brand` 토큰으로 정의) |

## 2. 디자인 토큰 출처와 결정

토큰의 기준은 **SEED Design** (당근 디자인 시스템, Apache-2.0)이다. 과제 프롬프트에 적힌 값과 SEED 공식값이 다를 때는 SEED를 따랐다.

| 항목 | 프롬프트 지정값 | 채택값 (SEED) | 토큰 |
| --- | --- | --- | --- |
| Brand | `#FF6F0F` | `#FF6600` carrot-600 | `--bg-brand-solid` |
| Brand Hover/Pressed | `#E65F00` | `#E14D00` carrot-700 | `--bg-brand-solid-pressed` |
| Soft Orange | `#FFF3EB` | `#FFF2EC` carrot-100 | `--bg-brand-weak` |
| 텍스트 주 | `#212124` | `#1A1C20` gray-1000 | `--fg-neutral` |
| 텍스트 보조 | `#4D5159` | `#555D6D` gray-800 | `--fg-neutral-muted` |
| 메타/비활성 | `#868B94` | `#868B94` gray-700 | `--fg-neutral-subtle` |
| 구분선 | `#EAEBEE` | `#0000000C` static-black-alpha-200 | `--stroke-neutral-subtle` |
| 서브 배경 | `#F2F3F6` | `#F3F4F5` gray-200 | `--bg-layer-basement` |
| 폰트 | Pretendard | Pretendard → 시스템 폰트 fallback | `--font-sans` |

프롬프트의 별칭 이름(`--color-brand`, `--color-text-primary` …)도 `tokens.css` 하단에 SEED 역할 토큰을 가리키는 alias로 남겨 두었다.

- 반경: 카드 썸네일 `--r2`(8px), 뱃지 `--r1`(4px), FAB·칩·CTA `--r-full`
- 간격: SEED `x` 사다리 (`--x1` = 4px, `--x4` = 16px 화면 거터)
- 모션: 마이크로 ≤ 200ms(`--dur-d3` 150ms), 매크로 > 200ms(`--dur-d6` 300ms), 눌림 배율 `--scale-95/97/98`
- 가격·카운트 숫자는 `font-variant-numeric: tabular-nums`, 전역 `letter-spacing: -0.02em`

## 3. 파일 구조

```
CLAUDE.md
index.html          홈 피드(중고거래)
detail.html         상품 상세 (홈 첫 번째 매물)
chat.html           채팅 목록
neighborhood.html   동네생활
css/tokens.css      색(팔레트+역할)·간격·반경·타이포·그림자·모션·z-index
css/reset.css       리셋, 터치 하이라이트 제거, 스크롤바, sr-only, focus ring
css/shell.css       반응형 쉘: 모바일 풀스크린 / 데스크톱 iPhone 프레임 + 안내 카드
css/components.css  재사용 컴포넌트 (헤더, 탭바, 카드, 뱃지, 버튼, 바텀시트 …)
css/pages.css       페이지별 레이아웃과 CSS 상태 규칙(필터 등)
assets/products/    매물 썸네일 SVG
assets/posts/       동네생활 첨부 이미지 SVG
assets/favicon.svg  직접 그린 당근 심볼
```

## 4. 네이밍 규칙 — BEM

- `block`, `block__element`, `block--modifier` (예: `card__thumb`, `badge--reserved`)
- 상태는 `is-*` 클래스가 아니라 **실제 폼 상태**로 표현한다 (`:checked`, `:has()`, `[open]`)
- 상태용 input은 `.sr-only`로 시각적으로만 숨긴다 (`display:none` 금지 → 키보드 접근 유지)
- 필터 대상은 `data-tags="pop digital"` 처럼 공백 구분 토큰 + `[data-tags~="…"]` 선택자

## 5. 순수 CSS 상태 패턴

| 패턴 | 마크업 | 선택자 |
| --- | --- | --- |
| 토글(팝오버·FAB) | `<label><input type="checkbox" class="sr-only x-toggle">…</label>` + 바깥의 `<label for>` 백드롭 | `.app:has(.x-toggle:checked) …` |
| 단일 선택(칩 필터) | `<label class="chip"><input type="radio" name="filter" value="pop">` | `.chip:has(:checked)`, `.app:has([name=filter][value=pop]:checked) .card:not([data-tags~=pop])` |
| 일회성 피드백(토스트) | `<input id="toast-x" class="toast-trigger">` 바로 뒤 `.toast` | `.toast-trigger:checked + .toast` |
| 시트 | `input.sheet-trigger + label.backdrop + .sheet` | `:checked + .backdrop + .sheet` |
| 스크롤 연동 | `scroll-timeline` + `animation-timeline` (`@supports`로 점진적 향상) | 상세 헤더 배경, 캐러셀 인디케이터 |

## 6. 완료 전 체크리스트

- [ ] `grep -nE "<script|\son[a-z]+=|javascript:"` 결과 0건
- [ ] 4개 페이지 상대경로 링크 전부 존재하는 파일을 가리킴
- [ ] 긴 제목은 `-webkit-line-clamp: 2`, 한 줄 메타는 `text-overflow: ellipsis`
- [ ] 모든 눌리는 요소에 `:hover`(hover 가능한 기기만) + `:active`(scale 또는 배경) 피드백
- [ ] 390px / 1440px에서 문서 가로 스크롤 없음 (가로 스크롤은 칩·캐러셀 내부에서만)
