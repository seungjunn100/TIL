# 함수 ( Function )

- [함수의 기본](#함수의-기본)
  - [함수 정의 및 호출](#함수-정의-및-호출)
  - [기본적인 함수 사용](#기본적인-함수-사용)
  - [반복적인 작업을 하나의 함수로 표현](#반복적인-작업을-하나의-함수로-표현)
  - [함수의 매개변수, 인자](#함수의-매개변수-인자)
  - [반환 ( return )](#반환--return)
- [함수 정의](#함수-정의)
  - [함수 선언문](#함수-선언문)
  - [함수 표현식](#함수-표현식)
  - [화살표 함수](#화살표-함수)
  - [Function 생성자 함수](#function-생성자-함수)
  - [IIFE(Immediately-Invoked Function Expressions)](#iifeimmediately-invoked-function-expressions)
- [일급 객체 ( First-Class Object )](#일급-객체--first-class-object)
  - [콜백 함수](#콜백-함수)
  - [고차 함수](#고차-함수)




<br />
<br />




## 함수의 기본

함수는 특정한 일을 수행하는 코드의 `집합`이다. 반복되는 작업들은 하나의 함수로 만들어 **재사용성을 높일 수 있다.** 코드 구조를 명확하게 만들어 **가독성을 높일 수 있다.**

<br />

### 함수 정의 및 호출

```JavaScript
// 함수 정의
function add(a, b) {
  return a + b;
}

// 함수 호출
add(1, 2); // 3을 반환 받는다.
```

- `function` : 함수 정의 키워드
- `add` : 함수명
- `a, b` : Parameter(매개변수)를 통해 외부로 부터 데이터를 전달 받을 수 있다.
- `a + b` : 특정한 일을 수행한다.
- `return` : 특정한 일을 수행하여 나온 결과 값을 외부로 다시 반환한다.

<br />

### 기본적인 함수 사용

```javascript
function add(a, b) {
  const result = a + b;
  return result;
}

// 함수 내에서 result를 출력하거나 사용해야 한다면 변수로 할당해줘도 되지만,
// 결과 값만 바로 반환하는 경우에는 변수를 할당하지 않고 바로 반환해줘도 된다.
function add(a, b) {
  return a + b;
}

// 함수를 호출하면 결과 값 3을 반환 받는다.
// 하지만 반환된 값은 어디에도 저장되지 않는다.
add(1, 2);

// 변수를 선언하여 반환된 결과 값을 저장할 수 있다.
const result = add(1, 2);
console.log(result); // 3
```

<br>

### 반복적인 작업을 하나의 함수로 표현

```JavaScript
// 반복적인 작업
let firstName = '김';
let lastName = '첨지';
let fullName = `${firstName} ${lastName}`;
console.log(fullName); // 김 첨지

let firstName2 = '홍';
let lastName2 = '길동';
let fullName2 = `${firstName2} ${lastName2}`;
console.log(fullName2); // 홍 길동


// 하나의 함수
function fullName(firstName, lastName) {
  return `${firstName} ${lastName}`;
}
console.log(fullName('김', '첨지')); // 김 첨지
console.log(fullName('이', '몽룡')); // 홍 길동
```

<br />

### 함수의 매개변수, 인자

매개변수의 기본 값은 무조건 `undefined`이다.

```JavaScript
function add(a, b) {
  console.log(a);
  console.log(b);
  return a + b;
}
add(); // a = undefined, b = undefined
add(1, 2); // a = 1, b = 2
```

매개변수의 정보는 함수 내부에서 접근이 가능한 `arguments` 객체에 저장된다.

```JavaScript
function add(a, b) {
  console.log(a);
  console.log(b);
  console.log(arguments);
  console.log(arguments[1]);
  return a + b;
}
add(1, 2, 3);
// 1
// 2
// [Arguments] { '0': 1, '1': 2, '2': 3 }
// 2
// 필요한 값만 매개변수로 들어가고 나머지 인자는 무시된다. 3은 들어갈 매개변수가 없으므로 무시된다.
```

#### 매개변수 기본값

매개변수에 기본 값을 설정할 수 있다.

```JavaScript
function add(a = 1, b = 1) {
  console.log(a);
  console.log(b);
  return a + b;
}
add(); // 1, 1, undefined인 경우에만 기본 값이 할당된다.
add(2, 2); // 2, 2, 인자에 값을 설정한다면 설정한 값으로 할당된다.
```

#### Rest Parameters

얼마나 많은 개수의 인자가 전달될지 모를 때, 모든 것들을 배열로 받고 싶을 때 사용한다.

```JavaScript
function sum(...numbers) {
  console.log(numbers);
}
sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10); // [ 1, 2, 3, 4,  5, 6, 7, 8, 9, 10 ]

// 부분적으로 매개변수를 설정할 수 있다.
function sum(a, b, ...numbers) {
  console.log(a);
  console.log(b);
  console.log(numbers);
}
sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10); // 1, 2, [ 3, 4, 5, 6, 7, 8, 9, 10 ]
```

<br />

### 반환 ( return )

함수를 호출 했을 때, 함수 안에서 특정한 일을 수행하고 나온 **결과 값을 반환**하기 위해서 `return`을 사용한다.

```JavaScript
function add(a, b) {
  return a + b;
}

const result = add(1, 2);
console.log(result); // 3
```

함수에서 아무것도 반환하지 않으면 `undefined`가 반환된다.

```JavaScript
function add(a, b) {
  const sum = a + b;
  // return undefined;
}
// 함수에서 return을 명시적으로 작성하지 않으면
// 코드 상에서 자바스크립트 엔진이 return undefined;를 자동으로 처리해준다.
// 현재 함수 내에 return undefined;가 선언되어 있는 상태랑 같다.

const result = add(1, 2);
console.log(result); // undefined
```

함수에서 무거운 작업들을 실행하기 이전에 함수 도입 부분에서 조건을 걸어 함수를 계속 수행하기에 적합한 조건인지 먼저 검사를 해준 다음에 원하는 조건이 아닐 경우 `return;`을 통해 함수를 `즉시 종료`할 수 있다. `return;`은 `return undefined;`의 약자이다.

```JavaScript
// 원하는 조건 : num이 0보다 큰 수
function print(num) {
  if (num < 0) {
    return;
  }
  console.log(num);
}

// 원하는 조건을 성립하므로 if문을 통과해 다음 작업을 수행한다.
print(12); // 12

// 원하는 조건이 아니므로 return에 의해 함수가 종료된다.
print(-12); // undefined
```




<br />
<br />




## 함수 정의

### 함수 선언문

```JavaScript
function add(a, b) {
  return a + b;
}
```

<br />

### 함수 표현식

표현식은 **값으로 평가**될 수 있는 `문`을 뜻한다.

```JavaScript
const add = function (a, b) {
  return a + b;
};
console.log(add(1, 2)); // 3
```

<br />

### 화살표 함수

```JavaScript
const add = (a, b) => {
  return a + b;
}
console.log(add(1, 2)); // 3
```

코드 안에서 어떤 값만 바로 리턴하는 경우라면 `중괄호({})`와 `return`을 **생략**할 수 있다.

```javascript
const add = (a, b) => a + b;
console.log(add(1, 2)); // 3
```

매개 변수로 하나의 인자 값만 받는 경우라면 매개 변수의 `괄호(())`도 **생략**할 수 있다.

```javascript
const add = a => a + 2;
console.log(add(1)); // 3
```

<br />

### Function 생성자 함수

```JavaScript
const add = new Function('x', 'y', 'let result = x + y; return result;');
```

<br />

### IIFE(Immediately-Invoked Function Expressions)

즉각적으로 호출이 되는 함수 표현식이다.

```JavaScript
// 정의만 해놓고 호출하지 않으면 함수는 실행되지 않는다.
function run() {
  console.log('⭐️');
}

// IIFE 표현식을 통해 바로 호출해서 실행할 수 있다.
(function run() {
  console.log('⭐️');
})(); // ⭐️
```




<br />
<br />




## 일급 객체 ( First-Class Object )

일급 객체는 **값처럼 다룰 수 있는 객체를 의미**한다. 즉, 숫자나 문자열처럼 `변수나 자료구조(객체, 배열 등)에 저장`할 수 있고, `함수의 매개변수에 전달`할 수 있고, `함수의 반환값으로 사용`할 수 있다.

자바스크립트에서는 `함수`도 `일급 객체`로 취급된다. `일급 함수(First-Class Function)`라고도 불리며, 일급 객체처럼 함수도 `변수나 자료구조(객체, 배열 등)에 저장`할 수 있고, `함수의 매개변수에 전달`할 수 있고, `함수의 반환값으로 사용`할 수 있다.

```javascript
// 함수를 변수에 할당
const add = function (a, b) {
  return a + b
};


// 함수를 객체의 속성으로 할당 (메서드)
const obj = {};
obj.func = add;
console.log(obj); // { func: [Function: add] }


// 함수를 배열의 요소로 할당
const arr = [];
arr.push(add);
console.log(arr); // [ [Function: add] ]


// 함수를 함수의 매개변수에 전달
function func1(funcNum) {
  console.log('첫번째 함수 호출');
  funcNum();
}
function func2() {
  console.log('두번째 함수 호출');
}
func1(func2); // 첫번째 함수 호출 두번째 함수 호출


// 함수를 함수의 반환값으로 사용
function func1() {
  console.log('첫번째 함수 호출');
  return function func2() {
    console.log('두번째 함수 호출');
  };
}
func1(); // '첫번째 함수 호출' [Function: func2]
const func2 = func1();
func2(); // '첫번째 함수 호출' '두번째 함수 호출'
```

<br />

### 재귀 함수

**자기 자신을 호출**하는 함수를 의미한다.

```javascript
// 팩토리얼 : 1부터 자신까지의 모든 양수의 곱
// n! = 1 * 2 * ... * (n-1) * n
function factorial(n) {
  if(n === 1) return 1;
  return n * factorial(n - 1);
}

console.log(factorial(5)); // 120
/*
  5!
  = 5 * 4!
  = 5 * 4 * 3!
  = 5 * 4 * 3 * 2!
  = 5 * 4 * 3 * 2 * 1!
  = 5 * 4 * 3 * 2 * 1 = 120
*/
```

<br />

### 콜백 함수

**나중에 호출해주는 함수**를 뜻하며, 다른 함수에게 매개변수로 전달되어 나중에 실행되는 함수를 의미한다.

```javascript
// setTimeout() 함수는 지정한 시간(밀리초)이 지난 뒤에 전달된 콜백 함수를 실행하는 고차 함수이다.
setTimeout(function () {
  console.log('3초 후에 실행!');
}, 3000);
```

`setTimeout();` 함수의 매개변수로 `function () { ... }` 콜백 함수와 `3000(=3초)` 인자가 전달되어 3초 후에 콜백함수가 실행되어 `3초 후에 실행!`이라는 문장이 출력된다.

<br />

### 고차 함수

**인자로 함수를 받거나, 함수를 반환하는 함수를 의미**한다.

```JavaScript
const add = (a, b) => a + b;
const multiply = (a, b) => a * b;

function calculator(a, b, action) { // action은 외부로 부터 주어지는 콜백 함수를 전달받는 매개변수이다.
  const result = action(a, b); // 전달 받은 참조값을 통해 연산을 진행 후 결과 값을 변수에 저장한다.
  console.log(result);
  return result;
}

// add, multiply - 함수를 호출하는 것이 아니라 함수의 참조값을 전달해 준다.
calculator(1, 2, add); // 3
calculator(1, 2, multiply); // 2
```

콜백함수가 호출될 수 없는 조건을 만들어 사용할 수도 있다.

```JavaScript
const add = (a, b) => a + b;
const multiply = (a, b) => a * b;

function calculator(a, b, action) {
  if (a < 0 || b < 0) {
    return;
  }
  const result = action(a, b);
  console.log(result);
  return result;
}

let outcome = calculator(-1, -2, add);
console.log(outcome); // undefined
```

함수를 호출했지만 if문에 의해 함수가 종료되어 undefined 값이 반환된다. 그 아래에 있는 코드들은 실행되지 않아 결과 값을 출력하거나 반환할 수 없다.
<!-- 




<br />
<br />




## 불변성(Immutability) -->