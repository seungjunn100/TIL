# 타입 추론, 단언, 가드, 호환, 연산자

- [타입 추론](#타입-추론)
  - [변수의 타입 추론](#변수의-타입-추론)
  - [객체의 타입 추론](#객체의-타입-추론)
  - [함수의 타입 추론](#함수의-타입-추론)
- [타입 단언](#타입-단언)
  - [Non-null Assertion Operator ( `!` )](#non-null-assertion-operator)
  - [타입 단언 주의 사항](#타입-단언)
- [타입 가드](#타입-가드)
  - [typeof 연산자 사용](#typeof-연산자-사용)
  - [instanceof 연산자 사용](#instanceof-연산자-사용)
  - [구별된 유니언 타입 사용](#구별된-유니언-타입-사용)
  - [사용자 정의 타입 가드 사용](#사용자-정의-타입-가드-사용)
- [타입 호환](#타입-호환)
- [타입 연산자](#타입-연산자)
  - [keyof 연산자](#keyof-연산자)
  - [typeof 연산자](#typeof-연산자)
  - [인덱스 접근 타입 ( Indexed Access Types )](#인덱스-접근-타입--indexed-access-types)




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

변수로 여러 타입이 지정되었을 경우, 타입의 범위를 좁혀 정확한 타입 추론을 할 수 있도록 도와주는 기능이다.

<br />

### typeof 연산자 사용

```typescript
// number, string
function print(msg: number | string) {
  if (typeof msg === 'string') {
    // msg가 string 타입으로 추론
    console.log(msg.toUpperCase());
  } else {
    // msg가 number 타입으로 추론
    console.log(msg.toFixed(2));
  }
}

// number, string, null
function getLength(value: string | number[] | null) {
  if (value === null) {
    return 0;
  }
  if (typeof value === 'string') {
    return value.length;
  }
  return value.length; // number[] 추론
}
```

<br />

### instanceof 연산자 사용

```typescript
function print(msg: number | string[] | Date){
  if (typeof msg === 'number') {
    console.log(msg.toFixed(2));
  }

  if (msg instanceof Array ) {
    console.log(msg.length);
  }

  if (msg instanceof Date) {
    console.log(msg.getFullYear());
  }
}
```

<br />

### 구별된 유니언 타입 사용

```typescript
interface User {
  name: string;
  grade: '🫘' | '🌱' | '🌸';
  admin: false; // 속성 정의 시 구체적인 값을 지정한 후 객체의 속성값으로 확인
}

interface AdminUser {
  name: string;
  level: 1 | 2 | 3;
  admin: true;
}

const user1: User = {
  name: 'user',
  grade: '🫘',
  admin: false
};

const user2: AdminUser = {
  name: 'admin',
  level: 1,
  admin: true
};

function greetUserByRole(user: User | AdminUser) {
  if (user.admin === true) { // 속성 정의 시 구체적인 값을 지정한 후 객체의 속성값으로 확인
    console.log(`안녕하세요. Lv ${user.level} "${user.name}" 관리자님!`);
  } else {
    console.log(`안녕하세요. ${user.grade} "${user.name}" 유저님!`);
  }
}

greetUserByRole(user1); // 안녕하세요. 🫘 "user" 유저님!
greetUserByRole(user2); // 안녕하세요. Lv 1 "admin" 관리자님!
```

<br />

### 사용자 정의 타입 가드 사용

```typescript
interface User {
  name: string;
  grade: '🫘' | '🌱' | '🌸';
  admin: false;
}

interface AdminUser {
  name: string;
  level: 1 | 2 | 3;
  admin: true;
}

interface Guest {
  name: string;
}

const user1: User = {
  name: 'user',
  grade: '🫘',
  admin: false
};

const user2: AdminUser = {
  name: 'admin',
  level: 1,
  admin: true
};

const user3: Guest = {
  name: 'guest'
}

function greetUserByRole(user: User | AdminUser | Guest) {
  if(isAdmin(user)){ // AdminUser일 경우
    console.log(`안녕하세요. Lv ${user.level} "${user.name}" 관리자님!`);
  }else if(isUser(user)){ // User일 경우
    console.log(`안녕하세요. ${user.grade} "${user.name}" 유저님!`);
  }else{ // Guest일 경우
    console.log(`안녕하세요. "${user.name}" 게스트님!`);
  }
}

// user is AdminUser : 반환값이 true일 경우 user는 AdminUser 타입으로 인식한다.
// 'admin' in user : 객체에 지정한 속성이 포함되어 있는지 여부를 반환한다.
function isAdmin(user: User | AdminUser | Guest): user is AdminUser {
  return 'admin' in user && user.admin === true;
}
function isUser(user: User | AdminUser | Guest): user is User {
  return 'admin' in user && user.admin === false;
}

greetUserByRole(user1); // 안녕하세요. 🫘 "user" 유저님!
greetUserByRole(user2); // 안녕하세요. Lv 1 "admin" 관리자님!
greetUserByRole(user3); // 안녕하세요. "guest" 게스트!
```




<br />
<br />




## 타입 호환

한 타입의 값이 다른 타입에 대입될 수 있는지를 판단하는 규칙이다. 이러한 타입 호환은 타입스크립트의 구조적 타입 시스템에 의해 동작된다. 타입을 비교할 때 타입의 구조를 기준으로 호환 여부를 판단한다.

```typescript
interface User {
  name: string;
  grade: '🫘' | '🌱' | '🌸';
  admin: false;
}

interface Guest {
  name: string;
}

const user1: User = {
  name: 'user',
  grade: '🫘',
  admin: false
};

const user2: Guest = {
  name: 'guest'
};

// Guest 타입은 name 속성만 존재하기에, name 속성을 가지고 있는 타입이라면 호환 가능하다.
function welcomGreet(user: Guest) {
  console.log(`안녕하세요. ${user.name}님!`);
}

welcomGreet(user1); // 안녕하세요. user님!
welcomGreet(user2); // 안녕하세요. guest님!
```




<br />
<br />




## 타입 연산자

### keyof 연산자

객체의 모든 키 이름을 타입으로 지정하여, 객체 타입의 키를 유니언 타입으로 추출 가능하다.

```typescript
interface Todo {
  id: number;
  title: string;
  content: string;
}

type TodoKeys = keyof Todo; // 'id' | 'title' | 'content'

function getProperty(obj: Todo, key: TodoKeys) {
  return obj[key]; // 객체의 속성값을 리턴
}

const todo: Todo = { id: 1, title: '제목', content: '내용' };
const id = getProperty(todo, 'id'); // 1
```

<br />

### typeof 연산자

값으로부터 타입을 반환하는 연산자이다.

```typescript
const kong = {
  name: '콩이',
  age: 10,
  address: '서울시'
};

type DogType = typeof kong; // { name: string; age: number; address: string; }

const dandan: DogType = {
  name: '단단',
  age: 11,
  address: '서울시'
};
```

<br />

### 인덱스 접근 타입 ( Indexed Access Types )

`객체 타입[속성명]` 형태로 그 속성 값의 타입을 가져오는 문법이다.

```typescript
// 타입의 특정 속성을 이용해 타입 추출
interface Todo {
  id: number;
  title: string;
  content: string;
}
type TodoTitle = Todo['title']; // string
type TodoIdOrContent = Todo['id' | 'content']; // number | string


// 배열 타입의 요소를 이용해 타입 추출
type TodoArray = {
  0: Todo;
  1: Todo;
  length: 2;
};
type FirstTodo = TodoArray[0]; // Todo
```