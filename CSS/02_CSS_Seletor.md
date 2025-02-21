## 기본 선택자
- 태그 선택자 
  - `h1`

- 클래스 선택자 
  - `.highlight`

- 아이디 선택자 
  - `#header `


<br />
<br />


## 결합 선택자
- 후손 선택자 
  - `div p`

- 자식 선택자 
  - `ul > li`

- 형제 선택자
  - `h1 ~ p`

- 인접 형제 선택자 
  - `h1 + p`


<br />
<br />


## 속성 선택자
- 기본 속성 선택자 
  - `input[type="text"]`

- 부분 속성 선택자
  - 속성값이 특정 값으로 시작하는 경우 `^=`
    - `a[href^="https://"]`
  - 속성값이 특정 값으로 끝나는 경우 `$=`
    - `img[src$=".png"]`
  - 속성값이 특정 값을 포함하는 경우 `*=`
    - `div[class*="main"]`


<br />
<br />


## 의사(가상) 클래스
📌 `:`는 의사 클래스를 나타낸다.
- 구조 의사 클래스
  - `:first-child`
    - 자식 요소 중에 첫 번째 자식 요소를 선택한다.
  - `:last-child`
    - 자식 요소 중에 마지막 자식 요소를 선택한다.
  - `:nth-child(n)`
    - 자식 요소 중에 n 번째 자식 요소를 선택한다.
  - `:nth-last-child(n)`
    - 자식 요소 중에 마지막에서부터 n 번째 자식 요소를 선택한다.
  - `:first-of-type`
    - 자식 요소 중에 자신의 유형과 일치하는 첫 번째 자식 요소를 선택한다.
  - `:last-of-type`
    - 자식 요소 중에 자신의 유형과 일치하는 마지막 자식 요소를 선택한다.
  - `:nth-of-type(n)`
    - 자식 요소 중에 자신의 유형과 일치하는 n 번째 자식 요소를 선택한다.
  - `:nth-last-of-type(n)`
    - 자식 요소 중에 마지막에서부터 자신의 유형과 일치하는 n 번째 자식 요소를 선택한다.
  - `only-child`
    - 자식 요소 중에 유일한 자식 요소를 선택한다.

- 동적 의사 클래스
  - `:link`
    - `<a>` 요소의 기본 스타일
    - 사용자가 요소의 링크를 한 번도 누르지 않은 상태
  - `:visited`
    - 사용자가 요소의 링크를 한 번이라도 누른 상태
  - `:hover`
    - 사용자가 요소 위에 마우스를 올려놓은 상태
  - `:active`
    - 요소가 클릭중인 상태
  - `:focus`
    - 요소에 포커스가 맞춰진 상태

- 상태 의사 클래스
  - `:disabled`
    - 비활성화된 상태의 요소를 선택한다.
  - `:enabled`
    - 활성화된 상태의 요소를 선택한다.
  - `:checked`
    - 체크된 상태의 요소(`checkbox`, `radio`)를 선택한다.

- 기타 의사 클래스
  - `:not(selector)`
    - 특정 선택자에 해당하지 않는 요소를 선택한다.
  - `:has(selector)`
    - 부모 요소가 특정 자식 요소를 가지고 있을 경우
  - `:empyt`
    - 자식 요소나 텍스트가 없는 요소를 선택한다.
  - `:lang(language)`
    - 특정 언어 속성을 가진 요소를 선택한다.

- [더 다양한 의사 클래스 - MDN](https://developer.mozilla.org/ko/docs/Web/CSS/Pseudo-classes)


<br />
<br />


## 의사(가상) 요소
📌 `::`는 의사 요소를 나타낸다.
- `::before`
  - 선택된 요소 내용의 시작 부분에 가상 요소를 생성한다.

- `::after`
  - 선택된 요소 내용의 끝 부분에 가상 요소를 생성한다.

- `::first-line`
  - 요소의 첫 번째 줄에 스타일을 적용한다.

- `::first-letter`
  - 요소의 첫 번째 글자에 스타일을 적용한다.

- `::marker`
  - 리스트(`ul`, `ol`)의 항목 불릿이나 번호에 스타일을 적용한다.

- `::selection`
  - 사용자가 선택한(드래그) 텍스트에 스타일을 적용한다.

- `::placeholder`
  - `<input>`, `<textarea>` 요소의 `placeholder` 텍스트에 스타일을 적용한다.

- [더 다양한 의사 요소 - MDN](https://developer.mozilla.org/ko/docs/Web/CSS/Pseudo-elements)


<br />
<br />


## 게임을 활용한 선택자 공부법
- [CSS Diner - Where we feast on CSS Selectors!](https://flukeout.github.io/)