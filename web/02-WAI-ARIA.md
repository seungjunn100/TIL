# 웹접근성을 위한 WAI-ARIA

- [WAI-ARIA](#wai-aria)
  - [유저 에이전트와 접근성 API 및 보조 기술 간의 관계](#유저-에이전트와-접근성-api-및-보조-기술-간의-관계)
- [WAI-ARIA의 세 가지 구성 요소](#wai-aria의-세-가지-구성-요소)
- [WAI-ARIA 작성 규칙](#wai-aria-작성-규칙)




<br />
<br />




## WAI-ARIA

**WAI-ARIA(Web Accessibility Initiative - Accessible Rich Internet Applications)는 웹 콘텐츠의 접근성을 높이기 위해 W3C WAI에서 개발한 기술**이다. 웹이 단순한 문서 연결을 넘어 복잡한 사용자 경험(UX)을 제공하는 리치 인터넷 애플리케이션(RIA) 시대로 발전하면서 등장했다.

초기 웹은 정적이었으나, JavaScript와 Ajax 같은 기술로 웹 페이지가 동적으로 변하고 다양한 UI 컴포넌트가 등장하면서 기존 HTML만으로는 그 의미를 보조 기술(스크린 리더 등)에 정확히 전달하기 어려워졌다. 예를 들어, `<div>`나 `<span>` 태그로 만든 컴포넌트의 기능과 상태를 보조 기술이 파악할 수 없는 문제가 발생했다.

**WAI-ARIA**는 이러한 문제를 해결하기 위해 **역할(Role)**, **속성(Property)**, **상태(State)** 정보를 마크업에 추가하여 웹의 동적인 콘텐츠와 복잡한 UI를 보조 기술이 인식하고 올바르게 전달할 수 있도록 돕는 역할을 한다.

<br />

### 유저 에이전트와 접근성 API 및 보조 기술 간의 관계

**WAI-ARIA**는 **유저 에이전트(웹 브라우저)와 보조 기술 사이의 커뮤니케이션을 중재**하는 핵심적인 역할을 수행한다.

1. **DOM에 ARIA 속성 추가**

   개발자는 HTML 요소에 `role`, `property`, `state`와 같은 ARIA 속성을 추가한다.

2. **유저 에이전트의 역할**

   웹 브라우저는 HTML 문서와 ARIA 속성을 해석하여 **접근성 트리(Accessibility Tree)를 생성**한다. 이 접근성 트리는 **웹 콘텐츠의 구조, 역할, 상태에 대한 정보**를 담고 있다.

3. **접근성 API의 역할**

   웹 브라우저는 운영체제(OS)에서 제공하는 접근성 API를 통해 이 접근성 트리를 노출한다.

4. **보조 기술의 역할**

   스크린 리더와 같은 보조 기술은 접근성 API를 통해 접근성 트리의 정보를 읽어 들인다. 이 정보를 바탕으로 사용자에게 웹 콘텐츠를 전달하며 웹 페이지를 탐색하고 상호작용할 수 있도록 돕는다.




<br />
<br />




## WAI-ARIA의 세 가지 구성 요소

- **역할(Role)**

  요소의 **역할**을 정의한다. 이는 해당 요소가 어떤 종류의 UI 컴포넌트인지 또는 페이지의 어느 영역인지 나타낸다.

  - `role="button"`은 해당 요소가 버튼 기능을 수행
  - `role="navigation"`은 내비게이션 영역

- **속성(Property)**

  요소의 **특성**을 정의한다. 이는 콘텐츠의 상태나 특성을 보조 기술에 전달하는데 사용된다.

  - `aria-label="메뉴 열기"`는 해당 요소에 대한 설명 텍스트 제공
  - `aria-required="true"`는 해당 요소가 필수 항목임을 알수 있도록 제공

- **상태(State)**

  요소의 **현재 상태**를 나타낸다. 속성과 유사하지만 상태는 사용자의 상호작용에 따라 동적으로 변하는 값이다.

  - `aria-expanded="true"`는 확장 가능한 영역이 현재 펼쳐져 있음
  - `aria-checked="true"`는 체크박스가 선택되어 있음




<br />
<br />




## WAI-ARIA 작성 규칙

- **HTML의 시맨틱 요소 사용**

  시맨틱 요소들은 기본적으로 의미와 기능을 제공할 수 있어 접근성을 가지고 있다. 굳이 ARIA를 사용할 필요가 없다.

  - `<header>` = `role="banner"`
  - `<nav>` = `role="navigation"`
  - `<button>` = `role="button"`

  ```HTML
  <span role="button" tabindex="0">버튼</span>
  ```

  ```Javascript
  // role="button"
  var roleButton = document.querySelector('[role="button"]');

  // keyup 이벤트 핸들러 함수
  function keyUpHandler(event) {
    if (event.key === 'Enter' || event.key == 'Space' || event.key == 'Spacebar' ||event.keyCode === 13 || event.keyCode === 32) {
    // Enter 키 또는 Spacebar 키가 눌렸을 때 실행할 작업
    }
  }

  // role="button"으로 지정된 요소에 keyup 이벤트 리스너 추가
  roleButton.addEventListener('keyup', keyUpHandler);
  ```

  `<button>` 요소를 사용했다면, 위와 같은 불필요한 스크립트를 작성할 필요가 없게된다.

- **HTML 요소의 기능 변경 제한**

  모든 HTMl 요소에 ARIA 속성을 추가하거나 기존의 의미를 변강하는건 좋지 않다.

  ```HTML
  <!-- 이미지 이면서 버튼 역할을 할 수 없다. -->
  <img src="./src/images/photo.jpg" alt="photo" role="button" />
  ```

  요소의 의미론적 충돌로 인해 보조 기술 사용자들은 혼란스러울 수 있다.

- **키보드 사용 보장**

  사용자와 상호 작용이 필요한 대화형 UI의 경우 키보드로도 접근 및 사용이 가능하도록 제공해야 한다. 기본적으로 키보드로 접근할 수 없는 HTML 요소의 경우 `tabindex=""` 속성을 사용하여 키보드로 접근이 가능하도록 할 수 있다.

  ```HTML
  <!-- 키보드로 접근 가능 -->
  <span role="button" tabindex="0">버튼</span>

  <!-- 키보드로 접근 불가능 -->
  <span role="button" tabindex="-1">버튼</span>
  ```

- **숨김 콘텐츠**

  ARIA를 사용하거나 CSS를 사용해서 숨김 처리를 하면 접근성이 차단될 수 있다.

  - `display: none` 또는 `visibility: hidden` 스타일 속성을 사용하면, 보조 기술뿐만 아니라 모든 사용자에게서 숨겨진다.
  - `aria-hidden="true"`, `role="presentation"`, `role="none"`는 사용자에게 보여지지만 보조 기술에 노출되지 않도록 한다.
    - `aria-hidden="true"` : 요소의 시맨틱 의미를 제거
    - `role="presentation"/"none"` : 요소 자체와 자식 전부 숨김

- **모든 상호작용 요소에 접근 가능한 이름을 부여**

  상호작용 가능한 모든 요소는 접근 가능한 이름을 가져야 한다.

  ```HTML
  <!-- 레이블 요소를 사용한 경우 -->
  <div class="container">
    <label for="user-name">이름</label>
    <input type="text" id="user-name" />
  </div>

  <!-- aria-label, aria-labelledby 속성을 사용한 경우 -->
  <div>
    <div id="user-name">이름</div>
    <input type="text" aria-labelledby="user-name" />
  </div>

  <button type="button" aria-label="닫기"> X </button>
  ```
- [더 다양한 WAI-ARIA 작성 방법](https://mulder21c.github.io/aria-practices/)