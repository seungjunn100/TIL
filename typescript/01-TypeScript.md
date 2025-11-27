# TypeScript란 무엇인가

- [타입스크립트란](#타입스크립트란)
  - [타입스크립트 동작 방식](#타입스크립트-동작-방식)
- [개발 환경 설정](#개발-환경-설정)
  - [타입스크립트 환경 설정 tsconfig.json](#타입스크립트-환경-설정-tsconfigjson)




<br />
<br />




## 타입스크립트란

자바스크립트는 런타임시 타입이 결정되는 `약형(Weakly Typed) 언어`이다. 즉, 코드를 작성하는 도중에 변수의 타입을 지정하지 않아도 되고, 실행 도중에 자유롭게 변경할 수 있다. 이러한 특징들은 예상치 못한 **타입 오류로 인해 런타임시 에러가 발생할 가능성이 높아**지게 된다.

이러한 문제점을 보완하기 위해 **타입스크립트가 등장**했다. 타입스크립트는 자바스크립트를 기반으로 하며, 추가적으로 타입을 부여하여 코드를 안전하게 관리할 수 있고 코드의 의도를 명확하게 이해할 수 있기 때문에 `강형(Strongly Typed) 언어`에 가깝게 사용할 수 있다.

타입스크립트는 런타임 전에 에러를 미리 잡기 위한 도구로 사용된다.

<br />

### 타입스크립트 동작 방식

브라우저는 자바스크립트 언어만 이해할 수 있다. 그래서 타입스크립트 코드는 자바스크립트 코드로 컴파일해서 사용할 수 있다. 이때 `TypeScript Compiler(tsc)`를 사용하며, 타입 검사를 통해 오류를 찾으면 컴파일 타임에 에러를 검출할 수 있다. 타입 관련 에러가 발생해도 컴파일되어 자바스크립트 파일이 생성된다.

#### 타입스크립트 코드

```typescript
// sum.ts
function sum(a: number, b: number): number {
  return a + b;
}
sum(10, 20);
```

#### 타입스크립트 컴파일 (TypeScript Compiler(tsc))

```
$ tsc sum.ts
```
새로운 `sum.js` 파일이 생성된다.

#### 컴파일된 자바스크립트 코드

```typescript
// sum.js
function sum(a, b) {
  return a + b;
}
sum(10, 20);
```




<br />
<br />




## 개발 환경 설정

[Node.js](https://nodejs.org/en/download)를 설치한 뒤 `VSCode` 터미널에서 명령어를 통해 타입스크립트를 설치할 수 있다.

```bash
# 설치
npm i -g typescript

# 설치 후 버전 확인 
tsc --version
tsc -v
```

<br />

### 타입스크립트 환경 설정 `tsconfig.json`

컴파일러의 컴파일 옵션을 지정할 수 있는 파일이다. `tsconfig.json` 파일 없이 tsc 명령을 실행하면, 기본 설정만을 사용하여 컴파일 한다.

`tsconfig.json` 파일을 생성하기 위해 명령어를 실행해야한다.

```bash
tsc --init
```

#### 자주 사용하는 `tsconfig.json` 설정

```json
{
  "compilerOptions": {
    "target": "ES2020", // 어떤 버전의 자바스크립트로 변환할지 지정
    "module": "ESNext", // 모듈 시스템 지정
    "strict": true, // 가장 중요한 타입 안전 옵션
    /*
      아래의 세부 옵션들을 한번에 켠다.
      - noImplicitAny
      - strictNullChecks
      - strictBindCallApply
      - strictFunctionTypes
      - alwaysStrict
    */
    "jsx": "react-jsx", // React 17 이상에서 JSX 변환 방식을 사용하도록 설정
    "moduleResolution": "Node", // Node.js 방식으로 모듈을 해석하도록 설정
    "esModuleInterop": true, // CommonJS 모듈(require)과 ES 모듈(import)을 호환되게 해주는 설정
    "forceConsistentCasingInFileNames": true, // 대소문자 불일치 에러를 방지
    "skipLibCheck": true, // 외부 라이브러리 타입 검사 생략
    "outDir": "./dist", // 출력(컴파일 결과) 디렉토리를 지정
    "rootDir": "./src", // 입력(소스) 디렉토리를 지정
    "baseUrl": "./src", // 모듈을 불러올 때 기준이 되는 기본 경로를 지정
    "paths": {
      "@/*": ["*"] // @/로 src 내부를 참조할 수 있도록 별칭 설정
    },
    "sourceMap": true, // 디버깅용 소스맵 생성
    "noImplicitAny": true // 타입을 명시하지 않은 변수에 자동으로 any가 붙는걸 방지
  },
  "include": ["src"], // 컴파일 대상 폴더를 지정
  "exclude": ["node_modules", "dist"] // 컴파일 제외 폴더를 지정
}
```

<br />

#### `tsc --watch` 옵션

하위 폴더를 포함해서 타입스크립트 파일 변경을 감지하고 자동으로 컴파일한 후 outDir로 지정한 폴더에 자바스크립트 파일을 생성한다.

`tsconfig.json` 파일이 있는 폴더에서 명령어를 실행해야 한다.

```
$ tsc --watch
```