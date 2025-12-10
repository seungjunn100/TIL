# useReducer

- [useReducer](#usereducer-1)
  - [사용예시](#사용-예시)
  - [useReducer를 흉내내본 커스텀 훅](#usereducer를-흉내내본-커스텀-훅)
  - [useState와 차이점](#usestate와-차이점)




<br />
<br />




## useReducer

`useState`와 비슷하지만, 복잡한 상태 변경 로직을 하나의 `reducer` 함수로 다루는 훅

```jsx
const [state, dispatch] = useReducer(reducer, initialArg, init?);
```

- `state` : 현재 상태값

- `dispatch(action)` : 상태값을 변경하는 `setter` 함수

- `reducer` : `state`와 `action`을 인자로 받아 새로운 `state`를 반환하는 함수

- `initialArg` : 초기값

- `init`(선택) : `initialArg`를 인자로 받고 리턴한 값이 초기 상태로 지정되는 함수

```jsx
function reducer(state, action) { }
```

`state`와 `action`을 인자로 받아 새로운 `state`를 반환하는 `순수 함수(Pure Function)`

- `state` : 현재 상태값

- `action` : 동작을 정의한 객체

  - 자유롭게 작성, 일반적으로 `type` 속성에 동작을, `value` 속성에 값을 지정

<br />

### 사용 예시

#### 컴포넌트

```jsx
function Counter({ children }: CounterProps) {
  const initCount = Number(children);

  const [ count, countDispatch ] = useReducer(counterReducer, initCount);

  const [ step, setStep ] = useState(1);

  // 카운트 감소
  const handleDown = () => {
    countDispatch({ type: 'DOWN', value: step });
  };

  // 카운트 증가
  const handleUp = () => {
    countDispatch({ type: 'UP', value: step });
  };

  // 카운트 초기화
  const handleReset = () => {
    countDispatch({ type: 'RESET', value: initCount });
  };

  return (
    <div id="counter">
      <label htmlFor="step">증감치</label>
      <input id="step" type="number" value={ step } onChange={ (e) => setStep(Number(e.target.value)) } />
      <Button bgColor="red" color="black" onClick={ handleDown }>-_-</Button>
      <Button bgColor="gray" onClick={ handleReset }>0_0</Button>
      <Button onClick={ handleUp }>+_+</Button>
      <span>{ count }</span>
    </div>
  );
}
```

![useReducer-1](../src/images/useReducer-1.png)

- `useState`로 상태를 관리하던걸 `useReducer`로 변경하는 과정이다.

- 특정 동작을 `type`으로 지정하고 특정 값을 `value`에 전달한다.

#### reducer 함수

```jsx
export interface CounterAction {
  type: 'UP' | 'DOWN' | 'RESET';
  value: number;
}

export function counterReducer(state: number, action: CounterAction) {
  let newState = state;

  // 값이 명확하게 정해져있으면 switch 문법을 사용하는게 좋다.
  switch(action.type) {
    case 'UP':
      newState = state + action.value;
      break;
    case 'DOWN':
      newState = state - action.value;
      break;
    case 'RESET':
      newState = action.value;
      break;
    default:
      break;
  }

  // 테스트
  console.log(`${state} ${action.type} ${action.value} -> ${newState}`); // 5 UP 3 -> 8

  return newState;
}

// 테스트
console.log(counterReducer(5, { type: 'UP', value: 3 }) === 8); // true
```

- 특정 동작을 하는 함수의 기능들을 `reducer` 함수에 구현하여 생성한다.

- `countDispatch`의 인자인 `action`에 `type`과 `value`를 객체로 전달받는다.

  - 리액트 내부에서 `counterReducer(state, { type: ..., value: ... })` 형태로 `reducer` 함수를 호출한다.

- 특정 동작 함수가 발생하면 위의 방식처럼 `reducer` 함수가 호출된다.

- `state`인 현재 값과 전달받은 `value`에 의해 `tpye`에 따라 계산되어 새로운 `상태값(state)`을 `return`한다.

- 이전 상태값과 새로운 상태값을 비교하여 값이 변경되어 리렌더링된다.

<br />

### useReducer를 흉내내본 커스텀 훅

`useState` 훅을 사용해 `useReducer`의 내부 메커니즘을 흉내내본 커스텀 훅

```tsx
function useMyReducer(reducer: (state: number, action: CounterAction) => number, initValue: number){
  const [ state, setState ] = useState(initValue);

  function dispatch(action: CounterAction){
    const newState = reducer(state, action);
    setState(newState);
  }

  return [ state, dispatch ] as const;
}
```

- `reducer` 인자 : `state`와 `action`을 인자로 받는 `reducer` 함수로 상태값을 `number` 타입으로 `return`한다.

- `initValue` 인자 : 초기값

- `useState`에 의해 `상태값(state)`과 상태값을 비교후 리렌더링해줄 `setState` 함수를 `return`받는다.

- `dispatch` 함수를 정의한다. 
  
  - `reducer` 함수는 `state`, `action`을 인자로 받고 함수가 실행되면 새로운 `상태값(newState)`을 `return`하고, 새로운 상태값을 인자로 받아 `setState` 함수가 실행되는 함수를 정의해놓았다.

- 변경된 `상태값(state)`과 `dispatch` 함수를 `return`한다.

- `dispatch` 함수가 실행되면 `reducer` 함수에 의해 새로운 상태값을 `setState` 함수의 인자로 받아 실행되어 값의 변경이 있으면 리렌더링하게 된다.

<br />

### useState와 차이점

- 컴포넌트 외부에서 상태 관리가 가능하다.

- 여러 컴포넌트가 유사한 상태 관련 로직을 사용할 경우, `reducer` 함수에 공통으로 작성해서 사용할 수 있다.

- `useState`를 사용해 상태 변경 로직이 복잡해지면 `useReducer`에 상태 변경 로직을 집중시키고 컴포넌트를 분리하여 사용할 수 있다.

- `useReducer`는 상태 변경 로직이 한 곳에 있기 때문에 디버깅이 편하다.

- `reducer` 함수는 컴포넌트와 독립적인 순수 함수이기 때문에 따로 테스트가 가능하다.