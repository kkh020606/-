

```markdown
# [TRD] 광안리 모던 감성 카페 랜딩페이지 기술 요구사항 정의서

## 1. 기술 스택 (Tech Stack)
* **Frontend:** HTML5, CSS3, Vanilla JavaScript (ES6+)
* **CSS Framework:** Tailwind CSS (CDN 방식 활용)

---

## 2. 프로젝트 구조 (Project Structure)
본 프로젝트는 단일 랜딩페이지로, 가볍고 빠른 로딩을 위해 아래와 같이 최소한의 구조로 관리합니다.

```

project/
├── index.html       # 메인 마크업 및 Tailwind CDN 포함
└── assets/          # 이미지 및 그래픽 리소스 관리
├── hero.jpg     # 메인 배너 이미지
└── gallery/     # 갤러리에 사용될 감성 사진들

```

---

## 3. UI 및 레이아웃 구현 명세

### 3.1. 전역 스타일 및 반응형 대응 (Tailwind CSS)
* **모바일 퍼스트:** 기본 속성은 모바일 화면에 맞추고, `md:` 및 `lg:` 접두사를 사용하여 태블릿 및 데스크톱 스케일링 대응.
* **설정 색상 (Custom Color 구성 체계):**
  * 배경 및 여백: `bg-[#FDFBF7]` (Warm Ivory)
  * 주 텍스트 및 포인트: `text-[#002F6C]` (Deep Blue)

### 3.2. 섹션별 마크업 구현 방안
1. **Hero Section:**
   * `h-screen`, `w-full` 레이아웃으로 브라우저 화면 전체를 점유.
   * `flex items-center justify-center` 구도를 사용하여 슬로건 정중앙 배치.
2. **About Section:**
   * 넓은 패딩(`py-24 px-6`)과 큰 여백을 주어 미니멀 매거진 룩 완성.
3. **Gallery Section (비정형 격자 레이아웃):**
   * Tailwind의 CSS Grid 활용: `grid grid-cols-2 gap-4` 기반.
   * 각 이미지 요소에 `row-span-2`, `col-span-1` 등을 비대칭적으로 부여하여 핀터레스트 스타일 구현.
   * 모바일(2열)에서 필요시 데스크톱(3~4열)으로 확장되도록 구현.

---

## 4. 인터랙션 및 애니메이션 명세 (JavaScript & CSS)

### 4.1. 메인 배너 은은한 줌 인 (Pure CSS Animation)
* 외부 스크립트 없이 Tailwind의 커스텀 키프레임 또는 인라인 CSS `@keyframes`로 구현.
* `scale(1.0)`에서 `scale(1.05)`로 대략 10~15초에 걸쳐 아주 천천히 확대되는 루프 애니메이션 적용하여 정적인 화면에 생동감 부여.

### 4.2. 격자 갤러리 마우스 호버 효과 (Tailwind Utilities)
* 갤러리 내 각 이미지 아이템에 다음 클래스 조합을 적용하여 부드러운 반응 효과 구현.
  * `transition-all duration-700 ease-out-expo`
  * `hover:scale-103 hover:shadow-lg`
* 이미지 컨테이너에 `overflow-hidden`을 적용하여 격자 틀 안에서만 부드럽게 확대되도록 제어.

### 4.3. 스크롤 스르륵 등장 효과 (Intersection Observer API)
* 모바일 환경의 메모리 최적화를 위해 무거운 라이브러리를 배제하고 브라우저 내장 API 활용.
* JS로 화면에 진입하는 섹션 요소를 감지하여 Tailwind의 투명도 및 위치 클래스 제어.
  * 진입 전: `opacity-0 translate-y-8 transition-all duration-1000`
  * 진입 후: `opacity-100 translate-y-0` 클래스 부여.

---

## 5. 성능 최적화 및 주의사항 (Performance)
* **이미지 최적화:** 비주얼 중심 페이지이자 모바일 퍼스트인 만큼, 모든 사진 리소스는 `.webp` 포맷으로 변환하고 적정 용량(배너 300KB 이하, 갤러리 100KB 이하)으로 압축하여 초기 로딩 속도 방어.
* **CDN 캐싱:** Tailwind CSS 최신 안정화 버전의 CDN 링크를 활용하여 브라우저 캐싱 이점 극대화.

```
