# 리액트 라이브러리의 원리를 이해하는 과정

- [HTML + JavaScript](#html--javascript)
- [HTML 대신 JavaScript로 UI 구성](#html-대신-javascript로-ui-구성)
- [UI를 생성하는 함수를 만들어 사용](#ui를-생성하는-함수를-만들어-사용)
- [생성한 UI를 랜더링하는 함수](#생성한-ui를-랜더링하는-함수)
- [상태(데이터) 변경시 자동으로 리렌더링](#상태데이터-변경시-자동으로-리렌더링)




<br />
<br />




## HTML + JavaScript

예를 들어 카운트 기능을 설계한다고 가정했을 때, 보통은 HTML로 마크업을 하고 자바스크립트로 기능을 구현할 것이다.

```html
<div id="app">
  <header>
    <h1>Counter - 01 HTML + JS</h1>
    <p>파일 경로: <span id="filepath"></span></p>
  </header>
  <div id="counter">
    <button type="button" onclick="handleDown()">-</button>
    <button type="button" onclick="handleReset(event)">0</button>
    <button type="button" onclick="handleUp()">+</button>
    <span>0</span>
  </div>
</div>
```

```javascript
let count = 0; // 상태, 전역 변수

// 카운터 감소
const handleDown = () => {
  // 데이터 갱신, count 값 감소
  count--;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};

// 카운터 증가
const handleUp = () => {
  // 데이터 갱신, count 값 감소
  count++;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};

// 카운터 초기화
const handleReset = event => {
  // 데이터 갱신, count 값 초기화
  count = 0;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};
```




<br />
<br />




## HTML 대신 JavaScript로 UI 구성

페이지에서 데이터 변화에 따라 화면을 동적으로 갱신하기 위해선, 자바스크립트로 DOM 요소를 만들고 수정하는 방식이 쓰이기 시작했다.

```javascript
// <h1>Counter - 02 HTML 대신 JS로 UI 구성</h1>
const h1 = document.createElement('h1');
const h1Txt = document.createTextNode('Counter - 02 HTML 대신 JS로 UI 구성');
h1.appendChild(h1Txt);

// <p>파일 경로: <span id="filepath"></span></p>
const span1 = document.createElement('span');
span1.setAttribute('id', 'filepath');
const p = document.createElement('p');
const pTxt = document.createTextNode('파일 경로: ');
p.appendChild(pTxt);
p.appendChild(span1);

// <header></header>
const header = document.createElement('header');
header.appendChild(h1);
header.appendChild(p);

// <button type="button" onclick="handleDown()">-</button>
const button1 = document.createElement('button');
const button1Txt = document.createTextNode('-');
button1.setAttribute('type', 'button');
button1.setAttribute('onclick', 'handleDown()');
button1.appendChild(button1Txt);

// <button type="button" onclick="handleReset(event)">0</button>
const button2 = document.createElement('button');
const button2Txt = document.createTextNode('0');
button2.setAttribute('type', 'button');
button2.setAttribute('onclick', 'handleReset(event)');
button2.appendChild(button2Txt);

// <button type="button" onclick="handleUp()">+</button>
const button3 = document.createElement('button');
const button3Txt = document.createTextNode('+');
button3.setAttribute('type', 'button');
button3.setAttribute('onclick', 'handleUp()');
button3.appendChild(button3Txt);

// <span>0</span>
const span2 = document.createElement('span');
const span2Txt = document.createTextNode(0);
span2.appendChild(span2Txt);

// <div id="counter"></div>
const counter = document.createElement('div');
counter.setAttribute('id', 'counter');
counter.appendChild(button1);
counter.appendChild(button2);
counter.appendChild(button3);
counter.appendChild(span2);

// <div id="app"></div>
const app = document.createElement('div');
app.setAttribute('id', 'app');
app.appendChild(header);
app.appendChild(counter);

// root 요소에 app 추가
document.querySelector('#root').appendChild(app);
```

```javascript
let count = 0; // 상태, 전역 변수

// 카운터 감소
const handleDown = () => {
  // 데이터 갱신, count 값 감소
  count--;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};

// 카운터 증가
const handleUp = () => {
  // 데이터 갱신, count 값 감소
  count++;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};

// 카운터 초기화
const handleReset = event => {
  // 데이터 갱신, count 값 초기화
  count = 0;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};
```




<br />
<br />




## UI를 생성하는 함수를 만들어 사용

DOM을 직접 건드리는 작업이 많아져 코드량이 늘어나고 관리가 어려워진다. 

요소를 만들고, 속성을 추가하고, 요소에 자식 요소를 추가하는 반복적인 작업을 함수를 만들어 사용하면 코드량도 줄고 유지보수가 쉬워질 수 있다.

**reaction.js**

```javascript
const reaction = {
  // tag: 요소
  // props: 속성 목록
  // children: 자식으로 받는 노드들이 하나 이상일 수 있어서 배열로 받음
  createElement: (tag, props, ...children) => {
    // 요소 노드 생성
    const elem = document.createElement(tag);

    // 속성 추가
    if (props) {
      // 객체안에 속성이 1개 이상일 때 for in 문
      for (const attrName in props) {
        const value = props[attrName];
        elem.setAttribute(attrName, value);
      }
    }

    // 자식 노드 추가
    for (let child of children) { 
      // 문자열일 경우와 태그일 때를 구분 지어줘야한다.
      if (typeof child === 'string' || typeof child === 'number') {
        child = document.createTextNode(child); 
      }
      elem.appendChild(child); // 태그는 그대로 추가하도록..
    }

    // 요소 노드 반환
    return elem;
  }
};

export default reaction;
```

```javascript
import Reaction from './reaction.js';

// <h1>Counter - 03 createElement() 함수 만들기</h1>
const h1 = Reaction.createElement('h1', null, 'Counter - 03 createElement() 함수 만들기');

// <p>파일 경로: <span id="filepath"></span></p>
const span1 = Reaction.createElement('span', { id: 'filepath' });
const p = Reaction.createElement('p', null, '파일 경로: ', span1);

// <header></header>
const header = Reaction.createElement('header', null, h1, p);

// <button type="button" onclick="handleDown()">-</button>
const button1 = Reaction.createElement('button', { type: 'button', onclick: 'handleDown()' }, '-');

// <button type="button" onclick="handleReset(event)">0</button>
const button2 = Reaction.createElement('button', { type: 'button', onclick: 'handleReset(event)' }, 0);

// <button type="button" onclick="handleUp()">+</button>
const button3 = Reaction.createElement('button', { type: 'button', onclick: 'handleUp()' }, '+');

// <span>0</span>
const span2 = Reaction.createElement('span', null, 0);

// <div id="counter"></div>
const counter = Reaction.createElement('div', { id: 'counter' }, button1, button2, button3, span2);

// <div id="app"></div>
const app = Reaction.createElement('div', { id: 'app' }, header, counter);

// root 요소에 app 추가
document.querySelector('#root').appendChild(app);
```

코드량을 줄이고 전체 구조가 한번에 보이도록 UI 구조를 트리 형태로 표현하여, 컴포넌트 형태로 구성할 수 있다.

```javascript
import Reaction from './reaction.js';

const App = 
  Reaction.createElement('div', { id: 'app' }, 
    Reaction.createElement('header', null, 
      Reaction.createElement('h1', null, 'Counter - 04 createElement() 함수 하나로 통합'), 
      Reaction.createElement('p', null, '파일 경로: ', 
        Reaction.createElement('span', { id: 'filepath' }))), 
    Reaction.createElement('div', { id: 'counter' }, 
      Reaction.createElement('button', { type: 'button', onclick: 'handleDown()' }, '-'), 
      Reaction.createElement('button', { type: 'button', onclick: 'handleReset(event)' }, 0), 
      Reaction.createElement('button', { type: 'button', onclick: 'handleUp()' }, '+'), 
      Reaction.createElement('span', null, 0)));

// root 요소에 App 추가
document.querySelector('#root').appendChild(App);
```

```javascript
let count = 0; // 상태, 전역 변수

// 카운터 감소
const handleDown = () => {
  // 데이터 갱신, count 값 감소
  count--;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};

// 카운터 증가
const handleUp = () => {
  // 데이터 갱신, count 값 감소
  count++;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};

// 카운터 초기화
const handleReset = event => {
  // 데이터 갱신, count 값 초기화
  count = 0;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};
```




<br />
<br />




## 생성한 UI를 랜더링하는 함수

UI를 생성하고 화면에 렌더링 된 후에, 나중에 데이터가 변경되면 재렌더링이 필요하거나 다른 곳에서도 사용할 수 있도록 확장 가능한 구조로 만든다.

**reaction.js**

```javascript
const reaction = {
  // tag: 요소
  // props: 속성 목록
  // children: 자식으로 받는 노드들이 하나 이상일 수 있어서 배열로 받음
  createElement: (tag, props, ...children) => {
    // 요소 노드 생성
    const elem = document.createElement(tag);

    // 속성 추가
    if (props) {
      // 객체안에 속성이 1개 이상일 때 for in 문
      for (const attrName in props) {
        const value = props[attrName];
        elem.setAttribute(attrName, value);
      }
    }

    // 자식 노드 추가
    for (let child of children) { 
      // 문자열일 경우와 태그일 때를 구분 지어줘야한다.
      if (typeof child === 'string' || typeof child === 'number') {
        child = document.createTextNode(child); 
      }
      elem.appendChild(child); // 태그는 그대로 추가하도록..
    }

    // 요소 노드 반환
    return elem;
  },
  createRoot: (rootNode) => { // 루트 노드를 관리하는 객체를 반환
    return {
      render: (appFn) => { // appFn을 실행한 결과 노드를 루트 노드의 자식으로 랜더링
        rootNode.appendChild(appFn());
      }
    };
  },
};

export default reaction;
```

```javascript
import Reaction from './reaction.js';

function App() {
  return (
    Reaction.createElement('div', { id: 'app' }, 
      Reaction.createElement('header', null, 
        Reaction.createElement('h1', null, 'Counter - 05 createRoot(), render() 함수 만들기'), 
        Reaction.createElement('p', null, '파일 경로: ', 
          Reaction.createElement('span', { id: 'filepath' }))), 
      Reaction.createElement('div', { id: 'counter' }, 
        Reaction.createElement('button', { type: 'button', onclick: 'handleDown()' }, '-'), 
        Reaction.createElement('button', { type: 'button', onclick: 'handleReset(event)' }, 0), 
        Reaction.createElement('button', { type: 'button', onclick: 'handleUp()' }, '+'), 
        Reaction.createElement('span', null, 0)))
  );
}

// root 요소에 App 추가
Reaction.createRoot(document.querySelector('#root')).render(App);
```

```javascript
let count = 0; // 상태, 전역 변수

// 카운터 감소
const handleDown = () => {
  // 데이터 갱신, count 값 감소
  count--;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};

// 카운터 증가
const handleUp = () => {
  // 데이터 갱신, count 값 감소
  count++;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};

// 카운터 초기화
const handleReset = event => {
  // 데이터 갱신, count 값 초기화
  count = 0;

  // 화면 갱신, count 값 화면에 표시
  document.querySelector('#counter > span').textContent = count;
};
```

컴포넌트를 세분화하여 명확한 트리 구조를 설계할 수 있고 유지보수 측면에서 좋다.

**reaction.js**

```javascript
const reaction = {
  // tag: 요소
  // props: 속성 목록
  // children: 자식으로 받는 노드들이 하나 이상일 수 있어서 배열로 받음
  createElement: (tag, props, ...children) => {
    // 요소 노드 생성
    const elem = document.createElement(tag);

    // 속성 추가
    if (props) {
      // 객체안에 속성이 1개 이상일 때 for in 문
      for (const attrName in props) {
        const value = props[attrName];
        if (attrName.toLowerCase().startsWith('on')) { // 해당 속성의 글자가 on 으로 시작할 경우
          elem.addEventListener(attrName.toLowerCase().substring(2), value);
        }
        elem.setAttribute(attrName, value);
      }
    }

    // 자식 노드 추가
    for (let child of children) {
      // 문자열일 경우와 태그일 때를 구분 지어줘야한다.
      if (typeof child === 'string' || typeof child === 'number') {
        child = document.createTextNode(child);
      } else if (typeof child === 'function') {
        child = child();
      }
      elem.appendChild(child); // 태그는 그대로 추가하도록..
    }

    // 요소 노드 반환
    return elem;
  },
  createRoot: (rootNode) => { // 루트 노드를 관리하는 객체를 반환
    return {
      render: (appFn) => { // appFn을 실행한 결과 노드를 루트 노드의 자식으로 랜더링
        rootNode.appendChild(appFn());
      }
    };
  },
};

export default reaction;
```

```javascript
import Reaction from './reaction.js';

// Header 컴포넌트
function Header() {
  return (
    Reaction.createElement('header', null, 
      Reaction.createElement('h1', null, 'Counter - 06 UI 구성 요소별 각각의 함수로 분리(컴포넌트로 만들기)'), 
      Reaction.createElement('p', null, '파일 경로: ', 
        Reaction.createElement('span', null, `ch${document.URL.split('/ch')[1]}index.html`)))
  );
}

// Counter 컴포넌트
function Counter() {
  let count = 0; // 상태, 전역 변수

  // 카운터 감소
  const handleDown = () => {
    // 데이터 갱신, count 값 감소
    count--;

    // 화면 갱신, count 값 화면에 표시
    document.querySelector('#counter > span').textContent = count;
  };

  // 카운터 증가
  const handleUp = () => {
    // 데이터 갱신, count 값 감소
    count++;

    // 화면 갱신, count 값 화면에 표시
    document.querySelector('#counter > span').textContent = count;
  };

  // 카운터 초기화
  const handleReset = event => {
    console.log(event);

    // 데이터 갱신, count 값 초기화
    count = 0;

    // 화면 갱신, count 값 화면에 표시
    document.querySelector('#counter > span').textContent = count;
  };

  return (
    Reaction.createElement('div', { id: 'counter' }, 
      Reaction.createElement('button', { type: 'button', onclick: handleDown }, '-'), 
      Reaction.createElement('button', { type: 'button', onclick: handleReset }, 0), 
      Reaction.createElement('button', { type: 'button', onclick: handleUp }, '+'), 
      Reaction.createElement('span', null, count))
  );
}

// App 컴포넌트
function App() {
  return (
    Reaction.createElement('div', { id: 'app' }, Header, Counter)
  );
}

// root 요소에 App 추가
Reaction.createRoot(document.querySelector('#root')).render(App);
```




<br />
<br />




## 상태(데이터) 변경시 자동으로 리렌더링

리액트의 원리는 상태(데이터)의 변경에 따라 반응(렌더링)하는 특징을 갖고있다.

**reaction.js**

```javascript
let _stateValue; // _ <- 내부에서만 사용할 변수이다.
let _root;

const reaction = {
  // tag: 요소
  // props: 속성 목록
  // children: 자식으로 받는 노드들이 하나 이상일 수 있어서 배열로 받음
  createElement: (tag, props, ...children) => {
    // 요소 노드 생성
    const elem = document.createElement(tag);

    // 속성 추가
    if (props) {
      // 객체안에 속성이 1개 이상일 때 for in 문
      for (const attrName in props) {
        const value = props[attrName];
        if (attrName.toLowerCase().startsWith('on')) { // 해당 속성의 글자가 on 으로 시작할 경우
          elem.addEventListener(attrName.toLowerCase().substring(2), value);
        }
        elem.setAttribute(attrName, value);
      }
    }

    // 자식 노드 추가
    for (let child of children) {
      // 문자열일 경우와 태그일 때를 구분 지어줘야한다.
      if (typeof child === 'string' || typeof child === 'number') {
        child = document.createTextNode(child); 
      } else if (typeof child === 'function') {
        child = child();
      }
      elem.appendChild(child); // 태그는 그대로 추가하도록..
    }

    // 요소 노드 반환
    return elem;
  },
  // 루트 노드를 관리하는 객체를 반환
  createRoot: (rootNode) => {
    let _appComponent;

    return _root = {
      render: (appFn) => {
        console.log(appFn ? 'Reaction: 최초 렌더링' : 'Reaction: 리렌더링');
        _appComponent = _appComponent ?? appFn;
        // appFn을 실행한 결과 노드를 루트 노드의 자식으로 랜더링
        rootNode.firstChild?.remove();
        rootNode.appendChild(_appComponent());
      }
    };
  },
  // 상태 값(데이터) 관리
  useState: (initValue) => {
    // || 논리합 연산자
    //    왼쪽 피연산자가 truthy일 때 왼쪽 값을,
    //    왼쪽 피연산자가 falsy(null, undefined, 0, '', false, NaN)일 때 오른쪽 값을 사용
    // _stateValue = _stateValue || initValue;

    // ?? null 병합 연산자
    //    왼쪽 피연산자가 null, undefined가 아닐 때 왼쪽 값을,
    //    왼쪽 피연산자가 null, undefined일 때 오른쪽 값을 사용
    _stateValue = _stateValue ?? initValue;
    // 초기에는 _stateValue가 undefined라서 initValue가 한 번 들어가고, 
    // 이후에는 _stateValue가 null/undefined로 되돌아가지 않는 이상 계속 유지된다.

    // 상태 값을 변경할 때 사용하는 함수
    function setValue(newValue) {
      const oldValue = _stateValue;
      _stateValue = newValue;

      // Object.is(a, b) : a와 b가 같은지 여부를 반환, 비교하는 두 값이 일치하면 true, 아니면 false
      // a, b가 원시형 타입일 때, 값이 다를 경우 false
      // a, b가 참조형 타입일 때, 내부의 속성이 바뀌어도 참조 주소가 바뀌지 않았다면 true가 됨
      if (!Object.is(oldValue, newValue)) { // oldValue와 newValue가 같은지 확인
        console.log('Reaction: 상태 변경으로 인해 리렌더링 수행');
        _root.render();
      }
    }

    return [ _stateValue, setValue ];
  },
};

export default reaction;
```

```javascript
import Reaction from './reaction.js';

// Header 컴포넌트
function Header() {
  console.log('Header 렌더링 됨');

  return (
    Reaction.createElement('header', null, 
      Reaction.createElement('h1', null, 'Counter - 07 상태(데이터) 변경시 자동으로 UI 리렌더링'), 
      Reaction.createElement('p', null, '파일 경로: ', 
        Reaction.createElement('span', null, `ch${document.URL.split('/ch')[1]}index.html`)))
  );
}

// Counter 컴포넌트
function Counter() {
  console.log('Counter 렌더링 됨');

  // 상태
  const [ count, setCount ] = Reaction.useState(5); // 구조 분해 할당

  // 카운터 감소
  const handleDown = () => {
    setCount(count - 1);
  };

  // 카운터 증가
  const handleUp = () => {
    setCount(count + 1);
  };

  // 카운터 초기화
  const handleReset = event => {
    console.log(event);
    setCount(0);
  };

  return (
    Reaction.createElement('div', { id: 'counter' }, 
      Reaction.createElement('button', { type: 'button', onclick: handleDown }, '-'), 
      Reaction.createElement('button', { type: 'button', onclick: handleReset }, 0), 
      Reaction.createElement('button', { type: 'button', onclick: handleUp }, '+'), 
      Reaction.createElement('span', null, count))
  );
}

// App 컴포넌트
function App() {
  console.log('App 렌더링 됨');
  return (
    Reaction.createElement('div', { id: 'app' }, Header, Counter)
  );
}

// root 요소에 App 추가
Reaction.createRoot(document.querySelector('#root')).render(App);
```

`useState`는 구조분해할당을 통해 count와 setCount에 값과 함수를 각각 할당받는다. 

click 이벤트 발생시, 해당 이벤트에 대한 setCount 함수가 동작하여 count 값이 변경되고 값이 같지 않으면, 데이터가 변경되어 컴포넌트를 리렌더링한다.