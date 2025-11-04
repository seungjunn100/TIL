# 엄격 모드 ( Strict Mode )

- ["use strict" 란](#use-strict-란)
- [엄격 모드에서 적용되는 주요 규칙](#엄격-모드에서-적용되는-주요-규칙)
  - [암묵적 전역 변수 금지](#암묵적-전역-변수-금지)
  - [`this`는 `window`가 아닌 `undefined`](#this는-window가-아닌-undefined)
  - [중복된 매개변수 사용 금지](#중복된-매개변수-사용-금지)
  - [미래에 사용될 수 있는 예약어 사용 금지](#미래에-사용될-수-있는-예약어-사용-금지)




<br />
<br />




## "use strict" 란

기존 자바스크립트의 느슨한 문법을 엄격하게 검사하는 모드를 말한다. 명시적인 에러로 강제하여 코드 품질을 높이고 미래 자바스크립트 문법과 호환되는 코드를 작성할 수 있게된다.

타입스크립트 `tsconfig.json` 파일에 `"strict": true` 나 `"alwaysStrict": true`로 설정하면 컴파일된 자바스크립트 파일에 `"use strict"`가 자동으로 추가된다.




<br />
<br />




## 엄격 모드에서 적용되는 주요 규칙

### 암묵적 전역 변수 금지

```typescript
'use strict';
function test() {
  x = 100; // ❌ ReferenceError
}
```

<br />

### `this`는 `window`가 아닌 `undefined`

```typescript
'use strict';
function print() {
  console.log(this); // undefined
}
```

<br />

### 중복된 매개변수 사용 금지

```typescript
'use strict';
function sum(a, a) { // ❌ SyntaxError
  return a + a;
}
```

<br />

### 미래에 사용될 수 있는 예약어 사용 금지

- `implements`, `interface`, `package`, `private`, `public`, `protected` 등