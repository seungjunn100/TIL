# CSS 란
- Cascading Style Sheets의 약자
  - `Cascading`
    - 폭포 같은, 연속 되는, 우선순위가 있는..
  - `Style Sheets`
    -  스타일 문서

- 웹 페이지의 디자인과 레이아웃을 정의하는 스타일링 언어이다.


<br />
<br />


## CSS 기본 구조
- CSS 규칙은 선택자(Selector), 속성(Property), 값(Value)으로 구성됩니다.
  ```css
  선택자 {
    속성: 값;
  }

  /* 태그 선택자 */
  p { color: pink; }
  
  /* 클래스(class) 선택자 */
  .highlight { background-color: yellow; }
  
  /* 아이디(id) 선택자 */
  #header { text-align: center; }

  /* 하위 선택자 */
  div p { color: green; }
  
  /* 그룹 선택자 */
  h1, h2, h3 { font-family: Arial; }
  ```

- [선택자의 여러 종류](/CSS/02_Seletor.md)


<br />
<br />


## CSS 사용 방식
- 태그 안에 style 속성을 사용한 `Inline` 방식
  ```html
  <div style="color: pink; font-size: 26px;"></div>
  ```

- HTML 파일 안에 `<style>` 태그 안에 작성
  ```html
  <head>
      <style>
          div {
            color: pink;
            font-size: 26px;
          }
      </style>
  </head>
  ```
  
- CSS 파일에 작성 후 HTML 파일에서 `<link>`로 연결하는 방식 - 추천 방식⭐️
  ```html
  <head>
      <link rel="stylesheet" href="style.css" />
  </head>
  ```
  - 한 번 수정하면 여러 HTML 파일에 적용되어 유지보수에 용이
  - 같은 CSS를 여러 페이지에서 활용 가능하여 재사용성 향상
  - CSS 파일이 다운로드되어 브라우저 캐시에 저장되 웹페이지 로딩 속도 향상
  - HTML 코드가 깔끔해지고 관리하기 쉬워 가독성이 향상
  - HTML 파일이 가볍고 깨끗해지므로, 검색 엔진이 HTML을 분석하는 속도가 빨라져 SEO 개선
  - 여러 CSS 파일을 모듈화하여 사용 가능


<br />
<br />


## CSS 적용 우선순위
- `!important`
  - 모든 우선순위를 무시하고 우선시해야 할 때 사용한다.
  - 왠만하면 사용하지 않는게 좋다.

- 우선순위
  1. `!important`
  2. `inline` - **1000점**
  3. `#id` - **100점**
  4. `.class`, 속성 선택자 (`[type="text"]`), 의사 클래스 (`:hover`) - **10점**
  5. `HTML tag`, 의사 요소 (`::before`) - **1점**

- 복합 선택자에서 하위 요소가 많아지면 우선순위가 높아진다.
  - 같은 `<li>` 태그를 선택했지만 `<ul>` 태그를 추가해준 복합 선택자가 우선 순위가 높다.
  ```css
  /* 2점 */
  div li { }

  /* 3점 */
  div ul li { }
  ```

- 동일한 레벨에서는 나중에 작성한 스타일이 우선순위가 높다.