# CSS 방법론
- `BEM`, `OOCSS`, `SMACSS`

<br />

## BEM (Block, Element, Modifier)
- Class 이름을 지을 때 `Block`, `Element`, `Modifier`로 구분하여 작성한다.

- CSS를 모듈화하고 재사용성을 높이기 위해 고안되었다.

- Class 이름만 보고도 역할과 계층 구조를 쉽게 이해할 수 있음.

- CSS의 충돌을 피할 수 있다.

<br />

### 구조
- `Block` : 재사용 가능한 독립적인 컴포넌트를 나타냅니다.

- `Element` : 블록의 하위 구성 요소를 나타냅니다.

- `Modifier` : 블록이나 요소의 상태나 변형을 나타냅니다.

  ```html
  <!-- Modifier 적용 X -->
  <div class="card">
      <h2 class="card__title">Title</h2>
      <button class="card__button">Click</button>
  </div>
  
  <!-- Modifier 적용 O -->
  <div class="card card--dark">
      <h2 class="card__title">Title</h2>
      <button class="card__button card__button--blue">Click</button>
  </div>
  ```

<br />

### 만약 웹사이트 전반적으로 동일하게 사용하는 Element의 경우❗
- `Element`, `Element--modifier` 형식으로 사용할 수 있다.

  ```html
  <!-- Block 포함 O -->
  <button class="card__button card__button--blue">Click</button>
  
  <!-- Block 포함 X -->
  <button class="button button--blue">Click</button>
  ```


<br />
<br />


## OOCSS (Object-Oriented CSS)
- 객체 지향 프로그래밍의 개념을 적용한 방법론이다.

- 재사용 가능한 코드 작성으로 중복을 최소화할 수 있다.

- 구조와 스킨이 분리되어 수정 시 코드 충돌을 피할 수 있으며 유지보수성 향상에 좋다.

- 공통된 객체를 사용하므로 UI 디자인의 일관성을 유지할 수 있다.

<br />

### 구조와 스킨 분리
- 요소의 레이아웃(구조)과 스킨(시각적 디자인)을 분리한다.
  - 구조 : 레이아웃이나 배치를 설정하는 속성이 포함된다.
    - `width`, `height`, `margin`, `padding`
  - 스킨 : 색상, 배경, 테두리 등 시각적 속성이 포함된다.
    - `color`, `background`, `border`

  ```html
  <div class="card card--primary">
      <h2 class="card__title">Title</h2>
  </div>
  ```
  ```css
  /* 구조 */
  .card { width: 200px; }

  /* 스킨 */
  .card--primary { background-color: blue; }
  .card--secondary { background-color: green; }
  ```

<br />

### 컨테이너와 컨텐츠 분리
- 콘텐츠와 상위 요소(컨테이너)의 스타일 의존성을 최소화한다.

- 이를 통해 컨텐츠가 바뀌더라도 스타일이 깨지지 않도록 할 수 있습니다.

  ```html
  <div class="card">
      <h2 class="card__title">Title</h2>
      <button class="card__button">Click</button>
  </div>
  ```
  ```css
  /* 컨테이너 */
  .card { width: 200px; }
  
  /* 컨텐츠 */
  .card__title { font-size: 16px; }
  .card__button { background-color: #111; }
  ```


<br />
<br />


## SMACSS (Scalable and Modular Architecture for CSS)
- CSS를 모듈화하고 체계적으로 관리하기 위해 고안된 방법론이다.

- 스타일 시트를 다섯 가지 카테고리로 나누어 작업한다.

- 스타일 시트가 구조화되어 있어 유지보수에 용이하다.

- 모듈화된 Class를 여러 곳에서 재사용할 수 있다.

### Base
- 브라우저 기본 스타일을 초기화하거나, HTML 태그에 대한 기본 스타일을 정의합니다.

  ```css
  html, body, p, h1, h2, h3, ul, ol, li {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
  }
  
  body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
  }
  ```

### Layout
- 페이지의 전체적인 레이아웃 구조를 정의한다.

- 헤더, 푸터, 사이드바 등 페이지의 주요 컨테이너를 설정한다.

- 주로 페이지의 배치와 크기를 다룬다.

  ```css
  .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
  }
  
  .footer {
      padding: 10px;
      color: white;
      text-align: center;
      background-color: #333;
  }
  ```

### Module
- 재사용 가능한 UI 컴포넌트를 정의한다.

- 카드, 버튼, 메뉴 등 독립적으로 동작하는 요소를 포함한다.

- 모듈은 보통 여러 곳에서 재사용되며, 작은 단위로 설계된다.

  ```css
  .card {
      padding: 20px;
      background-color: white;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .button {
      display: inline-block;
      padding: 10px 20px;
      background-color: #007bff;
      cursor: pointer;
  }
  
  .button:hover {
      background-color: #0056b3;
  }
  ```

### State
- UI 요소의 상태를 정의한다.

- 활성화, 비활성화, 숨김, 에러 상태 등 특정 조건에서 적용되는 스타일을 포함한다.

- 보통 is- 또는 has- 접두사를 사용하여 상태를 나타낸다.

  ```css
  .button.is-active {
      background-color: #28a745;
  }
  
  .card.is-hidden {
      display: none;
  }
  
  .form.has-error {
      border-color: red;
  }
  ```

### Theme
- 시각적 테마를 정의한다.

- 색상, 폰트 스타일, 다크 모드 등을 설정하는 데 사용된다.

- 프로젝트의 일관된 디자인 시스템을 관리하는 데 유용하다.

  ```css
  .theme-light {
      --background-color: #ffffff;
      --text-color: #333333;
  }
  
  .theme-dark {
      --background-color: #333333;
      --text-color: #ffffff;
  }
  
  body {
      background-color: var(--background-color);
      color: var(--text-color);
  }
  ```