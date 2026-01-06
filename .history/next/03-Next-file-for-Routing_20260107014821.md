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

<br />

### not-found

<br />

### route handler