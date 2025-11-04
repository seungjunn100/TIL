# 에러 핸들링(Error Handling)

- [Error Class](#error-class)
  - [사용자 정의 에러](#사용자-정의-에러)
- [에러 종류](#에러-종류)
- [에러 처리](#에러-처리)
  - [`try...catch` 문](#trycatch-문)
  - [`throw` 문](#throw-문)
- [에러 버블링(전파)](#에러-버블링전파)




<br />
<br />




## Error Class

`Error`는 자바스크립트의 기본 에러 객체 클라스이다. 모든 에러는 이 클래스를 상속받아 만들어진다.

`new Error(message?: string, options?: ErrorOptions) => Error`

- `message` : 에러 메세지
- `options` : 다른 에러를 원인(`cause`)으로 연결할 때 사용

#### 주요 속성

- `name` : 에러 이름 (`Error`, `TypeError`, `ReferenceError`, `SyntaxError` 등)
- `message` : 에러 설명
- `stack` : 에러가 발생한 지점의 콜 스택 정보

```typescript
function f1() {
  const err = new Error('에러 발생');
  console.log(err.name);
  console.log(err.message);
  console.log(err.stack);    
}

function f2() {
  f1();
}

f2();
/*
Error                - err.name
에러 발생             - err.message
Error: 에러 발생      - err.stack
    at f1 (file:///C:/Users/USER/febc15/js/workspace/ch08/ex08-01.js:4:21)
    at f2 (file:///C:/Users/USER/febc15/js/workspace/ch08/ex08-01.js:10:9)
    at file:///C:/Users/USER/febc15/js/workspace/ch08/ex08-01.js:12:5
    at file:///C:/Users/USER/febc15/js/workspace/ch08/ex08-01.js:13:3
*/
```

<br />

### 사용자 정의 에러

```typescript
class CustomError extends Error {
  constructor(message: string) {
    super(message);
    this.name = '사용자 정의 에러';
  }
}
function f1() {
  const err = new CustomError('에러 발생');
  console.log(err.name);
  console.log(err.message);
  console.log(err.stack);    
}

function f2() {
  f1();
}

f2();
/*
사용자 정의 에러                - err.name
에러 발생                      - err.message
사용자 정의 에러: 에러 발생      - err.stack
    at f1 (file:///C:/Users/USER/febc15/js/workspace/ch08/ex08-01.js:4:21)
    at f2 (file:///C:/Users/USER/febc15/js/workspace/ch08/ex08-01.js:10:9)
    at file:///C:/Users/USER/febc15/js/workspace/ch08/ex08-01.js:12:5
    at file:///C:/Users/USER/febc15/js/workspace/ch08/ex08-01.js:13:3
*/
```




<br />
<br />




## 에러 객체

`Error` 클래스를 상속 받아 세분화된 에러

- `SyntaxError` : 문법 오류

  ```typescript
  new Function('x', 'y', 'retttturn x + y');
  // Uncaught SyntaxError: Unexpected identifier 'x'
  ```

- `ReferenceError` : 선언되지 않은 변수 참조 시 발생

  ```typescript
  console.log(x);
  //Uncaught ReferenceError: x is not defined
  ```

- `TypeError` : 잘못된 타입의 값을 사용하거나 메서드 호출 시 발생
  
  ```typescript
  null.fn()
  // Uncaught TypeError: Cannot read properties of null (reading 'fn')
  
  undefined.fn()
  // Uncaught TypeError: Cannot read properties of undefined (reading 'fn')
  ```

- `RangeError` : 값이 허용된 범위를 벗어날 때 발생

- `URIError` : `encodeURI()` / `decodeURI()` 사용 시 잘못된 인자 전달




<br />
<br />




## 에러 처리

### `try...catch` 문

에러가 발생하면 프로그램 실행이 중단된다. 이를 해결하기 위해 에러가 발생해도 프로그램을 안전하게 실행하기 위해서 `try...catch` 구문을 사용한다.

`try` 블럭 안에서 에러가 발생하면 `catch` 블럭이 실행되고, 에러가 없으면 `catch`는 건너 뛰고 `finally`로 넘어간다. `finally`는 항상 실행되며, 선택적으로 사용한다.

```typescript
function f1() {
  console.log('1. f1 호출');

  try {
    const fn = new Function('rettturn 10'); // SyntaxError: Unexpected number
    console.log('2. fn 실행', fn()); // 문법 오류로 실행 X
  } catch(err) {
    // 에러가 다른 타입이 올 수도 있는 상황에 대한 타입 가드
    // 일반적으로 Error 객체가 온다.
    if (err instanceof Error) {
      console.error('3.', err.message);
    }
  } finally { // optional
    console.log('4. try...catch 문이 실행 완료된 후 실행');
  }
  
  console.log('5. f1 함수 정상 종료');
}

f1()
/*
1. f1 호출
3. Unexpected number
4. try...catch 문이 실행 완료된 후 실행
5. f1 함수 정상 종료
*/
```

<br />

### `throw` 문

개발자가 의도적으로 에러를 발생시킬 수 있다. 에러를 직접 처리하지 않고 함수를 호출한 쪽으로 전달할 때 사용한다.

`throw` 뒤에는 문자열, 숫자도 가능하지만 일반적으로 `Error` 객체를 던지는 것이 권장된다.

```typescript
function divide(x: number, y: number) {
  if (y === 0) { // y가 0이면 에러를 던지는 함수
    throw new Error('0으로 나눌 수 없습니다.');
  }
  return x / y;
}

function f1() {
  try {
    // Math.round(Math.random()) = 1 아님 0
    const result1 = divide(10, Math.round(Math.random()));
    console.log(result1);
  } catch(err) {
    if (err instanceof Error) {
      console.error(err.message);
    }
  }
  
  const result2 = divide(10, 2);
  console.log(result2);
}

f1()
/*
0으로 나눌 수 없습니다.
5
*/
```




<br />
<br />




## 에러 버블링(전파)

하위 함수에서 에러가 발생하면 상위 함수로 전파되어 올라간다. 즉, 내부 함수에서 `try...catch`문으로 처리하지 않으면 가장 가까운 `catch` 블럭에서 처리된다.

```typescript
function f1() {
  const fn = new Function('retturn 10'); // 최초 에러 - SyntaxError
  fn();

  console.log('1. f1 함수 정상 종료'); // 에러로 인해 실행 X
}

function f2() {
  f1(); // f1()에서 전파된 에러 - SyntaxError
  console.log('2. f2 함수 정상 종료'); // 에러로 인해 실행 X
}

try {
  f2(); // f2() 실행 결과 SyntaxError 에러
} catch(err) {
  console.error(err); // SyntaxError 에러 출력
}
console.log('3. 프로그램 함수 정상 종료');
/*
SyntaxError: Unexpected number
    at new Function (<anonymous>)
    at f1 (<anonymous>:5:20)
    at f2 (<anonymous>:11:13)
    at <anonymous>:18:5
    at <anonymous>:20:3
3. 프로그램 함수 정상 종료
*/
```