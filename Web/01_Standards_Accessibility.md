# 웹 표준 & 웹 접근성
- 웹 표준은 기술적인 규칙이고, 웹 접근성은 사용자 중심의 배려에 가깝다. 하지만 둘은 함께 구현될 때 가장 큰 효과를 낸다. ⭐️⭐️⭐️


<br />
<br />


## 웹 표준 ( Web Standards )
- 다양한 웹 브라우저와 기기에서도 동일한 결과를 보여주기 위한 공통의 기술 규칙 및 규약이다.

- 웹 기술의 호환성, 접근성, 유지보수성을 높이기 위한 기본 원칙이다.

- 주로 W3C와 WHATWG가 웹 표준을 정의한다.

<br>

### 웹 표준이 중요한 이유
- 브라우저 호환성 확보
  - 크롬, 엣지, 사파리 등 다양한 브라우저에서도 깨지지 않고 일관된 UI를 제공 할 수 있다.

- 접근성 향상
  - 스크린 리더, 키보드 탐색 등도 고려한 코드 작성이 가능하다.

- 유지보수성 & 확장성
  - HTML과 CSS가 분리되어 유지보수에 용이하다.
  - 구조화된 마크업은 협업과 리팩터링에도 용이하다.
  - 논리적이고 효율적으로 작성된 웹 문서는 코드의 양이 줄어 파일 크기가 줄고 서버 부담의 감소로 이어진다.

- SEO (검색엔진 최적화)
  - 구조화된 시멘틱 태그 사용이 검색 엔진에 긍정적 영향을 준다.

- 미래 기술 대응력
  - 최신 기술과의 호환성을 보장받기 쉽다.


<br />
<br />


## 웹 접근성 ( Web Accessibility )
-  모든 사람이 웹사이트나 웹 애플리케이션에 접근하고, 이해하고, 탐색하며, 상호작용할 수 있도록 보장하는 원칙과 실천을 말한다.

- 웹 표준과 마찬가지로 W3C에서 정한 WCAG는 웹 접근성을 개선하기 위한 국제 표준 가이드라인이다.

<br>

### 웹 접근성이 중요한 이유
- 모두를 위한 포용성
  - 시각 장애인, 색각 이상자, 노인, 일시적 장애를 가진 사용자, 느린 인터넷 환경, 다양한 디바이스 환경의 사용자 등 모든 사람이 웹을 사용할 수 있어야 한다.
  - 모두가 동등하게 정보에 접근할 권리를 가지도록 보장해야 한다.

- 법적 요구사항
  - 미국의 ADA법, 한국의 장애인차별금지법, 공공기관의 KWCAG 준수 의무 등 웹접근성은 많은 나라에서 법적으로 요구되고 있다.
  - 웹접근성이 미흡할 경우, 법적 제재나 벌금을 받을 수 있다.

- 사용자 수 확대
  - 웹접근성을 지키면 더 많은 사용자가 웹을 사용할 수 있어 시장 확대로 이어진다.
  - 검색엔진 최적화(SEO)에도 긍정적인 효과가 있어 유입 증가에도 기여한다.
    - 접근성 좋은 웹은 사용자 만족도가 높고, 구글 크롤러가 잘 읽기 때문에 SEO 측면에서도 이득이다.


<br />
<br />


## 웹 표준과 웹 접근성을 준수하는 방법
- DOCTYPE 선언 필수
  - 표준모드로 렌더링할 수 있게 해준다.
  ```html
  <!DOCTYPE html>
  ```

- 시맨틱 태그 사용
  - 의미론적인 태그들을 사용하면 SEO, 접근성, 코드의 유지보수성 & 확장성 등에 좋아진다.
  - `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>` 등

- 적절한 제목 구조 사용
  - 제목 태그는 논리적인 계층 구조로 사용해야 한다.
  - 문서에 `<h1>`은 보통 한 번만 사용하고, 그다음 내용을 `<h2>`, `<h3>`, ..., `<h6>`로 정리한다.

- 이미지 alt 속성 필수
  - 시각장애인을 위한 스크린 리더가 내용을 읽을 수 있도록 설명을 제공한다.
  - 장식용 이미지라면 alt=""으로 비워두는 것도 표준이다.
  ```html
  <img src="profile.jpg" alt="프로필 사진">
  <img src="decoration.jpg" alt="">
  ```

