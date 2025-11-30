# 리액트 라이브러리의 원리

- [리액트를 이해하는 과정](#리액트를-이해하는-과정)
- [주요 개념](#주요-개념)
  - [`createRoot`](#createroot)
  - [`useState`](#usestate)
  - [`props`](#props)




<br />
<br />




## 리액트를 이해하는 과정

리액트의 원리는 **상태(데이터)의 변경에 따라 반응(렌더링)하는 특징**을 갖고있다.

1. 어떤 기능을 설계한다고 가정했을 때, 보통은 HTML로 마크업을 하고 자바스크립트로 기능을 구현할 것이다.

2. 하지만 페이지에서 데이터 변화에 따라 화면을 동적으로 갱신하기 위해선, 자바스크립트로 DOM 요소를 만들고 수정하는 방식이 쓰이기 시작했다.

3. 그러면 DOM을 직접 건드리는 작업이 많아져 코드량이 늘어나고 관리가 어려워진다. 

4. 요소를 만들고, 속성을 추가하고, 요소에 자식 요소를 추가하는 반복적인 작업을 함수를 만들어 사용하면, 코드량도 줄고 유지보수가 쉬워질 수 있다.

5. UI를 생성하고 화면에 렌더링 된 후에, 나중에 데이터가 변경되어 리렌더링이 필요하거나 다른 곳에서도 사용할 수 있도록 확장 가능한 구조로 만든다.
   - 컴포넌트를 세분화하여 명확한 트리 구조를 설계할 수 있고 유지보수 측면에서 좋다.

6. 화면에 붙일 위치(rootNode)를 만들어, render 함수가 호출되면 해당 위치에 컴포넌트를 렌더링 하도록 한다.

7. `useState` 함수를 추가하여 **데이터의 변경에 따라 자동으로 전체를 리렌더링**한는 작업을 볼 수 있다.




<br />
<br />




## 주요 개념

> reaction.js
> > 리액트 라이브러리의 원리를 이해하기 위해 만들어본 라이브러리

### `createRoot`

```javascript
function App() {
  return (
    Reaction.createElement('div', { id: 'app' }, Header, Counter)
  );
}

Reaction.createRoot(document.querySelector('#root')).render(App);
```

```javascript
/* reaction.js */
let _root;        // 루트 관리용
let _stateValue;  // 상태 값 저장용

const reaction = {
  createRoot: (rootNode) => {
    let _appComponent;

    return _root = {
      render: (appFn) => {
        _appComponent = _appComponent ?? appFn;
        rootNode.firstChild?.remove();
        rootNode.appendChild(_appComponent());
      }
    };
  },
};
```

- `createRoot(dom)`를 호출하면, 

  - 그 `dom(#root)`에 렌더링할 루트 객체를 하나 만든다.

- `render(App)`이 처음 호출될 때, 

  - `_appComponent`에 `App` 함수를 저장하고, 

    - `App()`을 실행해서 나온 DOM을 `rootNode`에 붙인다.

- 이후에는 `render()`를 인자 없이 호출해도,

  - 저장해둔 `_appComponent(= App)`를 다시 실행해서 전체 UI를 다시 그린다.

<br />

### `useState`

```javascript
/* reaction.js */
let _root;        // 루트 관리용
let _stateValue;  // 상태 값 저장용

...

useState: (initValue) => {
  _stateValue = _stateValue ?? initValue;

  function setValue(newValue) {
    const oldValue = _stateValue;
    _stateValue = newValue;

    if (!Object.is(oldValue, newValue)) {
      _root.render();   // 상태가 바뀌면 리렌더링
    }
  }

  return [ _stateValue, setValue ];
},

...
```

> Object.is(a, b)
> > a와 b가 같은지 여부를 반환, 비교하는 두 값이 일치하면 true, 아니면 false
> > - a, b가 원시형 타입일 때, 값이 다를 경우 false
> >
> > - a, b가 참조형 타입일 때, 내부의 속성이 바뀌어도 참조 주소가 바뀌지 않았다면 true

- 최초 렌더링 시(App 처음 실행)

  ```javascript
  const [itemList, setItemList] = Reaction.useState(initItemList);
  ```

  - `_stateValue`가 아직 `undefined`이므로, `??` 연산자 때문에 `initValue(initItemList)`가 들어감
  
  - `itemList`는 초기 목록을 가지게 됨

- 이후 리렌더링 시

  - `_stateValue`에는 이미 이전 값이 들어 있으므로, `??` 연산자가 기존 값을 그대로 사용

  - 즉, 초기값은 딱 한 번만 쓰이고, 이후에는 항상 저장된 상태값을 재사용

- 데이터를 변경하는 함수를 통해 `setValue(newValue)` 호출 시

  ```javascript
  function addItem(title) {
    const newItemList = [...itemList];
    newItemList.push({ ... });
    setItemList(newItemList);
  }
  // 새 배열을 만드는 이유 : Object.is(a, b)로 값을 비교하기 위해
  ```

  - `oldValue`와 `newValue`를 `Object.is`로 비교

  - 값이 다르면, `_root.render()` 호출

  - `_root.render()`는 다시 `App()`을 실행 → 최신 `_stateValue`를 읽어서 새로운 UI 트리를 만들어 붙임

<br />

### `props`

- 부모 컴포넌트가 자식 컴포넌트에게 **데이터**를 전달하는 방법

- 자식이 부모의 상태를 변경하려면 부모의 함수를 받아서 실행

- **단방향(부모 → 자식)** 데이터 흐름이 유지되고 구조 예측 가능

- props를 하나의 객체 형태로 전달하는 이유

  - 데이터 흐름을 이름 기반으로 안정적
    - 이름만 맞으면 됨
    - 순서 상관없이 필요한 것만 선택적으로 사용 가능

  - 컴포넌트의 확장성/유지보수성/가독성을 극대화

  ```javascript
  // 객체 그대로 받기
  function Todo(props) {
    console.log(props.itemList);
    console.log(props.addItem);
    console.log(props.deleteItem);
  }

  // 구조 분해 할당으로 받기
  function Todo({ itemList, addItem, deleteItem }) {
    console.log(itemList);    // props. 없이 바로 사용 가능
    console.log(addItem);
    console.log(deleteItem);
  }
  ```