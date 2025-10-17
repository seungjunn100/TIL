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
- [함수 호출 방식에 결정되는 `this`](#함수-호출-방식에-결정되는-this)
  - [일반 함수 호출](#일반-함수-호출)
  - [메서드 호출](#메서드-호출)
  - [메서드(화살표 함수) 호출](#메서드화살표-함수-호출)
  - [`apply()`, `call()` 호출](#apply-call-호출)
  - [함수 내부의 `this`](#함수-내부의-this)
- [일급 객체 ( First-Class Object )](#일급-객체--first-class-object)
  - [재귀 함수](#재귀-함수)
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
function printNum(num1, num2) {
  console.log(num1, num2);
}
printNum(); // num1 = undefined, num2 = undefined
printNum(1, 2); // num1 = 1, num2 = 2


// 매개변수의 수가 많은 경우
function printNum(num1, num2, num3) {
  console.log(num1, num2, num3);
}
printNum(1, 2); // num1 = 1, num2 = 2, num3 = undefined


// 인자의 수가 많은 경우
function printNum(num1, num2) {
  console.log(num1, num2);
}
printNum(1, 2, 3); // a = 1, b = 2, 세번 째 인자의 수 3은 처리할 매개변수가 없기 때문에 무시된다.
```

#### Arguments

함수 호출 시 전달되는 모든 인자를 담고 있는 유사 배열 객체이다. 함수 내에서 접근이 가능하고 배열과 비슷하게 `length` 속성과 `index`로 각 인자에 접근이 가능하다.

```JavaScript
function printNum(num1, num2) {
  console.log(num1, num2, arguments);
}

printNum(); // undefined undefined [Arguments] {  }
printNum(10); // 10 undefined [Arguments] { '0': 10 }
printNum(10, 20); // 10 20 [Arguments] { '0': 10, '1': 20 }
printNum(10, 20, 30, 40); // 10 20 [Arguments] { '0': 10, '1': 20, '2': 30, '3': 40 }
// 필요한 값만 매개변수로 들어가고 나머지 인자는 무시된다.
```

#### 매개변수 기본값

매개변수에 기본 값을 설정할 수 있다. `undefined`인 경우에만 기본 값이 할당되며, 인자에 기본 값을 설정한다면 설정한 값으로 할당된다.

```JavaScript
function printNum(num1 = 0, num2 = 0) {
  console.log(num1, num2);
}

printNum(); // 0 0
printNum(10); // 10 0
printNum(10, 20); // 10 20
```

#### Rest Parameters

전달될 인자의 개수가 정해지지 않아 모를 때, 모든 인자를 배열로 전달 받고 싶을 때 사용한다.

```JavaScript
function printNum(...nums) {
  console.log(nums);
}
printNum(); // []
printNum(10); // [ 10 ]
printNum(10, 20); // [ 10, 20 ]
printNum(10, 20, 30, 40); // [ 10, 20, 30, 40 ]


// 부분적으로 매개변수를 설정할 수 있다.
function printNum(num1, num2, ...nums) {
  console.log(num1, num2, nums);
}
printNum(); // undefined undefined []
printNum(10); // 10 undefined []
printNum(10, 20); // 10 20 []
printNum(10, 20, 30, 40); // 10 20 [ 30, 40 ]
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
const star = '⭐️';
console.log(star);

// 정의만 해놓고 호출하지 않으면 함수는 실행되지 않는다.
function run() {
  const star = '⭐️';
  console.log(star);
}

// IIFE 표현식을 통해 바로 호출해서 실행할 수 있다.
(function run() {
  const star = '⭐️';
  console.log(star);
})(); // ⭐️
```

`star`의 변수를 함수 안에 두고 지역변수로만 사용하도록 사용하기 위해 사용할 수 있다. 전역 스코프를 오염시키지 않을 수 있다. 일회성 실행이 필요한 코드에 적합




<br />
<br />




## 함수 호출 방식에 결정되는 `this`

`this`는 함수, 객체, 클래스 내부에서 키워드로 접근 가능하며, 문맥에 따라 `this`가 가르키는 것이 결정된다. 이것을 `this 바인딩`이라고 한다.

<br />

### 일반 함수 호출

```javascript
// 함수 선언문
function print() {
  console.log(this); // 브라우저에서 this는 window 객체
  window.console.log('window.'); // window. // console은 window 객체의 속성이다.
  this.console.log('this.'); // this. // 브라우저에서 this는 window 객체
  console.log('window 생략'); // window 생략 // window 객체는 어디서나 참조 가능하므로 생략 가능
}
print();

// 한수 표현식
const print2 = function () {
  console.log(this); // 브라우저에서 this는 window 객체
};
print2();
```

<br />

### 메서드 호출

`this`는 메서드를 정의한 객체이다. 생성된 객체를 참조하므로 객체에 종속적인 속성을 부여하는게 가능하다.

```javascript
const getDogName = function () {
  return this.dogName;
};

const firstDog = {
  dogName: '콩이',
  age: 12,
  getName: getDogName
};

const secondDog = {
  dogName: '단이',
  age: 8,
  getName: getDogName
};

// 일반 함수 호출
console.log(getDogName()); // undefined // this = window 객체
// 일반 함수 호출에서 this는 window 객체를 가르키지만, window 객체에는 dogName의 속성이 없다.

// 메서드 호출
console.log(firstDog.age, firstDog.getName()); // 12 콩이 // this = firstDog
console.log(secondDog.age, secondDog.getName()); // 8 단이 // this = secondDog
```

변수, 배열의 요소, 객체의 프로퍼티에 함수 할당 후 실행해 보면 `this`의 결과가 다르다는 것을 알 수 있다.

```javascript
// 변수에 선언한 함수 표현식
const print = function () {
  console.log(this);
};
print(); // this = window 객체

// 배열의 요소에 함수 할당
const arr = [print];
arr[0](); // this = arr

// 객체의 속성에 함수 할당
const obj = {
  printThis: print
};
obj.printThis(); // this = obj
```

<br />

### 메서드(화살표 함수) 호출

화살표 함수는 함수 내부에 `arguments`와 `this`가 생성되지 않고, 상위 컨텍스트의 `arguments`와 `this`를 사용하게 된다.

```javascript
// 상위 컨텍스트의 this
console.log(this); // window 객체

const getDogName = () => {
  return this.dogName;
};

const firstDog = {
  dogName: '콩이',
  age: 12,
  getName: getDogName
};

const secondDog = {
  dogName: '단이',
  age: 8,
  getName: getDogName
};

// 일반 함수 호출
console.log(getDogName()); // undefined // this = window 객체

// 메서드 호출
console.log(firstDog.age, firstDog.getName()); // 12 undefined // this = window 객체
console.log(secondDog.age, secondDog.getName()); // 8 undefined // this = window 객체
```

<br />

### `apply()`, `call()` 호출

함수에 정의된 메서드이며, `this`를 명시적으로 지정할 수 있다. `함수명.apply()`, `함수명.call()` 형태로 호출할 수 있다.

#### `apply(param1, param2)`

- 두 개의 매개변수를 가진다.
- 첫 번째 매개변수(param1)에는 `this`로 사용할 객체를 전달한다.
- 두 번째 매개변수(param2)에는 함수에 전달할 배열을 전달한다.

`call(param1, param2, param3, ...)`

- 여러 개의 매개변수를 가진다.
- 첫 번째 매개변수(param1)에는 `this`로 사용할 객체를 전달한다.
- 두 번째 이후의 매개변수(param2, param3, ...)에는 함수에 전달할 인자값을 차례대로 전달한다.

```javascript
const add = function (a, b) {
  console.log(this.name);
  return a + b;
};

const hong = {
  name: '홍',
  getSum: add
};

const kong = {
  name: '콩',
  getSum: add
};

console.log(hong.name, hong.getSum.call(kong, 10, 20, 30)); // 홍, 콩 30
// call 메서드를 사용하여 첫번 째 인자의 this를 kong의 객체로 전달하여 hong.getSum 함수가 실행될 때 this.name은 kong.name의 값이 전달된다.
// 나머지 인자도 전달되어 함수가 실행될 때 a, b 두개의 매개변수만 존재 하므로 10과 20만 전달 받아 연산되고 나머지 인자는 무시된다.

console.log(kong.name, kong.getSum.apply(hong, [30, 40, 50])); // 콩, 홍 70
// apply 메서드를 사용하여 첫번 째 인자의 this를 hong의 객체로 전달하여 kong.getSum 함수가 실행될 때 this.name은 hong.name의 값이 전달된다.
// 두번 째 인자도 전달되어 함수가 실행될 때 a, b 두개의 매개변수만 존재 하므로 30과 40만 전달 받아 연산되고 배열의 나머지 요소는 무시된다.
```

<br />

### 함수 내부의 `this`

함수 내부의 `this`가 상위 스코프의 `this`를 참조하지 못하고 함수 자신의 `this`를 참조하는 경우로써, `visit2`는 호출 주체가 없는 일반 함수로 호출하여 `this`는 `window 객체`를 가르키게 된다.

```javascript
var count = 0; // window.count = 2;

const myObj = {
  count: 0,
  visit: function(){
    // 방문자를 한명 증가시킨다.
    this.count++; // this = myObj

    const visit2 = function () {
      // 방문자를 한명 증가시킨다.
      this.count++; // this = window
    };

    visit2();
  },
};

myObj.visit(); // this = myObj
myObj.visit(); // this = myObj
console.log('방문자수', count); // 방문자수 2
console.log('방문자수', myObj.count); // 방문자수 2
```

상위 스코프의 `this`를 참조할 수 있는 다양한 방법들이 있다.

```javascript
// 임시 변수로 상위 스코프의 this를 참조
var count = 0; // window.count = 0;
const myObj = {
  count: 0,
  visit: function(){
    this.count++; // this = myObj

    const that = this; // that = myObj

    const visit2 = function () {
      that.count++; // that = myObj
    };

    visit2();
  },
};
myObj.visit(); // this = myObj
myObj.visit(); // this = myObj
console.log('방문자수', count); // 방문자수 0
console.log('방문자수', myObj.count); // 방문자수 4


// call을 사용해서 상위 스코프의 this를 내부에 전달
var count = 0; // window.count = 0;
const myObj = {
  count: 0,
  visit: function(){
    this.count++; // this = myObj

    const visit2 = function () {
      this.count++; // this = myObj
    };

    visit2.call(this);
  },
};
myObj.visit(); // this = myObj
myObj.visit(); // this = myObj
console.log('방문자수', count); // 방문자수 0
console.log('방문자수', myObj.count); // 방문자수 4


// this가 생성되지 않는 화살표 함수 사용
var count = 0; // window.count = 0;
const myObj = {
  count: 0,
  visit: function(){
    this.count++; // this = myObj

    const visit2 = () => {
      this.count++; // this = myObj
    };

    visit2();
  },
};
myObj.visit(); // this = myObj
myObj.visit(); // this = myObj
console.log('방문자수', count); // 방문자수 0
console.log('방문자수', myObj.count); // 방문자수 4
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
function sendData(data, cb) {
  // data를 서버에 전송한다.
  // ......
  cb();
}

const newPing = { 
  name: '새로핑', 
  age: 7 
};
sendData(newPing, () => {
  console.log('회원 가입 완료'); // sendData 함수의 작업 완료 후에 호출
});

const newPost = {
  title: '콜백 함수란', 
  writer: '진지핑'
};
sendData(newPost, () => {
  console.log('게시글 작성 완료'); // sendData 함수의 작업 완료 후에 호출
});

/*
  데이터를 서버에 전송하면 그 내용에 따라 받는 콜백 함수가 다르다.
  newPing이라는 데이터를 서버에 보내면 콜백 함수로 회원 가입 완료라는 함수를 호출할 수 있다.
*/
```

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










배열, 함수를 넣어서 확인
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)
console.dir(); // 속성, 메서드(프로토타입)