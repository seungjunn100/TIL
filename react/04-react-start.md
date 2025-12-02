# 리액트 시작

- [리액트 특징](#리액트-특징)
- [JSX 문법](#jsx-문법)
- [가상(Virtual) DOM](#가상virtual-dom)
  - [가상 DOM 렌더링 과정](#가상-dom-렌더링-과정)
- [Props(속성)](#props속성)




<br />
<br />




## 리액트 특징

- React는 상태(데이터)가 변경되면 반응(랜더링)하는 방식으로 동작

- JSX 문법을 통해 HTML 작성 생산성 향상

- 가상 DOM으로 성능 저하 최소

- 컴포넌트별로 상태 관리가 용이하며, 재사용성과 유지보수성 향상

- 전역 상태 관리를 위한 라이브러리가 많음 (zustand, recoil 등)




<br />
<br />




## JSX 문법

리액트 컴포넌트 안에서는 HTML처럼 보이는 `JSX` 문법을 사용한다. 

실제로는 HTML이 아니라 자바스크립트가 이해할 수 있도록 변환되는 문법이며, 브라우저가 직접 이해하진 못한다.

- `JSX`는 `JavaScript + XML` 구조

- 브라우저가 직접 해석하지 못하므로 `Babel`이 자바스크립트 코드로 변환

  - CDN 방식으로 리액트를 사용할 경우, 스크립트에 `type="text/babel"` 설정 시 변환 가능

  ```javascript
  // JSX
  function TodoItem({ item, toggleDone, deleteItem }) {
    return (
      <li>
        <span>{ item.num }</span>  
        <span onClick={ () => toggleDone(item.num) }>
          { item.done ? <s>{ item.title }</s> : item.title }
        </span>  
        <button type="button" onClick={ () => deleteItem(item.num) }>삭제</button>
      </li>
    );
  }
  ```

  ```javascript
  // Babel 변환, JS
  function TodoItem({ item, toggleDone, deleteItem }) {
    return (
      React.createElement("li", null,
        React.createElement("span", null, item.num),
        React.createElement("span", {onClick: () => toggleDone(item.num)},
          item.done ? React.createElement("s", null, item.title) : item.title),
        React.createElement("button", {type: "button", onClick: () => deleteItem(item.num)}, "삭제")
      );
    );
  }
  ```

- `XML` 기반이라 문법이 엄격함

  - 모든 태그는 반드시 닫아야 함

  - 속성은 카멜 케이스 형태로 사용

    - `onClick`, `autoFocus` 등

- 자바스크립트 예약어로 인해 JSX에선 속성명이 바뀜

    - `class`는 `className` 사용

    - `for`는 예약어이므로 `htmlFor` 사용

- 변수를 넣거나 계산한 값을 출력하려면 자바스크립트 표현식이 필요

  - 중괄호 { } 안에서 표현식 사용 가능

- 단일 객체를 반환해야 함

  ```javascript
  // 여러 객체를 반환할 수 없음 ❌
  return (
    <h1>Todo List</h1>
    <div>...</div>
  );

  // 루트 요소 추가
  return (
    <div>
      <h1>Todo List</h1>
      <div>...</div>
    </div>
  );

  // Fragment 사용
  return (
    <Fragment>
      <h1>Todo List</h1>
      <div>...</div>
    </Fragment>
  );

  // Fragment 약어 사용
  return (
    <>
      <h1>Todo List</h1>
      <div>...</div>
    </>
  );
  ```

- `style` 속성은 객체 형태로 전달

  - 속성명은 카멜 케이스로 표기

  ```javascript
  <div style={{ backgroundColor: 'red', fontSize: '20px' }}>Hello</div>

  // 동적으로 사용
  const divStyle = {
    backgroundColor: 'red',
    fontSize: '20px',
    marginTop: '10px'
  };
  <div style={divStyle}>Hello</div>

  // 동적으로 사용
  const size = 24;
  <div style={{ color: 'red', fontSize: `${size}px` }}>Hello</div>
  ```




<br />
<br />




## 가상(Virtual) DOM

- 브라우저 `DOM`과 동일한 형태를 가진 가벼운 자바스크립트 객체 기반의 트리 구조

- 실제 `DOM`을 직접 건드리기 전에 중간 단계로 사용하는 UI의 복사본 역할

<br />

### 가상 DOM 렌더링 과정

- 상태 변경 시, 리액트가 변경된 상태를 기반으로 새로운 가상 `DOM` 생성

- 기존 가상 `DOM`과 비교(Diffing)

- 변화된 부분만 브라우저 `DOM`에 반영(Reconciliation)

- 불필요한 DOM 조작을 최소화하여 성능 최적화




<br />
<br />




## Props(속성)

- 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달할 때 Props를 사용

  - HTML 태그의 속성을 지정하는 것처럼 사용

  ```javascript
  //      App
  //       │
  //       │
  //    TodoList

  function App(){
    const list = [
      { _id: 1, title: 'React 공부', done: false},
      { _id: 2, title: 'Javascript 프로젝트', done: true},
      { _id: 3, title: 'Javascript 공부', done: true},
    ];

    return (
      <div id="app">
        <div>
          <Title title="08 Simple Todo List - React Props" />
          <TodoList list={ list } /> {/* 부모의 데이터를 자식에게 전달 */}
        </div>
      </div>
    );
  }

  function TodoList({ list }){
    const itemList = list.map(item => {
      return (
        <li key={ item._id }>{ item.title } - { item.done ? '완료' : '진행중' }</li>
      );
    });

    return (
      <ul className="todolist">
        { itemList }
      </ul>
    )
  }
  ```

- 자식 컴포넌트에서 부모 컴포넌트의 상태를 변경하려면 부모의 함수를 받아서 실행

  - **단방향(부모 → 자식)** 데이터 흐름이 유지되고 구조 예측 가능

  ```javascript
  function App() {
    const initItemList = [
      { num: 1, title: "자바스크립트 공부", done: true },
      { num: 2, title: "JS 프로젝트", done: true },
      { num: 3, title: "React 공부", done: false }
    ];

    const [ itemList, setItemList ] = Reaction.useState(initItemList);

    // 부모가 가진 상태 변경 함수들
    function addItem(title) {
      ... setItemList([ ...itemList, newItem ]);
    }

    ...
  }

  // 중간 컴포넌트(Todo)는 props를 그대로 자식에게 전달 (단방향 데이터 흐름)
  // 구조 분해 할당
  function Todo({ itemList, addItem, toggleDone, deleteItem }) {
    return Reaction.createElement(
      'div',
      { id: 'main' },
      TodoInput({ addItem }),
      TodoList({ itemList, toggleDone, deleteItem })
    );
  }

  // 자식이 부모의 상태를 변경하는 방식
  function TodoInput({ addItem }) {
    ...
      addItem(inputElem.value.trim()); // 부모 함수 호출
    ...
  }
  ```

  - 구조 분해 할당을 이용해서 필요한 속성을 바로 꺼내서 사용할 수 있음

    - 이름 기반으로 관리되므로 안정적

      - 순서 상관없이 이름만 맞으면 됨

      - 필요한 것만 선택적으로 사용 가능

    - 컴포넌트의 확장성/유지보수성/가독성을 극대화