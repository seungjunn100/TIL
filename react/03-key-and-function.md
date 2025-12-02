# 리스트 렌더링과 함수 전달 방식의 차이

- [리스트 렌더링과 `key props`](#리스트-렌더링과-key-props)
- [이벤트 핸들러에서 함수 전달 방식의 차이](#이벤트-핸들러에서-함수-전달-방식의-차이)




<br />
<br />




## 리스트 렌더링과 `key props`

리액트에서 배열을 렌더링할 때는 반드시 `key`를 지정해야 한다.

```javascript
// JavaScript
itemList.map(item => (
  <TodoItem key={item.num} item={item} />
))
```

```html
<!-- HTML -->
<ul class="todolist">
  <li>
    <span>1</span>
    <span><s>자바스크립트 공부</s></span>
    <button type="button">삭제</button>
  </li>
  <li>
    <span>2</span>
    <span><s>JS 프로젝트</s></span>
    <button type="button">삭제</button>
  </li>
  <li>
    <span>3</span>
    <span>React 공부</span>
    <button type="button">삭제</button>
  </li>
</ul>
```

- 리액트가 `DOM` 변경을 효율적으로 추적하기 위해 필요

- 내부적으로 식별하기 위해 사용되며, `props` 용도로 사용하지 않음

- 고유한 `key`가 없으면 어떤 요소가 변경·추가·삭제된 것인지 판단하기 어려움

  - 만약 `TodoItem`인 `li` 요소에 `key`가 없으면, 어떤 `li` 요소가 변경되었는지 판단하기 어려움




<br />
<br />




## 이벤트 핸들러에서 함수 전달 방식의 차이

```javascript
function Todo() {
  /* ... */
  function toggleDone(num) {
    const newItemList = itemList.map(
      item => item.num === num ? { ...item, done: !item.done } : item
    );

    setItemList(newItemList);
  }
  /* ... */
  return (
    /* ... */
  );
}

function TodoItem({ item, toggleDone, deleteItem }) {
  return (
    {/* ... */}
      <span onClick={ () => toggleDone(item.num) }> 
    {/* ... */}
  );
}
```

```javascript
<span onClick={ toggleDone(item.num) }>
```

- 렌더링 시점에 `toggleDone(item.num)`가 즉시 실행됨

- `onClick`에는 `toggleDone`의 리턴값 `undefined`가 들어감
  
  - `toggleDone()` 함수는 `return` 값이 없으므로..

- 클릭 시 실행할 함수가 없어 에러 발생

```javascript
<span onClick={ toggleDone }>
```

- 특정 항목을 토글하려면 특정 항목의 값(`item.num`)이 전달되어야 함

- 리액트가 내부적으로 `toggleDone(event)`를 호출

```javascript
<span onClick={ () => toggleDone(item.num) }>
```

- 렌더링 시 실행되지 않음

- 특정 항목의 값(`item.num`)을 전달할 수 있음

- 클릭할 때만 함수가 실행됨