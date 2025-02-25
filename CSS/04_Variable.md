# CSS 변수
- 값을 `변수`에 정의하고 여러 곳에서 사용할 수 있는 기능이다.

- 사용자 지정 CSS 속성(`CSS Custom Properties`)이라고도 불린다.


<br />
<br />


## CSS 변수의 기본 문법
- 변수 선언 및 사용

```css
/* 변수 선언 */
:root {
  --color-blue: #03e8f9;
  --font-size: 16px;
}

/* 변수 사용 */
h1 {
  color: var(--color-blue);
  font-size: var(--font-size);
}
```


<br />
<br />


## CSS 변수 대체값 설정
- 변수가 없다면 기본값을 사용하거나 대체 변수를 사용하도록 지정할 수 있다.

```css
:root {
  --color-sky: #03e8f9;
  --color-blue: #006dd7;
}

h1 {
  color: var(--color-sky, blue);
}

h2 {
  color: var(--color-sky, var(--color-blue, blue));
}
```


<br />
<br />


## 한 단계 추상화한 변수 작업💡
- 유지보수가 한 단계 더 향상된다.

```css
:root {
  /* Mainly used colors */
  --color-primary: var(--color-black); /* 주요 색상 */
  --color-primary-variant: var(--color-gray); /* 주요 색상에서 조금 변형된 색상 */
  --color-accent: var(--color-blue); /* 강조 색상 */
  --color-accent-variant: var(--color-orange); /* 강조 색상에서 조금 변형된 색상 */
  --color-text: var(--color-white); /* 텍스트 색상 */

  /* Colors */
  --color-white: #ffffff;
  --color-black: #050a13;
  --color-blue: #006dd7;
  --color-orange: #fd6413;
  --color-gray: #1b1e26;
}

h1 {
  color: var(--color-primary);
}
```


<br />
<br />


## CSS 변수의 장점
- 유지보수성 향상
  - 변수 이름만 수정하면 전체 스타일이 업데이트되어 작업 시간이 절약된다.

- 일관성 있는 디자인 유지
  - 프로젝트 전반에 걸쳐 동일한 색상, 크기, 간격 등을 유지할 수 있다.

- 가독성 증가
  - 의미 있는 변수명을 사용하면 코드 읽기가 쉬워집니다.