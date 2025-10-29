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

```node
npm i -g typescript
```

<br />

### 타입스크립트 환경 설정 `tsconfig.json`

```json
{
  // Visit https://aka.ms/tsconfig to read more about this file
  "compilerOptions": {
    // File Layout
    "rootDir": "./", // 컴파일할 소스 파일의 루트 경로
    // "outDir": "./dist", // 컴파일된 JS 파일을 저장할 경로

    // Environment Settings
    // See also https://aka.ms/tsconfig/module
    "module": "es2022", // 모듈 시스템 (import/export 방식)
    "target": "es2022", // 변환할 자바스크립트 버전
    "types": [], // 전역 타입 정의 파일(.d.ts) 사용 안 함
    // For nodejs:
    // "lib": ["esnext"], // 사용할 내장 라이브러리(JS 기능 수준)
    // "types": ["node"], // Node.js 타입 정의 사용
    // and npm install -D @types/node // Node 타입 설치 명령어

    // Other Outputs
    // "sourceMap": true, // 디버깅용 소스맵 파일 생성
    // "declaration": true, // 타입 선언 파일(.d.ts) 생성
    // "declarationMap": true, // 선언 파일용 소스맵 생성

    // Stricter Typechecking Options
    "noUncheckedIndexedAccess": true, // 배열/객체 인덱스 접근 시 undefined 고려
    "exactOptionalPropertyTypes": true, // 선택적 속성은 undefined만 허용 (엄격)

    // Style Options
    // "noImplicitReturns": true, // 모든 함수는 반드시 return 명시
    // "noImplicitOverride": true, // 상속 메서드 override 시 명시적으로 표시 필요
    // "noUnusedLocals": true, // 사용 안 한 지역 변수 있으면 에러
    // "noUnusedParameters": true, // 사용 안 한 매개변수 있으면 에러
    // "noFallthroughCasesInSwitch": true, // switch 문에서 break 누락 방지
    // "noPropertyAccessFromIndexSignature": true, // 인덱스 시그니처로 정의된 속성 접근 제한

    // Recommended Options
    "strict": true, // 모든 엄격한 타입 검사 활성화
    "jsx": "react-jsx", // React JSX 문법 지원
    "verbatimModuleSyntax": true, // import/export 문법 그대로 유지
    "isolatedModules": true, // 각 파일을 독립적으로 컴파일 가능하게
    "noUncheckedSideEffectImports": true, // 부수효과(import 시 실행) 있는 파일 검사
    "moduleDetection": "force", // 모든 JS/TS 파일을 모듈로 간주
    "skipLibCheck": true, // 외부 라이브러리 타입 검사 생략(속도↑)
  }
}

```

<br />

#### `tsc --watch` 옵션

하위 폴더를 포함해서 타입스크립트 파일 변경을 감지하고 자동으로 컴파일한 후 outDir로 지정한 폴더에 자바스크립트 파일을 생성한다.

`tsconfig.json` 파일이 있는 폴더에서 명령어를 실행해야 한다.

```
$ tsc --watch
```