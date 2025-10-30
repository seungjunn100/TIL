# 제네릭 ( Generic )

- [제네릭](#제네릭)
  - [제네릭 타입 제약](#제네릭-타입-제약)
  - [제네릭 사용](#제네릭-사용)




<br />
<br />




## 제네릭

함수를 정의할 때 타입을 미리 정하지 않고 함수를 호출할 때 타입을 지정해서 사용할 수 있다. 즉, 하나의 함수를 통해 다양한 타입의 데이터를 받을 수 있다.

```typescript
// string 타입만 받을 수 있는 함수
function getText(text: string): string {
  return text;
}
console.log(getText('Hello')); // Hello
// console.log(getText(100)); // 타입 에러


// 제네릭 함수
function getData<T>(data: T): T {
  return data;
}
console.log(getData<string>('Hello')); // Hello
console.log(getData<number>(100)); // 100
console.log(getData<boolean>(true)); // true

// 매개변수와 리턴값의 타입을 다르게 설정해도 된다.
function getData<T>(data: T): string {
  return 'string ' + data;
}
```

<br />

### 제네릭 타입 제약

제네릭에 전달받을 타입을 지정한 타입만 가능하도록 제약할 수 있다. `extends` 키워드를 사용하여 제약할 수 있다.

```typescript
function getData<T extends string | number>(data: T): T {
  return data;
}
console.log(getData<string>('Hello')); // Hello
console.log(getData<number>(100)); // 100
// console.log(getData<boolean>(true)); // 타입 에러, 문자열과 숫자만 받으므로

function getData<T extends { length: number }>(data: T): void {
  console.log(data.length);
}

getData<string>('Hello'); // 5
getData<number[]>([1, 2, 3, 4]); // 4
```

<br />

### 제네릭 사용

```typescript
// 함수
function getData<T>(data: T): T {
  return data;
}

// 인터페이스
interface User<T> {
  name: string;
  value: T;
}

// 클래스
class List<T> {
  private items: T[] = [];
  add(item: T) {
    this.items.push(item);
  }
  getAll(): T[] {
    return this.items;
  }
}

const numList = new List<number>();
numList.add(100.123);
numList.add(100.456);
console.log(numList.getAll()); // [100.123, 100.123456]
console.log(numList.getAll()[0]?.toFixed(2)); // 100.12

const strList = new List<string>();
strList.add('Hello');
strList.add('World');
console.log(strList.getAll()); // ['Hello', 'World']
console.log(strList.getAll()[1]?.toUpperCase()); // HELLO
```