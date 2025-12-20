# 리액트 라우터의 동작 원리

- [라우팅이란](#라우팅이란)
  - [전통적인 웹 방식](#전통적인-웹-방식)
  - [리액트(SPA) 방식](#리액트spa-방식)
- [리액트 라우터란](#리액트-라우터란)
  - [리액트 라우터 모드](#리액트-라우터-모드)
- [예제로 보는 라우팅 동작 구현](#예제로-보는-라우팅-동작-구현)




<br />
<br />




## 라우팅이란

URL 변경에 따라 어떤 페이지를 보여줄지 결정하는 방식이다.

<br />

### 전통적인 웹 방식

서버가 페이지 이동을 담당한다.

#### 최초 웹 서버 접속

- 브라우저가 웹 서버에 `HTML` 문서 요청

- 서버는 요청을 처리한 뒤 완성된 `HTML` 응답

- 브라우저는 `HTML`을 파싱

- 필요한 리소스(`CSS`, `JS`, 이미지 등)를 추가로 서버에 요청

- 모든 리소스를 받아 화면 렌더링

#### 페이지 이동

- 사용자가 링크 클릭

- 현재 화면이 초기화 (새로고침)

- 다시 서버에 `HTML` 요청 (위 과정 반복)

- 주소창 `URL` 변경

- 이전 `URL`은 브라우저 히스토리에 저장

- 브라우저 기본 기능으로 뒤로/앞으로 이동 가능

<br />

### 리액트(SPA) 방식

클라이언트가 페이지 이동을 담당한다.

#### 최초 웹 서버 접속

- 브라우저가 웹 서버에 `HTML` 요청

- 서버는 빈 초기 페이지(`index.html`) 응답

- 브라우저가 `HTML` 파싱

- `JS`, `CSS` 등 리소스를 다운로드

- 자바스크립트가 화면을 직접 렌더링

#### 페이지 이동

- 사용자가 링크 클릭

- 자바스크립트가 주소창 `URL` 변경

- 이미 다운로드된 자바스크립트로 `URL`에 매칭되는 새로운 컴포넌트 렌더링

- 브라우저 히스토리 관리도 자바스크립트로 직접 구현




<br />
<br />




## 리액트 라우터란

- 리액트 기반의 라우팅 라이브러리

- `URL`에 따라 어떤 화면(컴포넌트)을 보여줄지 결정해주는 클라이언트 라우팅 기능을 제공

- 리액트 라우터는 리액트의 공식 라우터가 아닌 서드파티 라이브러리

- 리액트는 `UI`를 그리는 데만 집중하는 라이브러리이기 때문에

  - 페이지 이동, `URL` 관리 같은 라우팅 기능을 자체적으로 제공하지 않는다.

- 리액트 라우터를 사용하면

  - `URL`이 바뀔 때 새 `HTML`을 요청하지 않고

  - 이미 다운로드된 자바스크립트로 해당 `URL`에 맞는 컴포넌트를 렌더링할 수 있다.

<br />

### 리액트 라우터 모드

#### Declarative Mode (선언적 방식)

- 가장 기본적인 라우팅 방식

- `<BrowserRouter>`, `<Routes>`, `<Route>` 사용

- URL에 맞는 컴포넌트를 렌더링하는 것에 초점

<br />

#### Data Mode

- 라우팅 + 데이터 로딩 + 액션 처리까지 포함

- `createBrowserRouter`, `loader`, `action` 사용

- 화면 진입 전에 데이터를 불러오고, 폼 요청도 라우트 단위로 처리

- 라우팅과 데이터 페칭을 하나의 흐름으로 다룸

<br />

#### Framework Mode

- 파일 시스템 기반 라우팅

- 타입 안전성 강화

- 프레임워크에 가까운 사용 방식

<br />

#### Data Mode와 Next.js

- `Data Mode`에서 사용하는 `loader`와 `action` 개념은
`Next.js`의 데이터 페칭과 `Server Actions`와 사고 방식이 매우 유사하다.

- `Next.js`는 `SSR` 방식인데 `Data Mode`는 `SSR`과 유사한 데이터 흐름을 개념적으로 이해 할 수 있다.

- `Data Mode`를 이해하면

  - 라우팅과 데이터 페칭의 관계를 구조적으로 이해할 수 있고

  - 클라이언트와 서버의 역할 분리를 이해할 수 있으며

  - 이후 Next.js의 데이터 흐름을 이해하기 수월해진다.




<br />
<br />




## 예제로 보는 라우팅 동작 구현

### 전통적인 웹 페이지 이동

```jsx
function Header() {
  return (
    <>
      <header>
        <h1>리액트 라우터 - 01 클라이언트 라우팅 직접 구현 - SPA</h1>
        <a className="menu-dark" href="/home">home</a>
        <br/>
        <a className="menu" href="/page1">page1</a>
        <br/>
        <a className="menu" href="/page2">page2</a>
      </header>
    </>
  )
}
```

- 전통적인 웹의 페이지 이동은 링크를 클릭시 해당 링크로 이동한다.

- 새로고침이 발생하며 서버에 다시 `HTML` 문서를 요청하고 응답 받는다.

- `HTML` 코드를 파싱하며 필요한 리소스를 다시 서버에 추가 요청하여 렌더링한다.

- 이러한 방식을 아래와 같이 `SPA` 방식으로 바꿀 수 있다.

<br />

### 리액트(SPA) 웹 페이지 이동

#### Header 컴포넌트

```jsx
function Header() {
  return (
    <>
      <header>
        <h1>리액트 라우터 - 01 클라이언트 라우팅 직접 구현 - SPA</h1>
        <MyLink className="menu-dark" to="/home">home</MyLink>
        <br/>
        <MyLink className="menu" to="/page1">page1</MyLink>
        <br/>
        <MyLink className="menu" to="/page2">page2</MyLink>
      </header>
    </>
  )
}
```

#### MyLink 컴포넌트

```jsx
function MyLink({ children, to, ...props }: MyLinkProps) {
  const handleClick = (e: React.MouseEvent<HTMLAnchorElement>) => {
    // 브라우저 기본 동작 취소
    e.preventDefault();

    // Histroy API를 사용해서 URL 변경하고 history에 쌓는다.
    window.history.pushState(null, '', e.currentTarget.href);

    // dispatchEvent : 이벤트를 수동으로 발생
    // PopStateEvent : 브라우저의 뒤로, 앞으로 가기 등의 이벤트를 생성
    window.dispatchEvent(new PopStateEvent('popstate'));
  };

  return (
    <a { ...props } href={to} onClick={handleClick}>{ children }</a>
  );
}
```

- `<a>` 태그를 클릭했을 때 브라우저의 기본 동작(페이지 이동, 새로고침)을 취소한다.

- `History API`를 이용하여 `URL`을 변경하고 `history`에 남긴다.

- 수동으로 직접 `popstate` 이벤트를 발생시킨다.

#### App 컴포넌트

```jsx

```