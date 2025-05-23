# JavaScript
- 객체 기반의 스크립트 프로그래밍 언어이다.
  - 프로그래밍 언어
    - 프로그램을 만들기 위해 정해진 문법으로 특정한 로직을 수행하도록 작성할 때 사용되는 언어이다.
    - 어떤 환경에 어떤 일을 하냐에 따라서 적절한 프로그래밍 언어를 선택해야한다.

- 웹 페이지에서 기능을 더하거나, HTML/CSS를 조작해 동적이게 만들 수 있다.

- 주로 웹 브라우저에서 사용되며, 서버 개발(Node.js), 애플리케이션 개발에서도 사용이 가능하다.

- 단순히 문법만 가지고 있을 뿐 다양한 일들을 하기 위해서는 JavaScript 외부에 있는 호스트 환경(WebAPIs, Node.js API 등), 라이브러리, 프레임워크 등을 통해서 화면에 보여주고, 네트워크 통신을 하고, 다양한 일들을 할 수 있다.


<br />
<br />


## JavaScript 엔진
- JavaScript가 동작 하기 위해서는 JavaScript 엔진이 필요하다.

- 브라우저별 JavaScript 엔진
  - IE - Chakra
  - Edge - V8
  - Chrome - V8
  - Safari - JavaScript Core
  - Firefox - SpiderMonkey
  - 추가로 Node.js도 V8 엔진을 사용한다.

- 프로그래밍 언어를 컴퓨터가 읽을 수 있게 기계어로 변환해주는 방식
  - 인터프리터
    - 동적타입 (Dynamic Type)
    - JavaScript 엔진에는 인터프리터가 내장되어 있다.
    - 런타임시 코드를 한 줄씩 번역해서 실행하여 보여준다.

  - 컴파일러
    - 정적타입 (Static Type)
    - 실행하기전 모든 코드를 컴파일링하여 컴퓨터가 이해할 수 있는 실행파일로 변경하면 이 파일을 통해 컴퓨터에서 바로 실행할 수 있게 된다.


<br />
<br />


## ECMAScript
- JavaScript 문법의 규격사항, 표준사항

- 브라우저별 JavaScript 엔진은 ECMAScript의 표준을 통해 구현되어 있다.

- `ES6`
  - `ECMAScript6` 또는 `ECMAScript 2015` 로 정의될 수 있다.
  - 2015년 `ES5` 이하 에서 문제가 되었던 부분들이 해결 되고 많은 최신 문법들이 추가 되며 큰 변화가 일어난 시점으로 `ES6`가 표준안이 되었다.
  - 가독성과 유지보수성이 향상되었다.
  - 이 이후로는 `ES6`에서 조금씩 변화되고 추가되며 표준안이 업데이트 되었다.

- [버전별 문법 지원 현황 확인](https://compat-table.github.io/compat-table/es6/)
