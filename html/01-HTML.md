# HTML
- `Hyper Text Markup Language`의 약자
  - `Hyper Text`
    - 문서 간의 연결(링크)을 의미하며, 링크에 따라 다양한 문서들로 넘어갈 수 있다.
  - `Markup Language`
    - 태그를 이용하여 문서의 구조를 표기하는 것을 의미한다.
    - content(제목, 글, 이미지, 버튼 등)의 성격을 표시해주는 기능만 있는 마크업 언어이다.


<br />
<br />


## HTML 역사
- 1990년 팀 버너스리에 의해 개발되었다.

- 1993년 HTML 1.0이 IETF(Internet Engineering Task Force)에 의하여 표준으로 등장했다.

- 1995년 HTML 2.0이 IETF에 의하여 표준으로 등장했다.

- 1997년 HTML 3.2이 W3C(World Wide Web Consortium)에 의해 권고안으로 등장했다.

- 1999년 HTML 4.0이 W3C에 의해 권고안으로 등장했다.
  - 안정된 표준의 HTML 버전
  - CSS(Cascading Style Sheet)로 디자인적인 요소를 구분하게 되었다.
  - HTML로는 웹페이지의 전반적인 구조만을 명시하도록 원칙을 정하였다.

- 2000년 XHTML이 W3C의 새로운 표준 권고안으로 등장했다.
  - XML(Extensible Markup Language)의 엄격함을 주요 내용으로 HTML을 합성한 웹 표준
  - W3C는 시장 요구에 부응하지 못했다.
  - 그로 인해 대중적인 브라우저를 가지고 있던 기업들(Apple, Mozilla, Opera)이 WHATWG(Web Hypertext Application Technology Working Group)라는 단체를 만드는 계기가 됐다.
  - WHATWG이 HTML에 기초하여 웹 기술과 시장의 요구를 분석하여 HTML5 작업을 착수했다.

- 2008년 HTML 5.0이 W3C에 의해 초안으로 등장했다.
  - W3C의 HTML5 수용

- 2014년 HTML 5.0이 W3C에 의해 표준안으로 등장했다.
  - WHATWG는 W3C와 협업을 진행하면서도 W3C와는 별도로 독자적인 HTML 표준의 작업을 시작했다.
  - HTML Living Standard라는 이름으로 발표했다.
  - HTML Living Standard는 W3C의 HTML5와는 달리 버전 없이 그때그때 업데이트된다.

- 2019년 HTML Living Standard가 표준화가 되었다.
  - 표준이 2개면 혼란이 발생하기 때문에 W3C와 WHATWG는 논의를 통해 HTML 표준을 HTML Living Standard로 단일화하였다.


<br />
<br />


## HTML 작성 규칙
- HTML 문서는 요소(elements)들로 구성된다.

- 태그를 통해 어떤 요소인지 (제목, 본문, 이미지, 비디오 등) 명시한다.

- 여는 태그와 닫는 태그로 요소의 범위를 지정한다.
  ```html
  <p>내용(content)</p>
  ```

- 요소의 속성은 속성명 = "속성값" 형식으로 기술한다.
  ```html
  <img src="image.png" alt="profile">
  ```

- 중첩 요소(Nesting elements)
  ```html
  <p><strong>내용(content)</strong></p>
  ```

- 빈 요소(Void Elements)
  - 종료 태그 없이 단독으로 사용되는 요소
  - `XHTML` 에서 빈 요소인 경우에는 뒤에 슬래쉬(/)를 넣어줘야지만 브라우저가 Closing tag를 찾지 않고 동작을 하는 형태이다.
  - `HTML5` 에서는 빈 요소의 슬래쉬(/) 작성은 자유지만 한가지의 형태로 일관성있게 코드를 작성해야한다.
  ```html
  <hr>
  <br>
  <img src="image.jpg" alt="이미지 설명">
  <meta charset="UTF-8">
  ```

