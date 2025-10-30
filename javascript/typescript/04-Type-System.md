# 타입 추론, 단언, 가드, 호환

- [타입 추론]()
- [타입 단언]()
- [타입 가드]()
- [타입 호환]()




<br />
<br />




## 타입 추론

명시적으로 타입을 지정하지 않아도 타입스크립트가 코드를 해석해서 적절한 타입을 자동으로 지정한다.

<br />

### 변수의 타입 추론

할당된 값과 일치하는 타입으로 추론한다.

```typescript
let name = '백'; // string 타입으로 추론
// name = 100; // 타입 에러

const age = 10; // number 타입으로 추론

let email; // any 타입으로 추론
email = 'abc@gmail.com';
email = 100;
// any 타입이 유지되어 어떤 값을 할당하더라도 타입은 변하지 않는다.
```

<br />

### 객체의 타입 추론

객체를 초기화할 때 객체 내부의 속성과 속성 값에 맞춰서 타입을 추론한다.

```typescript
const user = {
  name: '백',
  age: 31,
  email: 'abc@gmail.com',
  address: '서울시',
}

// 추론되는 타입
const user: {
  name: string;
  age: number;
  email: string;
  address: string;
}
```

<br />

### 함수의 타입 추론

#### 매개변수의 타입

- 매개변수의 타입을 지정하지 않으면 `any` 타입으로 추론한다.
- 매개변수에 기본값을 지정했을 경우, 기본값의 타입을 따라가도록 타입 추론한다.
  - 매개변수는 인자를 받지 않아도 기본값에 의해 실행이 된다.
  - 그래서 매개변수는 선택적으로 동작하게 되므로 `?`(옵셔널 파라미터)가 추가되어 추론된다.

#### 리턴 타입

- 리터값의 타입을 기반으로 추론한다.
- 매개변수의 타입과 연산자를 기반으로 리턴값의 타입을 추론한다.

```typescript
function add(num = 10) {
  return num + 20; 
}

// 추론되는 타입
function add(num?: number = 10): number

const result1 = add(100.123);
const result2 = add();
console.log(result1.toFixed(2)); // 120.12
console.log(result2); // 30
```

#### 리턴 타입 생략시

리턴 타입을 생략하면 리턴할 수 있는 모든 케이스를 다 계산해서 최대한 좁은 범위의 타입으로 추론한다.

```typescript
function checkNumber(x: number, y: number) {
  if(x === 10){
    return 10; 
    // 리턴 값 : 10 | undefined
  }else if(x === 20) {
    return 20; 
    // 리턴 값 : 10 | 20 | undefined
  }else if(x > y) {
    return 'x가 큼'; 
    // 리턴 값 : 10 | 20 | 'x가 큼' | undefined
  }else if(x < y) {
    return 'y가 큼'; 
    // 리턴 값 : 10 | 20 | 'x가 큼' | 'y가 큼' | undefined
  }else if(x === y) {
    return 'x, y는 ' + x; 
    // 리턴 값 : 10 | 20 | string | undefined
    // x의 값에 따라 바뀌는 넓은 범위의 string 타입을 갖게된다.
    // 그래서 'x가 큼' | 'y가 큼' 리터럴 타입도 포함된다.
  }else if(x === y) {
    return x + y;
    // 리턴 값 : number | string | undefined
    // x, y의 값에 따라 바뀌는 넓은 범위의 number 타입을 갖게된다.
    // 그래서 10 | 20 리터럴 타입도 포함된다.
  } else {
    return x;
    // 리턴 값 : number | string
    // 무조건 x의 값이라도 반환하므로 undefined를 반환할 일이 없게된다.
    // 그래서 undefined 타입은 사라진다.
  }
}
```




<br />
<br />




## 타입 단언

타입 추론에 기대지 않고 명시적으로 타입을 직접 지정할 수 있다. `as` 키워드로 타입을 지정하면, 타입스크립트 컴파일러가 타입 검사를 수행하지 않는다. 넓은 범위의 타입을 더 구체적인 타입으로 지정할 때 사용한다.

```typescript
function getMsg(msg: string | number) { // 리턴값은 string | number 타입으로 추론
  return msg;
}

const msg1: number = getMsg(100.123) as number; // 리턴값이 number인지 정확하면 타입 단언
console.log(msg1.toFixed(2)); // 100.12

const msg2 = getMsg('hello') as string; // 리턴값이 string인지 정확하면 타입 단언
console.log(msg2.toUpperCase()); // hello
```

<br />

### Non-null Assertion Operator ( `!` )

`!` 키워드를 사용하여 값이 `null`이나 `undefined`가 아님을 단언한다. 옵셔널 속성(`?`)이나 유니언 타입에서 `null` 또는 `undefined`가 포함된 경우, 값 뒤에 `!`를 붙여서 값이 확실히 존재함을 단언한다.

```typescript
// querySelector는 Element | null 타입을 갖는다.
const a = document.querySelector('a[href="ch06/ex06-24.js"]') as Element;
a.textContent += ' 클릭';

// Non-null Assertion Operator (!)
const a = document.querySelector('a[href="ch06/ex06-24.js"]');
a!.textContent += ' 클릭';
// null이나 undefined가 아님을 단언하므로, querySelector가 갖는 타입에서 null 타입은 제거된다.

// 런타임 에러 발생
const a = document.querySelector('a[href="aaabbbcccdddeeefff"]');
a!.textContent += ' 클릭';
// a가 null 타입이 되므로 런타임시 에러가 발생한다.
// 타입스크립트에서는 에러를 발견할 수 없지만, 컴파일 후 자바스크립트 런타임시 에러가 발생할 확률이 있어 왠만하면 사용하지 않는것이 좋다.

// 타입 가드 : 정확한 타입 추론으로 안전한 코드 작성 가능
const a = document.querySelector('a[href="ch06/ex06-24.js"]');
if (a !== null) {
  a!.textContent += ' 클릭';
}
```

<br />

### 타입 단언 주의 사항

- 실제 값이 단언한 타입 구조와 다르면 런타임 에러가 발생한다.
- 타입 단언은 확신이 있을 때만 사용해야 한다.
- 타입 단언보다는 타입 가드를 우선적으로 고려하는게 안전하다.
- 타입 단언은 컴파일 시 타입 검사만 통과시킬 뿐, 실제 값을 보정하지 않는다. TypeScript에서는 오류가 없어도 컴파일 후 런타임에서 에러가 발생할 수 있다. 따라서 가능하면 사용을 최소화하는 것이 좋다.




<br />
<br />




## 타입 가드




<br />
<br />




## 타입 호환