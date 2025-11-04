# ESM(ECMAScript Modules)

- [모듈이란](#모듈이란)
- [export](#export)
  - [Named Export](#named-export)
  - [Default Export](#default-export)
- [import](#import)
  - [Named Import](#named-import)
  - [Default Import](#default-import)
  - [Mixed Import](#mixed-import)
  - [Type Import](#type-import)
  - [Dynamic Import](#dynamic-import)
- [CJS와 ESM 차이](#cjs와-esm-차이)
  - [CJS ( CommonJS )](#cjs--commonjs)
  - [ESM ( ECMAScript Modules )](#esm--ecmascript-modules)




<br />
<br />




## 모듈이란

일반 `<script>`는 모두 전역 스코프를 공유하여 다른 파일에 있는 변수나 함수를 다른 파일에서 바로 사용할 수 있다. 전역에서 공유가 되기 때문에, 이름이 충될되어 에러가 발생할 가능성이 크다.

```html
<script src="math.js"></script>
<script src="index.js"></script>
```

```typescript
// math.js
function plus(a: number, b: number) { return a + b; }
function minus(a: number, b: number) { return a - b; }
```

```typescript
// index.js
plus(10, 20);
minus(10, 20);
```

`모듈(module)`은 코드의 일부를 독립된 파일 단위로 분리한 것이다. 불필요한 전역 오염 없이 재사용할 수 있게된다. 즉, 각 파일이 하나의 모듈이며, 모듈끼리 서로 내보내기(`export`)와 가져오기(`import`)를 통해 재사용할 수 있다.

브라우저에서 모듈을 사용하려면, `HTML`에서 `<script>` 태그에 `type="module"`을 지정해야 한다.

```html
<script type="module" src="math.js"></script>
<script type="module" src="index.js"></script>
```

```typescript
// math.js
export function plus(a: number, b: number) { return a + b; }
export function minus(a: number, b: number) { return a - b; }
```

```typescript
// index.js
import { plus, minus } from './math.js';
```




<br />
<br />




## `export`

모듈에서 변수, 함수, 클래스, 타입 별칭, 인터페이스 등을 외부로 내보내 다른 파일에서 사용할 수 있게 해준다.

<br />

### `Named Export`

#### math.js (`export`)

```typescript
// 방법 1
export function plus(a: number, b: number) { return a + b; }
export function minus(a: number, b: number) { return a - b; }

// 방법 2
export { plus, minus };
```

#### index.js (`import`)

`import` 시 중괄호 안에 정확한 구성 요소명을 지정해야한다.

```typescript
import { plus, minus } from './math.js';
```

<br />

### `Default Export`

#### math.js (`export`)

모듈 내에서 대표로 내보낼 값으로 한번만 사용 가능하다.

```typescript
export default function multiply(a: number, b: number) { return a * b; }
```

#### index.js (`import`)

`import` 시 중괄호 없이 자유롭게 이름을 지정할 수 있다.

```typescript
import MyMath from './math.js';
```




<br />
<br />




## `import`

다른 파일에서 `export`된 요소를 가져올 때 사용한다.

<br />

### `Named Import`

#### math.js (`export`)

```typescript
export function plus(a: number, b: number) { return a + b; }
export function minus(a: number, b: number) { return a - b; }
```

#### index.js (`import`)

이름이 정확히 일치 해야 하며 필요한 것만 선택해서 `import` 가능하다. `as`를 이용해서 다른 이름으로 변경해서 사용 가능하다.

```typescript
import { plus as add, minus } from './math.js';
```

<br />

### `Default Import`

#### math.js (`export`)

```typescript
export default function multiply(a: number, b: number) { return a * b; }
```

#### index.js (`import`)

```typescript
import MyMath from './math.js';
```

<br />

### `Mixed Import`

`Named Import`와 `Default Import`를 같이 사용할 수 있지만, 가독성 측면에서 권장하지 않는다.

#### math.js (`export`)

```typescript
export function plus(a: number, b: number) { return a + b; }
export function minus(a: number, b: number) { return a - b; }
export default function multiply(a: number, b: number) { return a * b; }
```

#### index.js (`import`)

```typescript
import MyMath, { plus, minus } from './math.js';
```

<br />

### `Type Import`

타입 별칭이나 인터페이스를 export 했을 경우 import 시 type 키워드를 추가헤서 사용한다.

#### math.js (`export`)

```typescript
function printUser(user: User) {
  console.log(`${user.name} ${user.age}`);
}

export type User = {
  name: string;
  age: number;
}
```

#### index.js (`import`)

```typescript
// 방법 1
import type { User } from './math.js';
import { printUser } from './math.js';

// 방법 2
import { type User, printUser } from './math.js';
```

<br />

### `Dynamic Import`

보통 일반적인 `import`는 정적 방식으로 코드가 실행되기 전에 모듈을 미리 불러와 `import`가 완료되어야 한다.

```typescript
import { plus } from './math.js';
console.log('프로그램 실행되기 전');
```

반면 `Dynamic Import`는 `import()` 함수 형태로 사용하여 동적 방식으로 코드가 실행되는 시점에 모듈을 불러올 수 있다.

```typescript
// async/await 방식
async function loadModule() {
  const module = await import('./math.js');
  console.log(module.plus(10, 20));
}

// Promise 방식
import('./math.js').then((module) => {
  console.log(module.plus(10, 20));
});

// 조건부 로딩
if (condition) {
  const module = await import('./module1.js');
} else {
  const module = await import('./module2.js');
}
```




<br />
<br />




## CJS와 ESM 차이

### CJS ( CommonJS )

브라우저 밖에서 실행되는 자바스크립트를 위한 묘듈 규격이다. 주로 `Node.js`에서 모듈화를 위해 사용한다.

#### math.js (`module.exports`)

```typescript
function plus(a, b) {
  return a + b;
}
module.exports = { plus };

```

#### index.js (`require`)

```typescript
const math = require('./math');
console.log(math.plus(2, 3));
```

#### Node.js에서의 파일 확장자

- `.js` : `package.json`에 `"type": "module"` 속성이 있을 경우 ESM 방식으로, 해당 속성이 없을 경우 CJS 방식으로 사용한다.
- `.cjs` : 무조건 CJS 방식의 모듈 사용
- `.mjs` : 무조건 ESM 방식의 모듈 사용

<br />

### ESM ( ECMAScript Modules )

ES6(2015)에서 도입된 자바스크립트의 공식 모듈 표준이다.

#### math.js (`export`)

```typescript
export function plus(a: number, b: number) { return a + b; }
```

#### index.js (`import`)

```typescript
import { plus } from './math.js';
```