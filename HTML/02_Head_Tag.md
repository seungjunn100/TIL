# `<head>`에 들어가는 태그
- 웹 페이지의 메타 정보, 스타일, 스크립트, SEO 최적화 요소 동을 포함하는 중요한 부분이다.


<br />
<br />


## `<title>` 태그
- 페이지의 제목을 정의하며, 검색 결과의 링크로 표시됩니다.
  ```html
  <title>SEO에 최적화된 메타태그 작성법</title>
  ```


<br />
<br />


## `<meta>` 태그
- 페이지에 대한 정보를 포함하고 있다.

- 메타태그는 검색 엔진이 페이지의 내용과 목적을 파악하는 데 필요한 정보를 제공한다.

- 검색 엔진이 메타태그를 기반으로 페이지를 색인(indexing)하고 검색 결과에 노출할 키워드를 결정한다.

<br />

### 문자 인코딩 (Charset)
- HTML 파일의 인코딩 방식을 명시하는 태그이다.

- 유니코드인 UTF-8의 charset으로 다양한 언어를 모두 표현할 수 있다.
  ```html
  <meta charset="UTF-8" />
  ```

<br />

### 뷰포트 (Viewport)
- 모바일 친화적인 페이지를 제공하기 위해 화면 크기를 설정한다.

- 모바일 SEO에 매우 중요하다.
  ```html
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  ```

<br />

### 브라우저 호환성 (X-UA-Compatible)
- Internet Explorer(IE) 브라우저에서의 호환성을 제어하기 위해 도입되었다.

- 웹 페이지가 IE에서 어떤 렌더링 모드를 사용할지 지정하는 데에 사용된다.

- IE의 사용이 줄어들면서 현대적인 웹 개발에서는 이 태그가 거의 필요하지 않게 되었다.
  ```html
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  ```

<br />

### 저자 (Author)
- 페이지의 저자를 지정할 수 있다.
  ```html
  <meta name="author" content="BBaek" />
  ```

<br />

### 설명 (Description)
- 페이지 요약 정보를 제공한다.

- 검색 결과 페이지(SERP)에 표시되는 설명 텍스트로 사용된다.
  ```html
  <meta name="description" content="메타(meta)태그를 알아보자!" />
  ```

<br />

### 키워드 (Keywords)
- 페이지와 관련된 키워드 목록을 나열한다.

- 과거에는 SEO에 중요했지만, 현재 대부분의 검색 엔진(예: Google)에서는 사용하지 않는다. 
  ```html
  <meta name="keywords" content="SEO, 메타태그, 검색엔진 최적화">
  ```

<br />

### OG (Open Graph Data)
- Facebook에서 만들었으며 웹 사이트에 더 풍부한 메타 데이터를 제공하기 위해 발명하였다.
  ```html
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="BBaek’s record">
  <meta name="twitter:description" content="BBaek’s record">
  <meta name="twitter:image" content="https://example.com/image.jpg">
  ```

<br />

### Twitter 카드
- Facebook에서 만들었으며 웹 사이트에 더 풍부한 메타 데이터를 제공하기 위해 발명하였다.
  ```html
  <meta property="og:title" content="BBaek’s record" />
  <meta property="og:url" content="https://example.com" />
  <meta property="og:image" content="https://example.com/image.jpg" />
  ```

<br />

### 로봇 (Robots)
- 검색 엔진 크롤러가 페이지를 색인하거나 링크를 따라가는 방식을 제어한다.
  ```html
  <meta name="robots" content="index, follow">
  ```


<br />
<br />


## `<link>` 태그
- favicon
  ```html
  <link rel="shortcut icon" href="favicon.ico" type="image/x-icon" />
  ```

- CSS
  ```html
  <link rel="stylesheet" href="css/style.css" />
  ```


<br />
<br />


## `<script>` 태그
- Javascript
  ```html
  <script src="js/script.js"></script>
  ```