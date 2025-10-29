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
  - [숫자형 Enum](#숫자형-enum)
  - [문자열 Enum](#문자열-enum)
- [Union 타입]()
- [Intersection 타입]()
- [Interface 타입]()
- [타입 별칭(Type Alias)]()




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

### boolean

```typescript
let bool1: boolean = true;
let bool2: boolean = false;
```

### null

```typescript
let nullVal: null = null;
```

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

### array

같은 타입의 데이터를 순서대로 저장하는 배열

```typescript
let numbers: number[] = [ 1, 2, 3 ];
let alphabet: Array<string> = [ 'a', 'b', 'c' ];

// tuple : 배열의 길이와 타입이 고정된 배열
let dog: [string, number] = ['콩이', 10]
```

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
<br />




## Enum 타입

유사한 성격의 상수들을 **하나의 타입으로 묶어서 관리하는 열거형 데이터 타입**이다.

### 숫자형 Enum

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

### 문자열 Enum

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

### Enum 활용

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
<br />




## Union 타입

여러 종류의 타입 중 하나의 타입만 허용하는 **합지합 타입**이다. `|`(OR 연산자) 기호를 사용하여 연결한다.

```typescript
let value: number | string;
value = 100;
value = 'Hello';

function print(name: number | string): void {
  console.log(name);
}
print(100);
print('백');
```




<br />
<br />




## 타입 별칭(Type Alias)




<br />
<br />




## Intersection 타입




<br />
<br />




## Interface 타입