- form 요소에는 label 연결하기
  - label은 시각적 또는 기술적으로 입력 필드와 연결되어야 한다.
  ```html
  <label for="email">이메일</label>
  <input type="email" id="email" name="email">
  ```

- 중첩 구조 준수
  - HTML 요소는 정해진 올바른 위치에 사용해야 한다.
  ```html
  <!-- 잘못된 예: <p> 안에 <div> -->
  <p>
    잘못된 예
    <div>잘못된 예</div>
  </p>

  <!-- 올바른 예 -->
  <div>
    <p>올바른 구조입니다.</p>
  </div>
  ```

- 의미 없는 태그 남용 지양
  - `<div>`나 `<span>`은 의미가 없는 비시맨틱 태그로, 꼭 필요할 때만 사용하는게 좋다.

- 웹 접근성 고려한 속성 사용
  - `lang`, `role`, `aria-*` 속성
  ```html
  <html lang="ko">

  <a href="#" role="button" aria-label="모달창 열기">+</a>
  ```

- 문법 오류 없는 깔끔한 코드
  - 태그를 닫지 않거나, 속성 따옴표 누락, 중복 id 사용 등은 표준을 위반하는 것이다.
  ```html
  <!-- 비표준 -->
  <input type=text name=email>

  <!-- 표준 -->
  <input type="text" name="email">
  ```

- W3C 유효성 검사 통과하기
  - 작성한 HTML이 웹 표준에 맞게 작성되었는지 검사할 수 있다.
  - <a href="https://validator.w3.org/" target="_blank">W3C Validator</a>

- 스타일과 구조 분리
  - HTML에 인라인 스타일 사용 ❌
  - 스타일은 CSS에만 작성하고, 구조는 HTML에만 작성하는 게 웹 표준 방식이다.

- CSS 선택자는 의미 있고 명확하게 작성
  - 클래스명은 의미 있는 단어로 작성하고, 너무 복잡한 선택자 지양하는 것이 좋다.
  - 불필요한 중첩은 피하고 재사용 가능한 선택자를 만드는 것이 좋다.
  ```css
  /* 안 좋은 예 (너무 구체적) */
  div#header ul.menu li.item a.link {}

  /* 좋은 예 */
  .menu-link {}
  ```

- 레이아웃은 최신 표준 방식 사용
  - 예전의 `float`, `position: absolute` 남용 대신 `Flexbox`, `Grid` 활용하는 것이 좋다.
  - 최신 레이아웃 방식은 더 깔끔하고 반응형에도 유리하다.

- 접근성 고려한 스타일링
  - 포커스 표시 제거하지 말기 (또는 대체 스타일 제공)
  ```css
  /* 포커스 제거는 접근성 문제 */
  button:focus {
    outline: none;
  }

  /* 대체 포커스 스타일 제공 */
  button:focus {
    outline: 2px solid blue;
  }
  ```

- 단위 일관성 유지
  - `px`, `rem`, `%`, `vw` 등 혼용 주의
  - `rem`, `%`를 주로 사용하면 반응형에 유리하고 유지보수 용이하다.

- 미디어 쿼리로 반응형 웹 구현
  - 반응형 웹은 이제 기본이며, 표준 기반으로 다양한 디바이스에 대응해야 한다.

- 시각적 효과는 CSS로 처리 (JS 남용 ❌)
  - `hover`, `animation`, `transition` 등은 JS가 아닌 CSS에서 처리하는 게 웹 표준을 준수하는 방법이다.

- 속성 축약 사용으로 코드 간결하게
  ```css
  /* 긴 코드 ❌ */
  margin-top: 10px;
  margin-right: 20px;
  margin-bottom: 10px;
  margin-left: 20px;

  /* 축약형 ✅ */
  margin: 10px 20px;
  ```

- 브라우저 호환성 고려
  - CSS 속성을 사용할 때는 해당 속성이 주요 브라우저에서 지원되는지 확인할 수 있다.
  - <a href="https://caniuse.com/" target="_blank">Can I use</a>

- W3C 유효성 검사 통과하기
  - 작성한 CSS가 웹 표준에 맞게 작성되었는지 검사할 수 있다.
  - <a href="https://jigsaw.w3.org/css-validator/" target="_blank">W3C CSS Validator</a>