- Element Tag와 Container Tag
  - Element Tag : 기본 요소를 나타내는 태그
  - Container Tag : 다른 요소를 감싸는 태그
  ```html
  <!-- Element Tag -->
  <h2>제목입니다</h2>
  <p>이것은 일반 텍스트입니다.</p>

  <!-- Container Tag -->
  <div class="container">
    <h2>제목입니다</h2>
    <p>이것은 일반 텍스트입니다.</p>
  </div>
  ```

- 블록(Block)과 인라인(Inline)
  - 블록 레벨 요소 : 요소 하나당 한 줄을 꽉 차지한다.
  - 인라인 레벨 요소 : 요소의 컨텐츠만큼 자리를 차지한다.

- HTML5 에서는 모두 소문자로 작성하는 것을 권장한다.


<br />
<br />


## HTML 문서의 구조
- HTML5의 표준을 지키는 HTML의 기본 골격
```html
  <!DOCTYPE html>
  <html lang="ko">
    <head>
      <!-- HEAD 영역 -->
    </head>
    <body>
      <!-- BODY 영역 -->
    </body>
  </html>
```

<br>

### `<!DOCTYPE>`
- 웹 문서의 형식과 버전을 브라우저에 알려주는 역할을 한다.
  - 이는 브라우저가 페이지를 올바르게 렌더링하도록 돕는 중요한 요소이다.

- HTML5 표준 이전에는 버전을 명시하여 브라우저가 명시된 버전에 맞는 문법으로 해석하였다.

- 현재는 대부분의 브라우저가 HTML5의 표준을 준수하고 있기때문에 `<!DOCTYPE html>`이라고만 적어도 해석이 가능하다.

- 만약 `<!DOCTYPE>`을 선언하지 않으면❓
  - 브라우저는 웹 페이지를 쿼크 모드(Quirks Mode)로 렌더링하게 된다.
    - 현대적인 웹 표준을 따르지 않고, 과거의 비표준 방식(익스플로러5, 네비게이터4 등 구버전 브라우저와의 호환성 중심)으로 웹 페이지를 처리한다.

  - 발생할 수 있는 문제
    - CSS가 의도한 대로 적용되지 않을 수 있다.
    - 일부 JavaScript 기능이 현대적인 방식과 다르게 작동할 수 있다.
    - 브라우저별 렌더링 차이가 커져, 예상치 못한 결과가 발생할 수 있다.
    - 웹 페이지가 정상적으로 보이지 않을 경우 문제를 추적하기 어려워진다.

<br>

### `<html lang="ko">`
- 페이지 전체의 컨텐츠를 감싸는 최상위(root) 요소
- lang 속성 : 문서에서 사용하는 주언어 language 명시

<br>

### `<head>`
- 문서의 메타데이터(웹사이트에 대한 설명)
- CSS, script 링크(외부 파일 연결)
- [`<head>`에 들어가는 태그](/HTML/03_Head.md)

<br>

### `<body>`
- 문서의 UI 구성 요소들



































# HTML
- 웹 브라우저에서 보여지는 `문서`이며, 표준화된 마크업 언어를 사용한다.

- `Hyper Text Markup Language`의 약자
  - `Hyper Text`
    - `하이퍼링크(참조)`를 통해 한 문서에서 `다른 문서로 즉시 접근 가능`한 텍스트를 의미한다.

  - `Markup Language`
    - `태그를 이용`하여 문서의 `구조를 표기`하는 것을 의미한다.
    - `content(제목, 글, 이미지, 버튼 등)의 성격을 표시`해주는 기능만 있는 마크업 언어이다.


<br />
<br />


## HTML 문서의 구조
- HTML5의 표준을 지키는 HTML의 기본 골격
```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <!-- HEAD 영역 -->
  </head>
  <body>
    <!-- BODY 영역 -->
  </body>
</html>
```

<br>

### `<!DOCTYPE>`
- 웹 문서의 형식과 버전을 브라우저에 알려주는 역할을 한다.
  - 이는 브라우저가 페이지를 올바르게 렌더링하도록 돕는 중요한 요소이다.

