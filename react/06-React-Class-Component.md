# 클래스 컴포넌트

- [클래스 컴포넌트](#클래스-컴포넌트란)
  - [클래스 컴포넌트를 만드는 방법](#클래스-컴포넌트를-만드는-방법)
  - [클래스 방식의 상태관리](#클래스-방식의-상태관리)




<br />
<br />




## 클래스 컴포넌트란

- 리액트가 나오기 전에는 클래스로 컴포넌트를 정의하였다.

- 하지만 2019년에 리액트 16.8 버전에서 리액트 훅이 등장하면서 함수형 컴포넌트 방식을 사용하게 되었다.

- 현재는 함수의 컴포넌트와 훅을 사용하는 것을 권장하지만, 기본에 작업된 코드나 특정 상황에서 사용된다.

<br />

### 클래스 컴포넌트를 만드는 방법

```javascript
import { Component } from "react";

class ClickMe extends Component {
  render() {
    return (
      <div>
        <h1>01 클래스 컴포넌트</h1>
        <div>
          클릭 횟수 X 1: 0
          <button>클릭</button>
        </div>
      </div>
    );
  }
}
```

- `Component`를 상속 받는다.

- `render()` 메서드를 작성한다.

- 리액트내에서 `new` 연산자를 통해 컴포넌트(인스턴스)를 생성한다.

```javascript
class App extends Component {
  render() {
    return (
      <>
        <div>
          <h1>01 클래스 컴포넌트</h1>
          <ClickMe level={ 2 } />
          <ClickMe level={ 3 } />
        </div>
      </>
    )
  };
}
```
```javascript
import { Component } from "react";

interface ClickMeProps {
  level: number;
}

class ClickMe extends Component<ClickMeProps> {
  render() {
    return (
      <div>
        <h1>01 클래스 컴포넌트</h1>
        <div>
          클릭 횟수 X { this.props.level }: 0
          <button>클릭</button>
        </div>
      </div>
    );
  }
}
```

- 부모로부터 `props`를 객체로 전달 받는다.

- `this`를 통해 해당 인스턴스(컴포넌트)의 `props`를 전달 받는다.

- 자식 컴포넌트는 부모로부터 받은 `props`를 직접 수정할 수 없다.

  - 리액트는 단방향 데이터 흐름의 규칙을 갖고있기 때문이다.

  - 데이터는 부모에서 자식으로만 흐른다.

  - 자식에서 `props` 데이터의 변경이 필요하면 부모에게 요청하거나 `state`로 관리해야 한다.

<br />

### 클래스 방식의 상태관리

```javascript
// State의 타입 정의
interface ClickMeState {
  count: number;
}

class ClickMe extends Component<ClickMeProps, ClickMeState> {
  state = { count: 0 };

  increment() {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <div>
        <h1>01 클래스 컴포넌트</h1>
        <div>
          { this.state.count } X { this.props.level }: 0
          <button>클릭</button>
        </div>
      </div>
    );
  }
}
```

- 클래스 컴포넌트는 `React.Component`를 상속받기 때문에 `state`, `setState()` 기능을 사용할 수 있다.

- 클래스에서는 상태를 여러 개 변수로 사용할 수 없고 `state`의 객체 안에 여러개의 상태를 넣어 관리해야 한다.

- `setState()` 함수의 `this`는 `undefined`가 되어 타입에러가 발생한다.

  - 클래스 내부는 기본적으로 엄격 모드가 적용된다.

  - 클래스의 메서드는 자동으로 `this`가 바인딩 되지 않는다.

    > 바인딩
    > > `this`가 어떤 객체를 가리킬지 결정하는 행위

  - 이런 상태에서 함수를 직접 호출하면 `this`는 `undefined`가 된다.


```javascript
class ClickMe extends Component<ClickMeProps> {
  state = { count: 0 };

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <div>
        <h1>01 클래스 컴포넌트</h1>
        <div>
          { this.state.count } X { this.props.level }: 0
          <button onClick={ this.increment }>클릭</button>
        </div>
      </div>
    );
  }
}
```

- 화살표 함수로 메서드를 정의하면 에러를 해결할 수 있다.

  - 화살표 함수는 자체적으로 `this`를 생성하지 않고 상위 스코프의 `this`를 그대로 가져온다.

- 이벤트 핸들러는 `this` 바인딩을 위해 화살표 함수로 작성하는 편함

```javascript
class ClickMe extends Component<ClickMeProps, ClickMeState> {
  constructor(props: ClickMeProps) {
    super(props);

    // props를 이용해서 state를 초기화 해야할 경우 constructor에서 수행
    this.state = { count: props.level };

    // 이벤트 핸들러를 일반 함수로 작성할 경우 this.props, this.state에 접근하기 위해서 this 바인딩
    this.increment = this.increment.bind(this);
  }

  increment() {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    const result = this.state.count * this.props.level;

    return (
      <div>
        { this.state.count } X { this.props.level }: { result }
        <button onClick={ this.increment }>클릭</button>
      </div>
    );
  }
}
```

- 또는 생성자를 통해 바인딩하여 에러를 해결할 수 있다.

- `super(props)`가 있어야 `state` 초기화나 메서드 바인딩에서 `this` 활용이 가능해진다.