- 표준 DOM API 사용하기
  - 웹 표준에 맞는 DOM 접근 방식을 사용하는 게 기본이다.
  - `addEventListener`는 이벤트를 여러 개 등록할 수 있어서 더 유연하고, 최신 브라우저에서도 일관되게 작동한다.
  ```javascript
  // 권장 (표준 DOM 방식)
  const button = document.querySelector('#submitBtn');
  button.addEventListener('click', handleClick);

  // 비권장 (구식 방식)
  const button = document.getElementById('submitBtn');
  button.onclick = handleClick;
  ```

- 인라인 이벤트 핸들러 피하기
  - HTML 구조와 JavaScript 동작을 분리하면 유지보수와 접근성이 좋아진다.
  ```html
  <!-- 비권장 -->
  <button onclick="submitForm()">제출</button>

  <!-- 권장 -->
  <button id="submitBtn">제출</button>
  ```
  ```javascript
  document.querySelector('#submitBtn').addEventListener('click', submitForm);
  ```

- HTML 요소 조작 시 시멘틱 구조 유지하기
  - JavaScript로 동적으로 DOM을 만들거나 조작할 때도 시맨틱 태그와 올바른 구조를 고려해야 한다.
  ```javascript
  const section = document.createElement('section');
  section.innerHTML = `
    <h2>공지사항</h2>
    <p>2025년 업데이트 예정입니다.</p>
  `;
  document.body.appendChild(section);
  ```

- 접근성 고려
  - 동적으로 요소를 추가할 때, 스크린 리더 사용자도 사용할 수 있게 고려하는 것이 중요하다.
  - `role="alert"`은 즉시 사용자에게 메시지를 읽어준다.
  ```javascript
  const alert = document.createElement('div');
  alert.setAttribute('role', 'alert');
  alert.setAttribute('aria-live', 'assertive');
  alert.textContent = '저장이 완료되었습니다.';
  document.body.appendChild(alert);
  ```

- 모던 자바스크립트 문법 사용 (ES6+)
  - 최신 문법은 표준이자 협업에 적합한 방식이다.
  ```javascript
  // ES6 방식
  const items = ['사과', '바나나', '체리'];
  items.forEach(item => console.log(item));

  // 구식 방식
  var items = ['사과', '바나나', '체리'];
  for (var i = 0; i < items.length; i++) {
    console.log(items[i]);
  }
  ```

- `<script>` 렌더링 지연 방지
  - `<script>`는 `<body>` 하단에 배치하거나 `defer` 속성을 사용하는 것이 좋다.
  - 페이지 로딩 속도 개선, DOM이 완전히 준비된 후 `<script>`가 실행된다.
  ```html
  <body>
    <!-- ... 페이지 내용 ... -->

    <script src="js/ui.js"></script>
  </body>
  ```
  ```html
  <!DOCTYPE html>
  <html lang="ko">
  <head>
      <!-- ... 다른 head 요소들 ... -->
      <script defer src="js/ui.js"></script>
  </head>
  <body>
      <!-- ... 페이지 내용 ... -->
  </body>
  </html>
  ```

- 에러 처리로 사용자 경험 향상
  - 예외 처리는 사용자에게 문제가 생겼는지 알릴 수 있다.
  ```javascript
  try {
    const data = JSON.parse(responseText);
    console.log(data);
  } catch (error) {
    console.error('JSON 파싱 에러:', error.message);
  }
  ```

- 포커스 이동과 키보드 접근성 고려
  - 키보드만 사용하는 사용자도 주요 기능에 접근할 수 있도록 해야한다.
  ```javascript
  const dialog = document.querySelector('#myDialog');

  // 키보드 사용자에게 접근성 제공
  dialog.focus();

  // 포커스 가능한 요소가 없다면 tabindex 추가
  dialog.setAttribute('tabindex', '-1');
  ```

- 코드 품질 검사 도구 사용
  - JS 문법과 표준을 검사하는 도구
  - <a href="https://eslint.org/" target="_blank">ESLint</a>


<br />
<br />


## 참고 사이트
- <a href="https://www.w3.org/" target="_blank">W3C</a>
- <a href="https://a11y.gitbook.io/wcag/international-standards" target="_blank">WCAG</a>
- <a href="https://developer.mozilla.org/" target="_blank">MDN Web Docs</a>
- <a href="https://whatwg.org/" target="_blank">WHATWG</a>
- <a href="https://nuli.navercorp.com/education" target="_blank">NULI - 접근성 교육</a>
- <a href="https://www.wa.or.kr/m1/sub3.asp" target="_blank">한국웹접근성인증평가원 - 심사 기준</a>