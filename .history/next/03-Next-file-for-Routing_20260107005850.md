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

<br />

### error

<br />

### not-found

<br />

### route handler