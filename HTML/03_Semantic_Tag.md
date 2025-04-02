# 시맨틱 태그 (Semantic Tag)
- HTML에서 태그 자체가 콘텐츠의 의미나 역할을 명확히 표현하는 태그를 말한다.

- 시맨틱 태그가 중요한 이유
  - 접근성 향상
    - 스크린 리더가 HTML 구조를 더 잘 이해하여 장애를 가진 사용자에게 적합한 경험을 제공한다.
  - SEO 최적화
    - 검색 엔진 크롤러가 페이지의 구조와 내용을 명확히 이해하므로, 검색 엔진 최적화(SEO)에 유리하다.
  - 코드 가독성 향상
    - 개발자나 협업자가 HTML 코드를 읽을 때 구조를 쉽게 파악할 수 있다.


<br />
<br />


## 구조를 나타내는 태그
- 웹 페이지의 전체적인 레이아웃을 구성하는 태그이다.

### `<header>`
- 소개 및 탐색에 도움을 주는 콘텐츠

- 제목, 로고, 검색 폼, 작성자 이름 등을 포함할 수 있다.

- 전체 페이지를 대표하는 제목으로 들어갈 수 있다.

- 한 기사, 논문의 글 제목으로 들어갈 수 있다.

```html
<header>
  <h1>웹사이트 제목</h1>
  <nav>
    <a href="#home">Home</a>
    <a href="#about">About</a>
  </nav>
</header>
```

### `<nav>`
- 현재 페이지 내 또는 다른 페이지로의 링크를 보여주는 구획

```html
<nav>
  <a href="#home">Home</a>
  <a href="#about">About</a>
</nav>
```

### `<main>`
- body 태그의 하위 자식으로 사용되며 단 하나만 사용이 가능하다.

- 여러개 사용시에는 유일한 main 요소 외에 나머지 요소는 hidden 속성을 사용하여 눈에 보이지 않게 해야한다.

```html
<main>
  <section>
    <h2>섹션 제목</h2>
    <p>섹션 내용입니다.</p>
  </section>

  <section>
    <h2>섹션 제목</h2>
    <p>섹션 내용입니다.</p>
  </section>
</main>
```

### `<section>`
- 특정 주제나 섹션을 그룹화할 때 사용한다.

- `<article>`과는 다르게 단독적으로 사용 불가하다.

- `<h2>` 이상의 제목이 포함되는 것이 일반적이다.

- 회사 소개, 서비스 소개, 제품 정보, FAQ 목록 등에 사용이 된다.

```html
<!-- section만 사용 -->
<section>
  <h2>회사 소개</h2>
  <p>우리 회사는 2010년에 설립되었으며...</p>
</section>

<!-- section, article 사용 -->
<section>
  <h2>블로그 글</h2>
  
  <article>
    <h2>HTML5 시맨틱 태그란?</h2>
    <p>HTML5에서는 문서 구조를 명확하게 하기 위해...<p>
  </article>
  
  <article>
    <h2>HTML5 시맨틱 태그란?</h2>
    <p>HTML5에서는 문서 구조를 명확하게 하기 위해...<p>
  </article>
</section>
```

### `<article>`
- 독립적인 콘텐츠를 의미한다.

- 독립적으로 구분해 배포하거나 재사용할 수 있는 컨텐츠를 나타낸다.

- 식별할 수단으로 주로 제목(`<h1>` ~ `<h6>`) 요소를 넣어준다.

- 게시판과 블로그 글, 매거진이나 뉴스 기사 등에 사용이 된다.

```html
<!-- 메타 정보나 하단 정보가 필요 없을 때 -->
<article>
  <h2>HTML5 시맨틱 태그란?</h2>
  <p>HTML5에서는 문서 구조를 명확하게 하기 위해...<p>
</article>

<!-- 메타 정보나 하단 정보가 필요할 때 -->
<article>
    <header>
        <h2>HTML5 시맨틱 태그란?</h2>
        <p>작성자: 홍길동 | 날짜: 2025-03-17 | 카테고리: 웹 개발</p>
    </header>
    
    <p>HTML5에서는 문서 구조를 명확하게 하기 위해 시맨틱 태그를 도입했습니다...</p>

    <footer>
        <p>출처: <a href="https://example.com">example.com</a></p>
        <p>태그: <a href="#">#HTML5</a>, <a href="#">#웹개발</a></p>
    </footer>
</article>
```

### `<aside>`
- 문서의 주요 내용과 간접적으로만 연관된 부분을 나타낸다.

- 추가적인, 부가적인 정보지만 없다고 해서 본문에 크게 문제가 되지 않은 것들을 포함한다.
 
- 사이드바 혹은 콜아웃 박스

```html
<aside>
  <p>이 내용은 추가 정보입니다.</p>
</aside>
```

### `<footer>`
- 구획의 작성자, 저작권 정보, 관련 문서 등을 포함할 수 있다.

- 사이트의 전체를 아우를 수 있는 링크들을 포함할 수 있다.

```html
<footer>
    <p>&copy; 2025 Website</p>
</footer>
```


<br />
<br />


## 참고 사이트
- <a href="https://developer.mozilla.org/ko/docs/Web/HTML/Element" target="_blank">HTML Element</a> - MDN 기타 의미론적인 태그 참고

- <a href="https://html.spec.whatwg.org/" target="_blank">HTML Standard</a> - 예제를 통한 태그 사용법 참고 ⭐️