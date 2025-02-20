## 웹 표준 (Web Standards)
- 웹 표준은 웹에서 사용되는 기술들의 표준화를 의미한다.

- 웹 표준을 준수하여 작성한다면
  - 어떤 운영체제나 브라우저를 사용하더라도 동일하게 보여지는 웹 페이지를 만들 수 있다.
  - 검색 엔진에서 웹 페이지를 더욱 잘 인식할 수 있다.
  - 유지보수가 용이하다.
  - 논리적이고 효율적으로 작성된 웹 문서는 코드의 양이 줄어 파일 크기가 줄고 서버의 부담이 감소한다.
  - 모든 사용자가 쉽게 웹 페이지에 접근할 수 있도록 웹 접근성을 향상시킬 수 있다.

<br />

### 웹 표준을 준수하는 방법
- 시맨틱 태그 사용

- CSS 스타일 시트 사용

- 웹 호환성 고려

- 웹 접근성 고려


<br />
<br />


## 웹 접근성 (Web Accessibility)
- 웹 접근성은 장애를 가진 사람과 장애를 가지지 않은 사람, 모든 사용자들이 웹 사이트를 이용할 수 있어야 한다.

- 웹 브라우징에 쓰이는 보조과학기술
  - 스크린 리더
  - 화면 확대 도구구
  - 음성 인식
  - 키보드 오버레이
  - etc..

<br />

### 웹 접근성을 준수하는 방법
- 시각적 요소 처리
  - 대체 텍스트, 적절한 색상 대비, 텍스트 크기 등을 고려하여 시각적 요소를 처리해야 한다.
- 청각적 요소 처리
  - 자막, 수화, 오디오 설명 등을 제공하여 청각적 요소를 처리해야 한다.
- 키보드 접근성
  - 지체 장애인은 마우스를 사용하지 못하므로 키보드만으로 웹 사이트를 이용할 수 있도록 구현해야 한다.
- 웹 접근성 검사
  - [Accessibility Korea](https://accessibility.kr/)
  - [OpenWAX](https://chromewebstore.google.com/detail/openwax/bfahpbmaknaeohgdklfbobogpdngngoe)
  - [WAVE](https://wave.webaim.org/)
  - [W3C](https://validator.w3.org/)


<br />
<br />


## 웹 호환성 (Cross Browsing)
- 모든 브라우저에서 깨지지 않고 의도한 대로 동작하도록 하는 작업을 의미한다.

- 브라우저마다 화면을 보여주는 렌더링 엔진이 달라 브라우저에 따라서 다르게 보일 수 있다.

<br />

### 웹 호환성을 준수하는 방법
- DOCTYPE 정의
  - Document Type(문서의 타입)을 명시한다.
    - HTML이 어떤 버전으로 작성되었는지 미리 선언하여 웹 브라우저가 내용을 올바로 표시할 수 있도록 해준다.

  - 선언하지 않을 경우 비표준 모드(quirks mode)로 문서를 실행한다.
    - 익스플로러5, 네비게이터4 등 옛날 브라우저를 모방해서 문서를 실행해 호환성에 이슈가 발생할 수 있다.

- 코드 유효성 검사
  - 잘못된 HTML, CSS 코드로 인해 모든 브라우저에서 다양한 방식으로 이슈가 발생할 수 있다.
  - [W3C](https://validator.w3.org/)

- CSS 초기화
  - 브라우저마다 기본으로 제공하는 style이 있어서 기본값을 통일해 주기 위해 초기화 설정을 해주어야 한다.

- CSS 속성에 대한 지원 검토
  - 브라우저마다 CSS 속성을 동일하게 지원하지 않으므로 호환 여부를 확인하고 사용해야 한다.
  - [Can I Use](https://caniuse.com/)

- Vendor Prefix
  - 브라우저마다 지원되는 CSS 속성이 다를 수 있기 때문에 Vendor Prefix 사용하여 모든 브라우저에서 원할하게 사용할 수 있다.
    - IE, Edge : -ms-
    - Chrome : -webkit-
    - Firefox : -moz-
    - Safari : -webkit-
    - Opera : -o-
    - iOS Safari : -webkit-
    - Android Browser : -webkit-
    - Chrome for Android : -webkit-

- 반응형 웹사이트 제작
  - 모든 브라우저나 기기에서 기능이 가능하고 정보를 확인할 수 있어야 한다.

- meta 태그 이용
  - `<meta http-equiv="X-UA-Compatible" content="IE=edge">`
    - IE 브라우저의 최신 버전의 엔진을 사용하라는 뜻이며 오래된 버전의 브라우저를 최신 버전으로 지원하여 호환성을 가질 수 있다.

  - `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
    - PC에서 보는 화면을 모바일에서도 잘 보일수 있게 한다.

  - `<meta charset="utf-8">`
    - 문자를 인코딩하는 방식을 선언하여 문자 깨짐 현상 등 오류를 방지할 수 있다.