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

![라우팅용 특수 파일 - loading](../src/images/nextjs-route-loading.png)

- 3초 뒤에 `page`가 렌더링된다.

- 리액트는 Suspense 컴포넌트를 사용한다.

- 로딩을 안쓰면 posts의 경로에 들어가면 3초동안은 아무 것도 렌더링되지 않는다.

- 사용자 입장에서 게시물 목록 조회 말고 게시물 등록 페이지에 들어가려고해도 3초 동안 기다린 후에 렌더링이 되고 들어가야 하므로 UX 측면에서 좋진 않다.

<br />

### error

<br />

### not-found

<br />

### route handler