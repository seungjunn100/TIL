# useState

- [리액트 훅](#리액트-훅)
- [useState](#usestate-1)
  - [사용 예시](#사용-예시)




<br />
<br />




## 리액트 훅

- 2019년에 리액트 16.8 버전에서 리액트 훅이 등장하였다.

- 함수형 컴포넌트에서도 상태 관리와 생명 주기 이벤트를 사용할 수 있게 되었다.

- 함수형 컴포넌트는 순수 함수이기 때문에 기본적으로 상태 관리나 `렌더링 이후 처리(Side Effect)`를 처리할 수 없다.

  - 리액트 훅을 이용하면 가능하다.

- 클래스 컴포넌트보다 코드가 간결하고 유지보수가 용이해 함수형 컴포넌트 사용이 일반화 되었다.

- `use`로 시작하는 함수들을 `훅(Hook)`이라고 한다.

  - 이런 훅들은 컴포넌트의 루트 레벨에서만 사용 가능하다.




<br />
<br />




## useState

상태값을 추가하고 그 값이 변경되면 자동으로 리렌더링되게 하는 훅

```jsx
const [ state, setState ] = useState(initialState);
```

- `statae` : 현재 상태값 (읽기 전용)

- `setState` : 상태값을 변경하는 `setter` 함수
  
  - 상태값이 변경되면 기존 상태값과 비교하여 변경되었으면 리렌더링

- `initialState` : 컴포넌트가 처음 렌더링될 때의 초기값

<br />

### 사용 예시

```jsx
interface CounterProps {
  children: string;
}

function Counter({ children }: CounterProps) {
  console.log('\tCounter 호출됨.');

  const initCount = Number(children);

  const [ count, setCount ] = useState(initCount);

  const [ step, setStep ] = useState(1);

  // 카운트 감소
  const handleDown = () => {
    setCount(count - step);
  };

  // 카운트 증가
  const handleUp = () => {
    setCount(count + step);
  };

  // 카운트 초기화
  const handleReset = () => {
    setCount(initCount);
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

- `input`에 값을 입력시 입력된 값이 `setStep`의 인자로 전달된다.

  - `setStep` 함수 내부에서 인자로 전달된 상태값은 기존의 상태값 `step`과 비교하여 변경된걸 확인하면 리렌더링되어 `step`의 상태값이 입력된 값으로 변경된다.

- `count`의 상태값도 버튼 컴포넌트에 의해 이벤트가 동작하면, 기존의 `count` 상태값과 `step`의 상태값의 연산을 통한 값으로 `setter` 함수에 전달되어 비교하여 리렌더링되어 `count`의 상태값이 바뀌게 된다.

```jsx
function App() {
  console.log('App 호출됨.');
  return (
    <>
      <Header />
      <Counter>10</Counter>
    </>
  )
}
```

- 부모 컴포넌트에서 값을 입력하여 `props`로 전달할 수 있다.

- 자식 컴포넌트에서는 인자를 `children`이라는 변수명으로 전달 받는다.

  - `children`은 리액트에서 정해져 있는 `props` 이름이다.

  - `10`은 `JSX`의 텍스트 노드이기 때문에 `string` 타입이다.

  - `number` 타입으로 사용하려면 `{ 10 }` 표현식으로 표현해야 한다.

  - `children`을 `number` 타입으로 사용하기 위해 타입 설정을 해준다.

- 타입추론에 의해 `step`의 타입은 `number`를 갖게된다.

- 세터 함수의 인자값은 문자열로 전달되는데, 이걸 number로 바꿔주는 작업을 통해 에러 해결

```javascript
interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  // type?: 'button' | 'submit' | 'reset';
  // onClick: () => void; // 매개변수도 없고, return도 없는 함수이다라고 정의
  // children: string;
  bgColor?: string;
}

function Button({ type="button", children, bgColor, color, ...props }: ButtonProps) {
  return (
    <>
      <button 
        { ...props }
        className="rounded-button" 
        type={ type }
        style={{ ...props.style, backgroundColor: bgColor, color }}
      >
        { children }
      </button>
    </>
  );
}
```

- 리액트에서 버튼에 들어올 수 있는 모든 속성들을 타입으로 상속받아 사용할 수 있다.

- 컴포넌트에서 속성을 선언해서 사용할 때, 타입에 정의 했던 타입을 주석처리해도 리액트 내에서 모든 속성들을 상속받고있기 때문에 에러가 발생하지 않는다.

- 기본값을 설정하거나 명시적으로 `props`를 선언하는거 말고 나머지는 `나머지 매개변수(...props)`에 의해 컴포넌트에서 모든 속성들을 사용할 수 있다.

- `{...props}`를 맨 앞에 두어 명시적으로 정의한 `props`보다 먼저 적용이 되고 명시적으로 정의한 `props`가 있다면 덮어씌어질 수 있게 작업을해주어야 한다.