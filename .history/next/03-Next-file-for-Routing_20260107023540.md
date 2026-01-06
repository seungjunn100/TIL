# Next.js 라우팅용 특수 파일

- [라우팅용 특수 파일](#라우팅용-특수-파일)
  - [loading](#loading)
  - [error](#error)
  - [not-found](#not-found)
  - [route handler](#route-handler)




<br />
<br />




## 라우팅용 특수 파일

### loading

- 내부적으로 `React Suspense`를 사용하여 컨텐츠가 로드되는 동안 대체할 컴포넌트로 사용된다.

  - `Next.js`는 `Page` 컴포넌트가 `async` 함수일 때 반환되는 `Promise`를 이용해서 로딩중인지(`pending`) 완료되었는지(`fulfilled, rejected`) 상태를 추적해서 `loading` 컴포넌트를 보여줄 수 있다.

![라우팅용 특수 파일 - loading](../src/images/nextjs-route-loading-1.png)

- 3초 뒤에 `page`가 렌더링된다.

- 로딩중 상태에서도 공통 레이아웃은 사용 가능하다.

![라우팅용 특수 파일 - loading](../src/images/nextjs-route-loading-2.png)

- 로딩 컴포넌트를 사용하지 않고 해당 페이지를 렌더링하게 되면, 3초동안은 아무 것도 렌더링되지 않는다.

- 사용자 입장에서 게시물 목록 조회 말고 게시물을 등록하기 위해 글쓰기 페이지에 들어가려고해도,
  
  -  3초 동안 기다린 후에 렌더링이 되고 들어가야 하므로 `UX` 측면에서 좋지 않다.

- 리액트는 `<Suspense>`를 사용한다.

  ![React Suspense](../src/images/nextjs-react-suspense.png)

<br />

### error

- 정상적인 애플리케이션 흐름 중에 발생해서는 안 되는 버그나 문제를 처리하기 위해 사용한다.

- 컴포넌트 렌더링시 에러가 발생할 경우 `error` 파일에서 에러 처리 및 에러 `UI`를 보여준다.

  - 클라이언트 컴포넌트여야 한다.

- `posts` 하위의 `[id]` 페이지에서 에러가 발생했을 때 에러 파일이 없다면, 상위(`posts`)에 있는 에러 페이지를 렌더링하게 된다.

  - 하위의 파일들을 상위에서 한번에 해결할 수도 있다.

  ![라우팅용 특수 파일 - error](../src/images/nextjs-route-error-1.png)

- `page`에서 에러가 발생할 경우 같은 폴더의 `error`에서 처리되고, `layout`에서 에러가 발생할 경우 상위 폴더의 `error`에서 처리된다.

  ![라우팅용 특수 파일 - error](../src/images/nextjs-route-error-2.png)

- 루트 레이이웃에서 에러가 발생할 경우 상위 폴더가 없으므로 에러 처리가 안되면,
  
  - 대신 `app/global-error.tsx` 파일에서 에러 처리

<br />

### not-found

- 해당 경로에서 `404`(페이지를 찾을 수 없음) 오류가 발생했을 때 보여줄 사용자 정의 `404` 페이지를 구현할 때 사용

- 이 파일이 존재하는 폴더 및 하위 경로에서 라우팅이 실패하거나, 서버 컴포넌트/서버 함수에서 `notFound()` 함수를 호출하면 자동으로 `not-found`에 정의된 `UI`가 렌더링됨

- 사용자에게 친절한 안내 메시지, 홈으로 이동 버튼 등 커스텀 `404` 화면을 제공하도록 작성

- 일반적으로 글로벌 `404` 처리를 위해 루트(`app`) 폴더에 `not-found` 파일을 둠

![라우팅용 특수 파일 - not-found](../src/images/nextjs-route-not-found.png)

<br />

### route handler

#### Netlify 흐름도

![netlify 흐름도](../src/images/netlify-flowchart.png)

- `Netlify`에 배포하면 `HTML`, `JS`, `CSS` 같은 정적 파일들이 웹서버에 저장된다.

- 클라이언트(브라우저)는 페이지 요청 시 이미 만들어진 정적 파일을 전달받는다.

- 이 웹서버는 로직 실행 없이 요청에 대해 정해진 파일만 응답한다.

- 페이지가 렌더링되면서 브라우저에서 실행된 스크립트가 `API` 서버에 데이터 요청을 보낸다.

- `API` 서버는 `DB`에서 데이터를 조회해 다시 클라이언트에게 응답한다.

#### Next.js 흐름도

![nextjs 흐름도](../src/images/nextjs-flowchart.png)

- `Next.js` 서버는 `Node.js` 기반 애플리케이션 서버이다.

- 단순 웹서버와 달리 요청에 대한 응답뿐 아니라, 데이터 가공, 추가 로직 처리가 가능하다.

- `Route Handler`를 사용하면 `Next.js` 안에서 `API` 서버를 직접 구현할 수 있다.

  - `DB`와 직접 연동할 수도 있고, 외부 `API` 서버와 연동할 수도 있다.

- 서버 함수를 통해 데이터 조회, 가공, 응답을 서버에서 처리할 수 있다.

- 개발 시에는
→ console.log를 통해
→ 코드가 클라이언트에서 실행되는지, 서버에서 실행되는지를 구분할 수 있어야 한다.