# 데이터 타입 ( Data Type )

- [타입 주석(Type Annotation)](#타입-주석--type-annotation)
- [기본 타입](#기본-타입)
  - [string](#string)
  - [number](#number)
  - [boolean](#boolean)
  - [null](#null)
  - [undefined](#ud)
- [참조 타입](#참조-타입)
  - [object](#object)
  - [array](#array)
  - [function](#function)
- [특수 타입](#특수-타입)
  - [any](#any)
  - [unknown](#unknown)
  - [void](#void)
  - [never](#never)
  - [Enum 타입](#enum-타입)
  - [리터럴 타입](#리터럴-타입)
- [타입 별칭(Type Alias)](#타입-별칭--type-alias)
  - [타입 별칭으로 객체 타입 선언](#타입-별칭으로-객체-타입-선언)
- [타입 조합](#타입-조합)
  - [Union 타입](#union-타입)
  - [Intersection 타입](#intersection-타입)
- [Interface 타입](#interface-타입)
  - [인터페이스 타입 사용](#인터페이스-타입-사용)
  - [선택적 프로퍼티(Optional Property)](#선택적-프로퍼티--optional-property-)
  - [읽기 전용 프로퍼티(readonly)](#읽기-전용-프로퍼티--readonly)
  - [인터페이스 상속](#인터페이스-상속)
  - [선언 병합](#선언-병합)
  - [상속과 선언 병합의 차이](#상속과-선언-병합의-차이)
  - [타입 별칭과 인터페이스의 차이점](#타입-별칭과-인터페이스의-차이점)
  - [인덱스 시그니처(Index Signature)](#인덱스-시그니처--index-signature-)




<br />
<br />




## 타입 주석 ( Type Annotation )

타입스크립트에서 타입을 정의할 땐 변수의 이름 뒤에 콜론(`:`)을 붙여 사용한다. 이 문법을 `타입 주석` 또는 `타입 어노테이션`이라고 부른다.

```typescript
let str: string = 'Hello TypeScript~!';
```




<br />
<br />




## 기본 타입

### string

```typescript
let str1: string = "Hello";
let str2: string = 'TypeScript';
let str3: string = `Hello TypeScript`;
```

<br />

### number

```typescript
let num1: number = 20;
num1 = -20; // 재할당
let num2: number = 0.2;
num2 = -0.2;
let num3: number = Infinity;
num3 = -Infinity;
let num4: number = NaN;
```

<br />

### boolean

```typescript
let bool1: boolean = true;
let bool2: boolean = false;
```

<br />

### null

```typescript
let nullVal: null = null;
```

<br />

### undefined

```typescript
let emptyVal: undefined = undefined;
```




<br />
<br />




## 참조 타입

### object

여러 속성을 묶어 표현하는 기본 객체

```typescript
let user1: object = {
  name: '콩이',
  age: 10,
  color: 'black',
};

let user2: {name: string; age: number} = {
  name: '콩이',
  age: 10,
};
```

<br />

### array

같은 타입의 데이터를 순서대로 저장하는 배열

```typescript
let numbers: number[] = [ 1, 2, 3 ];
let alphabet: Array<string> = [ 'a', 'b', 'c' ];

// tuple : 배열의 길이와 타입이 고정된 배열
let dog: [string, number] = ['콩이', 10]
```

<br />

### function

함수의 매개변수와 반환 타입을 정의

```typescript
function getCount(count: number): string {
  return 'Count: ' + count;
}
console.log(getCount(20)); // Count: 20

let print: (age: number) => string;
print = (age) => 'my age: ' + age;
console.log(print(31)); // my age: 31
```

#### 선택적 파라미터 ( Optional Parameter )

```typescript
function dog(name: string, age: number) {
  console.log(name, age);
}
dog('하루', 5); // 하루 5
dog('나무'); // An argument for 'age' was not provided.
// age 매개변수를 전달하지않아 코드상에서 에러가 발생한다.

// Optional Parameter
function dog(name: string, age?: number) {
  console.log(name, age);
}
dog('하루', 5); // 하루 5
dog('나무'); // 나무 undefined
```




<br />
<br />




## 특수 타입

### any

값의 타입을 정확히 모를 때 사용하는 타입이다. **변수의 모든 타입을 허용**한다. 그래서 타입에 대한 검사를 모두 통과하기 때문에 어떤 타입 오류를 잡아낼 수 없다. 이는 타입스크립트를 사용하는 의미가 사라지게되므로 되도록 안쓰는 것을 추천한다.

```typescript
let anyVal: any = 'Hello';
anyVal = 10;
anyVal = true;
anyVal = { };
anyVal = [ ];
anyVal = function () {};

console.log(anyVal.toUpperCase()); // TypeError: anyValue.toUpperCase is not a function
// 코드에서는 에러를 잡지 못하지만 런타임시 오류가 발생한다.
// 마지막에 함수를 할당하여 문자열 메서드인 toUpperCase()를 사용할 수 없다.
// 규모가 커지면 에러도 많이 발생하며 에러를 처리하기 어려울 수 있다.
```

<br />

### unknown

값의 타입을 아직 모를 때 사용하는 타입이다. 변수의 모든 타입을 허용한다. 하지만, 사용 전에 에러가 발생하여 **타입 검사를 통해 사용할 수 있도록 설계**해야 한다. `any`보다 안전한 대안이다.

```typescript
let user: unknown = 12;
user = true;
user = '콩이';

console.log(user.toUpperCase()); // 'user' is of type 'unknown'
// 코드에서 오류가 발생하는걸 볼 수 있다.
// 문자열일 수 있지만 보장되지 않아 사용할 수 없다.

// 타입 검사를 통해 값을 사용할 수 있다.
if (typeof user === 'string') {
  console.log(user.toUpperCase());
}
```

<br />

### void

아무 값도 없음을 의미하는 타입이다.

```typescript
let voidVal: void;
console.log(voidVal); // undefined

voidVal = undefined; // void 타입에는 undefined 값만 담을 수 있다.

// 반환 값이 없는 함수에서도 타입을 지정한다.
function printValue(): void {
  console.log('Hello');
}
```

<br />

### never

값이 존재할 수 없거나, 끝나지 않는 상황을 나타내는 타입이다.

```typescript
// 무한 반복으로 인해 끝나지 않는 상황
function infiniteLoop(): never {
  while (true) { }
}

// 조건문에 의해 모두 걸러지고 남는게 없을 경우
function check(value: string | number) {
  if (typeof value === 'string') {
    console.log(value.toUpperCase());
  } else if (typeof value === 'number') {
    console.log(value.toFixed(2));
  } else {
    const neverValue: never = value;
  }
}
check(undefined); // Argument of type 'boolean' is not assignable to parameter of type 'string | number'
// 코드 상에서 에러가 발생한다.
```

<br />

### Enum 타입

유사한 성격의 상수들을 **하나의 타입으로 묶어서 관리하는 열거형 데이터 타입**이다.

#### 숫자형 Enum

숫자 값이 자동으로 할당된다. 첫번 째 값은 0부터 시작하며, 이후 값은 1씩 증가한다.

```typescript
enum Language {
  C,          // 0
  Java,       // 1
  Python,     // 2
  Javascript  // 3
}

console.log(Language.Python); // 2
console.log(Language.Java); // 1
```

숫자 초기값을 지정할 수도 있다.

```typescript
enum Language {
  C = 2,          // 2
  Java,           // 3
  Python,         // 4
  Javascript      // 5
}

console.log(Language.Python); // 4
console.log(Language.Java); // 3
```

#### 문자열 Enum

명시적으로 문자열 값을 할당하여 명확한 의미 전달이 되어 가동성이 좋다.

```typescript
enum Language {
  C = 'C',
  Java = 'J',
  Python = 'PY',
  Javascript = 'JS'
}

console.log(Language.Python); // PY
console.log(Language.Java); // J
```

#### Enum 활용

```typescript
enum Language {
  C = 'C',
  Java = 'J',
  Python = 'PY',
  Javascript = 'JS'
}

function getLanguage(lang: Language) {
  console.log('전달받은 lang', lang);

  switch(lang) {
    case Language.C:
      console.log('C 언어');
      break;
    case Language.Java:
      console.log('자바 언어');
      break;
    case Language.Python:
      console.log('파이썬 언어');
      break;
    case Language.Javascript:
      console.log('자바스크립트 언어');
      break;
  }
}

getLanguage(Language.Javascript); // 전달받은 lang JS, 자바스크립트 언어
getLanguage(Language.Java); // 전달받은 lang J, 자바 언어
```

<br />

### 리터럴 타입

특정 `값` 자체를 타입으로 사용하여 잘못된 값의 입력을 막을 수 있어 타입 추론의 범위를 좁혀 안정성을 높일 수 있다.

```typescript
function wakeUpTime(name: '짱구' | '철수', time: 8 | 9) {
  console.log(`${name}야, 일어나! ${time}시야!`);
}

wakeUpTime('짱구', 8); // 짱구야, 일어나! 8시야!
wakeUpTime('철수', 9); // 철수야, 일어나! 9시야!
```




<br />
<br />




## 타입 별칭 ( Type Alias )

유니언 타입 같은 복잡한 타입을 의미있는 변수명을 붙여서 저장해서 사용할 수 있다. `type` 키워드를 사용하여 사용자 정의 타입을 선언한다. 동일한 이름으로 중복 선언은 불가하다.

#### 타입 별칭을 사용하지 않은 경우

```typescript
function log(name: number | string): void {
  console.log(name);
}

const name1: string | number = '오일영';
const name2: string | number = 510;

log(name1); // 오일영
log(name2); // 510
```

#### 타입 별칭을 사용한 경우

```typescript
// 관례적인 명명 규칙 : PascalCase 사용, 명사형 사용
type UserName = string | number;

function log(name: UserName): void {
  console.log(name);
}

const name1: UserName = '오일영';
const name2: UserName = 510;

log(name1); // 오일영
log(name2); // 510
```

#### 컴파일 된 후의 자바스크립트 파일

```typescript
function log(name) {
  console.log(name);
}

const name1 = '오일영';
const name2 = 510;

log(name1); // 오일영
log(name2); // 510
```

<br />

### 타입 별칭으로 객체 타입 선언

속성은 `,` 또는 `;`으로 구분할 수 있지만, 공식적으로 `;`을 사용하는 걸 권장한다.

```typescript
type Dog = {
  name: string;
  age: number;
}

const haru: Dog = { name: '하루', age: 10 };
// const haru: Dog = { name: '하루' } // 컴파일 에러, age 속성이 빠짐
// const haru: Dog = { name: '하루', age: '10' } // 컴파일 에러, age 속성 값이 number가 아님
```




<br />
<br />




## 타입 조합

### Union 타입

여러 종류의 타입 중 하나의 타입만 허용하는 **합지합 타입**이다. `|`(OR 연산자) 기호를 사용하여 연결한다.

```typescript
let value: number | string;
value = 100;
value = 'Hello';

function print(name: number | string): void {
  console.log(name);
}
print(100); // 100
print('백'); // 백
```

<br />

### Intersection 타입

타입 여러개를 `&`(AND 연산자)로 연결하여 하나로 합쳐 타입 별칭을 확장할 때 주로 사용한다.

```typescript
// 기본 타입에서는 겹치는 값이 존재하지 않으므로 never 타입으로 추론된다.
let value: number & string;
```

```typescript
type TodoRegist = {
  id: number;
  title: string;
  content: string;
};

type TodoInfo = TodoRegist & {
  id: number; // 동일한 속성을 추가해도 에러가 발생하지 않지만, 굳이 중복할 이유는 없다.
  // id: string; // 타입이 다르면 never 타입이 되면서 컴파일 에러가 발생한다.
  done: boolean;
};

const todo1: TodoRegist = {
  id: 10,
  title: '할 일 제목1',
  content: '할 일 내용1'
};

const todo2: TodoInfo = {
  id: 10,
  title: '할 일 제목1',
  content: '할 일 내용1',
  done: false
};

console.log(todo1); // {id: 10, title: '할 일 제목1', content: '할 일 내용1'}
console.log(todo2); // {id: 10, title: '할 일 제목1', content: '할 일 내용1', done: false}
```




<br />
<br />




## Interface 타입

객체의 타입을 정의하기 위해 사용한다. `interface` 키워드를 사용하여 사용자 정의 타입을 선언한다. 속성은 `,` 또는 `;`으로 구분할 수 있지만, 공식적으로 `;`을 사용하는 걸 권장한다.

```typescript
interface Dog {
  name: string;
  age: number;
}

const kong: Dog = { name: '콩이', age: 10 };
// const kong: Dog = { name: '콩이' }; // 컴파일 에러, age 속성이 없음
// const kong: Dog = { name: '콩이', age: '1' }; // 컴파일 에러, age 속성 값이 숫자가 와야함
// const kong: Dog = { name: '콩이', userAge: 10 }; // 컴파일 에러, age 속성이 없음
```

<br />

### 인터페이스 타입 사용

```typescript
interface User {
  name: string;
  age: number;
}

// 변수
const lion: Animal = { name: '사자', age: 15 };

// 함수의 매개 변수
const getAge = (animal: Animal): number => {
  return animal.age;
};

// 함수의 리턴
const createAnimal = (name: string, age: number): Animal => {
  return { name, age };
}
```

#### 클래스 타입 지정

클래스 명 뒤에 `implements` 키워드를 사용하여 `interface` 타입을 지정한다.

```typescript
interface Score {
  kor: number;
  eng: number;
  sum(): number;
  avg(): number;
}

class HighSchool implements Score {
  kor: number;
  eng: number;
  constructor (kor: number, eng: number) {
    this.kor = kor;
    this.eng = eng;
  }
  sum(): number {
    return this.kor + this.eng;
  }
  avg(): number {
    return this.sum() / 2;
  }
}

function printScore(score: Score): void {
  console.log(score.sum(), score.avg());
};

const baek: Score = new HighSchool(90, 90);

printScore(baek); // 180 90
```

<br />

### 선택적 프로퍼티 ( Optional Property )

객체의 속성을 선택적으로 부여하고 싶을 때, 인터페이스 속성명 뒤에 `?`를 추가하여 사용한다.

```typescript
interface Todo {
  id: number;
  title: string;
  content: string;
  done?: boolean;
}

const todo1: Todo = {
  id: 1,
  title: '할 일 제목 1',
  content: '할 일 내용 1',
  done: false
};

const todo2: Todo = {
  id: 2,
  title: '할 일 제목 2',
  content: '할 일 내용 2'
};
```

<br />

### 읽기 전용 프로퍼티 ( readonly )

객체 생성 시에만 값 할당이 가능하고 생성된 이후에는 수정할 수 없는 속성을 만들 때 사용한다. 인터페이스 속성명 앞에 `readonly` 키워드를 추가하여 사용한다. 

```typescript
interface Todo {
  id: number;
  readonly title: string;
  content: string;
  done?: boolean;
}

const todo1: Todo = {
  id: 1,
  title: '할 일 제목 1',
  content: '할 일 내용 2',
  done: false
};

todo1.content = '할 일 내용 1';
console.log(todo1); // {id: 1, title: '할 일 제목 1', content: '할 일 내용 1', done: false}

const todo2: Todo = {
  id: 2,
  title: '할 일 제목 3',
  content: '할 일 내용 2',
  done: false
};

// todo2.title = '할 일 내용 2'; // 컴파일 에러, title는 readonly이므로 수정 불가
console.log(todo2); // {id: 2, title: '할 일 제목 3', content: '할 일 내용 2', done: false}
```

<br />

### 인터페이스 상속

부모 인터페이스의 속성과 메서드를 자식 인터페이스가 물려받아 확장할 수 있다. `interface` 선언부의 `extends` 키워드 뒤에 상속받을 부모 인터페이스를 지정하면 된다.

```typescript
interface TodoRegist {
  title: string;
  content: string;
}

interface TodoInfo extends TodoRegist {
  id: number;
  done: boolean;
}

const todo: TodoRegist = {
  title: '할 일 제목 1',
  content: '할 일 내용 1'
};

const todoInfo: TodoInfo = {
  id: 1,
  title: '할 일 제목 1',
  content: '할 일 내용 1',
  done: false
};

console.log(todo); // {title: '할 일 제목 1', content: '할 일 내용 1'}
console.log(todoInfo); // {id: 1, title: '할 일 제목 1', content: '할 일 내용 1', done: false}
```

#### 계층 구조 상속

인터페이스 상속은 여러 단계의 계층 구조로 구성 가능하다.

```typescript
interface TodoRegist {
  title: string;
  content: string;
}

interface TodoInfo extends TodoRegist {
  id: number;
  done: boolean;
}

interface TodoInfoDate extends TodoInfo {
  createdAt: Date;
  updatedAt: Date;
}

const todo: TodoRegist = {
  title: '할 일 제목 1',
  content: '할 일 내용 1'
};

const todoInfo: TodoInfo = {
  id: 2,
  title: '할 일 제목 2',
  content: '할 일 내용 2',
  done: false
};

const todoInfoDate: TodoInfoDate = {
  id: 3,
  title: '할 일 제목 3',
  content: '할 일 내용 3',
  done: false,
  createdAt: new Date(),
  updatedAt: new Date(),
};

console.log(todo); // {title: '할 일 제목 1', content: '할 일 내용 1'}
console.log(todoInfo); // {id: 1, title: '할 일 제목 1', content: '할 일 내용 1', done: false}
console.log(todoInfoDate); // {id: 3, title: '할 일 제목 3', content: '할 일 내용 3', done: false, createdAt: Wed Oct 29 2025 22:52:40 GMT+0900 (한국 표준시), …}
```

#### 다중 상속

둘 이상의 인터페이스를 상속 받은 구조로 구성 가능하다.

```typescript
interface TodoRegist {
  title: string;
  content: string;
}

interface TodoInfo extends TodoRegist {
  id: number;
  title: string; // 동일한 속성이 중복으로 존재해도 가능하지만, 타입이 동일해야 한다.
  done: boolean;
}

interface TodoInfoDate extends TodoRegist, TodoInfo {
  createdAt: Date;
  updatedAt: Date;
}

const todo: TodoRegist = {
  title: '할 일 제목 1',
  content: '할 일 내용 1'
};

const todoInfo: TodoInfo = {
  id: 2,
  title: '할 일 제목 2',
  content: '할 일 내용 2',
  done: false
};

const todoInfoDate: TodoInfoDate = {
  id: 3,
  title: '할 일 제목 3',
  content: '할 일 내용 3',
  done: false,
  createdAt: new Date(),
  updatedAt: new Date(),
};

console.log(todo); // {title: '할 일 제목 1', content: '할 일 내용 1'}
console.log(todoInfo); // {id: 1, title: '할 일 제목 1', content: '할 일 내용 1', done: false}
console.log(todoInfoDate); // {id: 3, title: '할 일 제목 3', content: '할 일 내용 3', done: false, createdAt: Wed Oct 29 2025 22:52:40 GMT+0900 (한국 표준시), …}
```

<br />

### 선언 병합

동일한 이름의 인터페이스를 **중복으로 선언하여 기존 인터페이스에 없는 속성을 추가해서 확장**할 수 있다. 이때, 기존 속성과 중복으로 정의는 가능하지만 타입은 동일해야 한다.

```typescript
interface Todo {
  id: number;
  title: string;
  content: string;
}

interface Todo {
  // title: number; // 컴파일 에러, 타입이 다르다.
  title: string; // 중복으로 정의는 가능하지만 굳이 필요하진 않다.
  done: boolean;
}

const todo: Todo = {
  id: 1,
  title: '할 일 제목 1',
  content: '할 일 내용 1',
  done: true
};
```

<br />

### 상속과 선언 병합의 차이

`상속`은 새로운 인터페이스를 생성해서 기존의 인터페이스를 확장할 수 있다. 즉, 부모 인터페이스의 타입을 상속받고 자식 인터페이스에 새로운 속성을 추가하여 자식 인터페이스를 만들 수 있다.

```typescript
interface Todo {
  id: number;
  title: string;
}

interface TodoInfo extends Todo {
  content: string;
  done: boolean;
}
// TodoInfo는 id, title, content, done 상속 받은 속성과 새로운 속성을 모두 가진다.
```

`선언병합`은 동일한 이름의 인터페이스를 재선언하여 자동으로 병합할 수 있다. 즉, 하나의 인터페이스에 여러 속성을 추가한다.

```typescript
interface Todo {
  id: number;
  title: string;
}

interface Todo {
  content: string;
  done: boolean;
}
// Todo 인터페이스가 병합되어 하나의 Todo가 된다.
// Todo는 id, title, content, done 모든 속성을 가진다.
```

`상속`은 부모와 자식 관계를 명시적으로 표현하며, 각 계층에 해당하는 인터페이스를 각각 활용하여 사용할 수 있다. `선언병합`은 이미 존재하는 외부 라이브러리에 속성을 추가해서 사용하거나 전역 타입 확장에 유용하게 사용할 수 있다.

<br />

### 타입 별칭과 인터페이스의 차이점

```typescript
// 타입 별칭
type UserName = string | number;
type User = {
  name: string;
  age: number;
};

// 인터페이스
interface User {
  name: string;
  age: number;
}
```

#### 타입 별칭 

- 객체, 기본 타입, 유니언 타입, 인터섹션 타입 등 모든 타입에서 사용 가능하다.
- 타입 확장은 `&` 인터섹션 타입으로 확장 가능하다. 
- 객체가 아닌 타입 별칭으로만 정의할 수 있는 경우에는 타입 별칭 사용을 권장한다.

#### 인터페이스

- 객체, 클래스의 타입을 정의할 때 사용한다.
- 타입 확장은 `extends` 키워드를 사용하거나 `선언병합`을 통해 확장 가능하다.
- 객체의 타입을 지정하는 경우 확장이 용이한 인터페이스 사용을 권장한다.

<br />

### 인덱스 시그니처 ( Index Signature )

속성명을 명시하지 않고 **속성명의 타입과 속성값의 타입을 미리 정의해두어 사용**한다. 동일한 타입을 가진 여러 속성들을 하나로 정의 가능하다.

```typescript
interface User {
  name: string;
  email: string;

  // 인덱스 시그니처
  [key: string]: string; // 문자열로 표현할 수 있는 모든 값이 들어올 수 있다.
}

const user: User = {
  name: '유저',
  email: 'user@gmail.com',
  phone: '010-2222-3333',
  address: '서울시'
};
```

#### 주의사항

- 인덱스 시그니처의 키는 `string`, `number`, `symbol` 타입만 가능하다
- 정의한 다른 타입들도 같은 타입을 가져야 에러가 발생하지 않는다.
- 인덱스 시그니처에 정의한 속성명 `key` 대신 다른 문자를 사용해도 된다.
- 동적 속성을 가진 객체에 유용하게 사용할 수 있다.