# 유틸리티 ( Utility ) & 맵드( Mapped ) 타입

- [유틸리티 타입](#유틸리티-타입)
  - [Readonly`<T>`](#readonlyt)
  - [Required`<T>`](#requiredt)
  - [Partial`<T>`](#partialt)
  - [Pick`<T, K>`](#pickt-k)
  - [Omit`<T, K>`](#omitt-k)
  - [Record`<K, T>`](#recordk-t)
- [맵드 타입](#맵드-타입)
  - [기본 문법](#기본-문법)
  - [기존 타입 유지하며 속성 변형](#기존-타입-유지하며-속성-변형)
  - [유틸리티 타입의 구현 원리](#유틸리티-타입의-구현-원리)




<br />
<br />




## 유틸리티 타입

정의되어 있는 타입을 기반으로 변형하거나 재활용해서 새로운 타입을 반환하는 내장 타입이다. 대상 타입은 변경되지 않고 새로운 타입을 생성한다.

[다양한 유틸리티 타입](https://www.typescriptlang.org/ko/docs/handbook/utility-types.html)

<br />

### Readonly`<T>`

타입의 모든 속성을 `읽기 전용(readonly)`으로 설정한 타입을 생성한다.

```typescript
interface Todo {
  title: string;
  content: string;
}

const todo: Readonly<Todo> = {
  title: '할 일',
  content: '내용'
};

// todo.title = '내일로 미루기'; // 읽기 전용 속성이라 수정 불가
```

<br />

### Required`<T>`

타입의 모든 속성을 `필수(required)`로 설정한 타입을 생성한다.

```typescript
interface Todo {
  title: string;
  content?: string; // 옵셔널 프로퍼티
}

const todo1: Todo = {
  title: '할 일',
};

const todo2: Required<Todo> = {
  title: '할 일',
  // content: '내용' // 옵셔널 프로퍼티를 필수로 변경하여 생략하면 컴파일 에러 발생
};
```

<br />

### Partial`<T>`

타입의 모든 속성을 `선택적(optional)`으로 설정할 수 있는 타입을 생성한다.

```typescript
interface Todo {
  title: string;
  content: string;
}

const todo1: Todo = {
  title: '할 일',
  content: '내용'
};

const todo2: Required<Todo> = {
  title: '할 일',
};
```

<br />

### Pick`<T, K>`

타입의 속성에서 `특정 속성만 선택`해서 사용할 수 있는 타입을 생성한다.

```typescript
interface Todo {
  id: number;
  title: string;
  content?: string; // 원래 속성의 특징을 그대로 받는다.
  done: boolean;
  createdAt: Date;
  updatedAt: Date;
}

// 단일 속성이나 유니온 타입으로 여러 속성 조합이 가능하다.
type TodoRegist = Pick<Todo, 'title' | 'content'>;

const todo1: TodoRegist = {
  title: '할 일 1',
};

const todo2: TodoRegist = {
  title: '할 일 2',
  content: '내용 2'
};
```

<br />

### Omit`<T, K>`

타입의 속성에서 `특정 속성만 제외`하여 사용할 수 있는 타입을 생성한다.

```typescript
interface Todo {
  id: number;
  title: string;
  content: string;
  done: boolean;
  createdAt: Date;
  updatedAt: Date;
}

type TodoInfo = Omit<Todo, 'createdAt' | 'updatedAt'>;

const todo: TodoInfo = {
  id: 1,
  title: '할 일 1',
  content: '내용 1'
  done: false
};
```

<br />

### Record`<K, T>`

주어진 `키의 타입(K)`에 `동일한 타입(T)`을 `할당`하여 사용할 수 있는 타입을 생성한다.

```typescript
type UserRole = 'admin' | 'user' | 'guest';
type UserPermissions = Record<UserRole, string[]>;

const permissions: UserPermissions = {
  admin: ['read', 'write', 'delete'],
  user: ['read', 'write'],
  guest: ['read']
};
```




<br />
<br />




## 맵드 타입

기존 객체 타입의 모든 속성을 순회(map)하면서 각각의 속성 타입을 변형하거나 새로 정의하는 타입 문법이다.

<br />

### 기본 문법

```typescript
interface UserFields {
  id: number;
  name: string;
  address: string;
  phone: string;
}

// keyof UserFields = 'id' | 'name' | 'address' | 'phone'
type User = {
  [K in keyof UserFields]: string;
};
// 각 속성(keyof UserFields)을 순회하면서 속성(K)의 타입(string)을 지정한다.

const user: User = {
  id: '1',
  name: '백',
  address: '서울시',
  phone: '010-2222-3333'
};
```

<br />

### 기존 타입 유지하며 속성 변형

속성의 특성(`?`, `readonly`)을 변경할 수 있다.

#### 옵셔널 ( `?` )

`Partial<T>`의 원리

```typescript
// 옵셔널(?) 추가
interface Todo {
  id: number;
  title: string;
  done: boolean;
}

type OptionalTodo = {
  [K in keyof Todo]?: Todo[K];
};
/*
  id?: number;
  title?: string;
  done?: boolean;
*/

// 옵셔널(?) 삭제
interface Todo {
  id: number;
  title?: string;
  done: boolean;
}

type OptionalTodo = {
  [K in keyof Todo]-?: Todo[K];
};
/*
  id: number;
  title: string;
  done: boolean;
*/
```

#### 읽기 전용 ( `readonly` )

`Readonly<T>`의 원리

```typescript
// readonly 추가
interface Todo {
  id: number;
  title: string;
  done: boolean;
}

type OptionalTodo = {
  readonly [K in keyof Todo]: Todo[K];
};
/*
  readonly id: number;
  readonly title: string;
  readonly done: boolean;
*/

// readonly 삭제
interface Todo {
  readonly id: number;
  readonly title: string;
  readonly done: boolean;
}

type OptionalTodo = {
  -readonly [K in keyof Todo]: Todo[K];
};
/*
  id: number;
  title: string;
  done: boolean;
*/
```

<br />

### 유틸리티 타입의 구현 원리

유틸리티 타입은 맵드 타입을 기반으로 만들어 졌다.

```typescript
// Partial<T>의 내부 구현
type MyPartial<T> = {
  [P in keyof T]?: T[P];
};

// Readonly<T>의 내부 구현
type MyReadonly<T> = {
  readonly [P in keyof T]: T[P];
};

// Pick<T, K>의 내부 구현
type MyPick<T, K extends keyof T> = {
  [P in keyof K]: T[P];
};
```