- HTML5 표준 이전에는 버전을 명시하여 브라우저가 명시된 버전에 맞는 문법으로 해석하였다.
  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
  ```

- 현재는 대부분의 브라우저가 HTML5의 표준을 준수하고 있기때문에 간략히 명시해도 해석이 가능하다.
  ```html
  <!DOCTYPE html>
  ```

#### 만약 `<!DOCTYPE>`을 선언하지 않으면❓
- 브라우저는 웹 페이지를 쿼크 모드(Quirks Mode)로 렌더링하게 된다.
  - 현대적인 웹 표준을 따르지 않고, 과거의 비표준 방식으로 웹 페이지를 처리한다.

- 발생할 수 있는 문제
  - CSS가 의도한 대로 적용되지 않을 수 있다.
  - 일부 JavaScript 기능이 현대적인 방식과 다르게 작동할 수 있다.
  - 브라우저별 렌더링 차이가 커져, 예상치 못한 결과가 발생할 수 있다.
  - 웹 페이지가 정상적으로 보이지 않을 경우 문제를 추적하기 어려워진다.

<br>

### `<html lang="ko">`
- 페이지 전체의 컨텐츠를 감싸는 `최상위(root)` 요소

- lang 속성 : 문서에서 사용하는 주언어 language 명시

<br>

### `<head>`
- 문서의 `메타데이터` - 웹사이트에 대한 설명
  - `SEO(Search Engine Optimization)` - title, 설명, 저자
    - 사용자가 어떤 키워드로 검색했을 때, 웹사이트를 검색엔진 결과에 나타낼 것인지..
    - 사용자가 빠르게 웹사이트를 찾을 수 있도록..
  - meta 태그를 사용해서 다양한 속성을 지정할 수 있다.

- `css`, `script` 외부 파일을 연결

- [`<head>`에 들어가는 태그](/HTML/03_Head_Tag.md)

<br>

### `<body>`
- 사용자에게 보여지는 웹사이트 내용 - `UI` 구성 요소들


<br />
<br />


## 웹의 표준화
- `W3C(World Wide Web Consortium)`는 웹의 표준화를 개발한다.

- W3C에서 태그를 정의하면 모든 브라우저들은 이 표준에 맞게 구현해야한다.
  - 그래서 태그를 작성했을 때 모든 브라우저들은 동일한 결과물을 기본적으로 제공하게 된다.

![웹의 표준화](../images/html-standard.png)


<br />
<br />


## HTML 작성 규칙
- HTML 문서는 요소(elements)들로 구성된다.

- 태그를 통해 어떤 요소인지 (제목, 본문, 이미지, 비디오 등) 명시한다.

- 여는 태그와 닫는 태그로 요소의 범위를 지정한다.
```html
  <p>내용(content)</p>
```

- 요소의 속성은 속성명 = "속성값" 형식으로 기술한다.
```html
  <img src="image.png" alt="profile">
```

- 중첩 요소(Nesting elements)
```html
  <p><strong>내용(content)</strong></p>
```

- 빈 요소(Void Elements)
  - 종료 태그 없이 단독으로 사용되는 요소
  - `XHTML` 에서 빈 요소인 경우에는 뒤에 슬래쉬(/)를 넣어줘야지만 브라우저가 Closing tag를 찾지 않고 동작을 하는 형태이다.
  - `HTML5` 에서는 빈 요소의 슬래쉬(/) 작성은 자유지만 한가지의 형태로 일관성있게 코드를 작성해야한다.
```html
  <hr>
  <br>
  <img src="image.jpg" alt="이미지 설명">
  <meta charset="UTF-8">
```

- Element Tag와 Container Tag
  - Element Tag : 기본 요소를 나타내는 태그
  - Container Tag : 다른 요소를 감싸는 태그
```html
  <!-- Element Tag -->
  <h2>제목입니다</h2>
  <p>이것은 일반 텍스트입니다.</p>

  <!-- Container Tag -->
  <div class="container">
    <h2>제목입니다</h2>
    <p>이것은 일반 텍스트입니다.</p>
  </div>
```

- 블록(Block)과 인라인(Inline)
  - 블록 레벨 요소 : 요소 하나당 한 줄을 꽉 차지한다.
  - 인라인 레벨 요소 : 요소의 컨텐츠만큼 자리를 차지한다.

- HTML5 에서는 모두 소문자로 작성하는 것을 권장한다.