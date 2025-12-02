# 빌드 도구 `Vite`

- [빌드 도구](#빌드-도구)
  - [Vite](#vite)




<br />
<br />




## 빌드 도구

프론트엔드 개발에 필요한 환경을 자동으로 구축해주는 도구로 다양한 기능들을 제공한다.

- 반복적으로 사용하는 프로젝트 기본 구조 자동 생성 (보일러플레이트 제공)
  
- 개발 서버, 번들링 설정 등 설정 파일을 자동 구성

- 필요한 라이브러리 기본 구성 (의존성 설치)

- `HMR(Hot Module Replacement)`: 코드 수정 시 새로고침 없이 화면 즉시 갱신

- 프로덕션 배포를 위한 번들링 기능 제공

  - 배포를 위한 `JS/CSS` 최적화 및 묶는 작업

  - 번들링 도구: `Webpack`, `Rollup`, `Parcel`, `ESBuild` 등

<br />

### Vite

그 중 하나가 `Vite`이며, 프랑스어로 `빠르다`는 의미의 차세대 프론트엔드 개발 도구이다.

- `Webpack`을 번들러로 사용하는 `CRA(create-react-app)` 대비, 10~100배 빠른 개발 서버 속도를 제공

- `React`, `Svelte`, `Solid` 등 다양한 `SPA` 개발 환경을 지원한다.

- `Dev server`에서는 `ESBuild`가 담당

  - 파일을 수정하면 `HMR`로 즉시 반영되어 개발 효율 높음
  
- `build`시 `Rollup` 기반 번들링

  - 트랜스파일링(컴파일) - JSX 문법을 Javascript 코드로 변환

  - Tree-Shaking(필요없는 것은 제거), 압축 등 최적화 수행

  - 결과물은 모두 하나의 번들로 묶여 `dist` 폴더에 생성

  ```html
  <script type="module" src="/assets/index-xxxx.js"></script>
  <link rel="stylesheet" href="/assets/index-xxxx.css" />
  ```

  - 불필요한 공백 제거/변수명, 함수명 축소로 바이트 절약

  - `public` 폴더의 파일은 그대로 `dist`로 복사

    - 경로는 항상 루트(/) 기준으로 접근




<br />
<br />




## import에서 사용할 별칭(alias) 추가