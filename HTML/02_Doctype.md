# `<!DOCTYPE>`
- 웹 문서의 형식과 버전을 브라우저에 알려주는 역할을 한다.
  - 이는 브라우저가 페이지를 올바르게 렌더링하도록 돕는 중요한 요소이다.
- HTML5 표준 이전에는 버전을 명시하여 브라우저가 명시된 버전에 맞는 문법으로 해석하였다.


<br />
<br />


## HTML5
- 현재는 대부분의 브라우저가 HTML5의 표준을 준수하고 있기때문에 html이라고만 적어도 해석이 가능하다.

  ```html
  <!DOCTYPE html>
  ```


<br />
<br />


## HTML 4.01
- HTML 4.01 Strict
  - 최신 웹 표준을 따르고, 오래된 태그나 속성을 허용하지 않는다.

  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
  ```

- HTML 4.01 Transitional
  - 오래된 태그와 속성도 허용되며, 현대적인 표준과 호환된다.

  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
  ```
  
- HTML 4.01 Frameset
  - 프레임셋을 사용하는 레이아웃을 지원한다.

  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
  ```


<br />
<br />


## XHTML 1.0
- XHTML 1.0 Strict
  - 최신 웹 표준을 따르고, 오래된 태그나 속성을 허용하지 않는다.

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
  ```

- XHTML 1.0 Transitional
  - 오래된 태그와 속성도 허용되며, 현대적인 표준과 호환된다.

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
  ```

- XHTML 1.0 Frameset
  - 프레임셋을 사용하는 레이아웃을 지원한다.

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
  ```


<br />
<br />


## XHTML 1.1
- XHTML 1.0 Strict의 확장판으로, 추가적인 모듈화 기능을 지원한다.

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
  ```


<br />
<br />


## 만약 doctype을 선언하지 않으면❓
- 브라우저는 웹 페이지를 쿼크 모드(Quirks Mode)로 렌더링하게 된다.
  - 현대적인 웹 표준을 따르지 않고, 과거의 비표준 방식(익스플로러5, 네비게이터4 등 구버전 브라우저와의 호환성 중심)으로 웹 페이지를 처리한다.

- 발생할 수 있는 문제
  - 레이아웃 및 스타일
    - CSS가 의도한 대로 적용되지 않을 수 있다.
  - Javascript 동작 차이
    - 일부 JavaScript 기능이 현대적인 방식과 다르게 작동할 수 있다.
  - 브라우저 간 차이 증가
    - 브라우저별 렌더링 차이가 커져, 예상치 못한 결과가 발생할 수 있다.
  - 디버깅 어려움
    - 웹 페이지가 정상적으로 보이지 않을 경우 문제를 추적하기 어려워진다.