# Node.js와 관리 도구들

- [Node.js](#nodejs)
  - [Node.js의 작동 방식 및 이점](#nodejs란)
- [NVM](#nvm)
  - [NVM 자주 쓰는 명령어](#nvm-자주-쓰는-명령어)
- [NPM](#npm)
  - [NPM 자주 쓰는 명령어](#npm-자주-쓰는-명령어)
  - [package.json](#packagejson)
  - [package-lock.json](#package-lockjson)
- [시맨틱 버전 관리 방식](#시맨틱-버전-관리-방식)
  - [표기법](#표기법)




<br />
<br />




## Node.js

`Node.js`는 웹 브라우저 **외부에서도** 자바스크립트 코드를 실행할 수 있도록 해주는 **자바스크립트 실행 환경**이다.

원래 자바스크립트는 웹 브라우저 안에서만 실행되도록 만들어 졌고 각 브라우저는 이를 해석하기 위해 자바스크립트 엔진을 가지고 있다. 구글은 `V8 엔진`이라는 빠른 자바스크립트 엔진을 개발해 크롬 브라우저에 적용했다. 이후 이 엔진을 기반으로 브라우저 외부에서도 자바스크립트를 실행할 수 있는 **Node.js가 등장**했다.

<br />

### Node.js의 작동 방식 및 이점

Node.js는 **싱글 스레드**로 동작 한다. 쉽게 말해, **한 명의 일꾼**이 있다고 생각하면 된다. 예를 들어 종업원(일꾼)이 주문을 받으면 직접 음식을 만들어내는 것이 아니라, 요리(**I/O 작업**)가 필요한 부분은 주방(**백그라운드**)에 맡겨 두고 곧바로 다음 손님의 주문을 받는다. 그리고 요리가 다 만들어지면 주방에서 일꾼에게 알려주고, 일꾼은 그제서야 손님에게 요리를 전달하게 된다.

이 방식 덕분에 일꾼은 혼자서도 수많은 손님의 주문을 빠르게 받을 수 있고, 한 명씩 기다리게 만드는 일이 줄어든다.

이러한 Node.js의 **비동기 논블로킹 I/O**와 **이벤트 루프**가 만들어내는 효율적인 처리 방식으로 처리 속도가 빨라 작업 시간이 짧으며 요청이 많이 들어오는 채팅 서비스나 실시간으로 데이터를 보여주는 차트를 활용한 프로젝트 등을 개발할 경우 Node.js를 사용하는 것이 좋다.

> **I/O 작업**
>
> > 파일 읽기/쓰기, 네트워크 요청(HTTP, API 호출 등)처럼 외부와 데이터를 주고 받는 일
>
> **백그라운드**
>
> > 운영체제, 데이터베이스 서버 등 I/O 작업을 처리하는 영역
>
> **비동기 논블로킹**
>
> > 작업이 끝날 때 까지 기다리지 않고 다른 일을 먼저 처리하는 방식
>
> **이벤트 루프**
>
> > 작업을 순서대로 처리하고 오래걸리는 작업은 백그라운드에 맡겼다가 끝나면 다시 메인 스레드에서 처리하는 방식

이러한 장점 때문에 전세계적으로 대형 IT 기업부터 스타트업까지 다양한 기업에서 Node.js를 활용하고 있다. [Node.js 사용 기업](https://www.codenary.co.kr/techstack/detail/nodejs)




<br />
<br />




## NVM

**Node Version Manager**의 약자로 **Node.js의 버전을 관리하는 도구**이다. 하나의 컴퓨터 안에서 여러 버전의 Node.js를 설치하고 자유롭게 전환할 수 있게 도와준다. 프로젝트마다 요구하는 버전이 다를때 마다 프로젝트에 맞는 **버전을 자유롭게 전환**할 수 있어 유용하다.

Node.js를 직접 깔지 말고 nvm을 먼저 설치한 뒤 nvm을 통해 원하는 Node.js 버전을 설치하는 방법이 좋다. GitHub에 정리된 [nvm 문서](https://github.com/nvm-sh/nvm)를 참고해서 **운영체제에 맞게 다운로드** 받을 수 있다.

<br />

### NVM 자주 쓰는 명령어

```bash
# 최신 LTS(Long Term Support) 버전 설치
nvm install lts

# 현재 설치된 버전 목록 확인
nvm ls

# 설치 가능한 Node.js 버전 목록 확인
npm ls-remote

# LTS의 버전 목록만 확인
npm ls-remote --lts

# 특정 버전 설치
nvm install <version>

# 특정 버전 제거
nvm uninstall <version>

# 특정 버전 사용
nvm use <version>

# 현재 사용 중인 버전 확인
node -v

# 기본으로 쓸 버전 지정
nvm alias default <version>

# 설치되어 있는 가장 최신 버전의 node를 기본으로 지정
nvm alias default node
```




<br />
<br />




## NPM

**Node Package Manager**의 약자로 Node.js 환경에서 **패키지를 설치하고 관리하는 도구**이다. 프로젝트 개발 시 필요한 다양한 패키지를 설치하고 관리할 수 있도록 도와준다. 다른 개발자들이 만든 패키지를 내 프로젝트에 쉽게 추가하고 의존성 관리를 간편하게 할 수 있다. 또한 자신이 만든 패키지를 다른 사람들과 공유하고 배포할 수도 있다.

NPM은 Node.js를 설치하면 함께 설치된다.

> 의존성이란
>
> > 설치한 패키지를 사용하기 위해 우리 프로젝트가 의존한다는 것을 의미한다.

<br />

### NPM 자주 쓰는 명령어

```bash
# 프로젝트 초기화
npm init # package.json 생성 (프로젝트 기본 정보 등록)
npm init -y # 질문을 건너뛰고 기본값으로 바로 생성

# 버전 확인
npm --version

# 현재 npm 환경설정 확인
npm config list

# 패키지 설치
npm install <패키지명> # 의존성 패키지 설치 (package.json에 추가됨)
npm install <패키지명>@<버전> # 특정 버전 설치
npm install -D <패키지명> # 개발 의존성으로 설치
npm install # package.json에 기록된 패키지를 전부 설치 (보통 클론 프로젝트 시작할 때 실행)

# 패키지 삭제
npm uninstall <패키지명>

# 패키지 업데이트
npm update <패키지명>

# 현재 설치된 패키지와 최신 버전 비교
npm outdated

# scripts에 정의한 명령 실행
npm run <스크립트명> # npm run dev, npm run build
npm start # npm run start는 run 생략 가능

# 설치된 패키지 목록 확인
npm ls # 내가 설치한 패키치와 그 안의 의존성 패키지까지 전부 확인
npm list --depth=0 # 내가 직접 설치한 패키지만 확인

# npm 캐시 삭제
npm cache claen --force # 패키지 설치 꼬일 때 사용

# 보안 취약점 검사
npm audit
npm audit fix # 발견된 보안 취약점 자동 수정 시도
```

<br />

### package.json

`package.json` 파일은 프로젝트의 **메타데이터**, **의존성 정보**, **스크립트 명령어** 등을 담고 있는 JSON 파일이다. `package.json` 파일은 프로젝트의 루트 디렉토리에 위치하며, `npm init` 명령어를 통해 초기화하거나 수동으로 작성할 수 있다. npm 명령어를 사용하여 패키지를 설치하면 자동으로 `package.json` 파일에 의존성 정보가 업데이트된다.

<br />

#### 프로젝트 정보

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "나의 첫 번째 Node.js 프로젝트",
  "main": "index.js"
}
```

- `"name"` : 프로젝트 이름
- `"version"` : 프로젝트 버전
- `"description"` : 프로젝트 설명
- `"main"` : 진입 파일

<br />

#### 스크립트 명령어

프로젝트에서 사용되는 스크립트들을 정의할 수 있다.

```json
{
  "scripts": {
    "start": "node index.js",
    "dev": "live-server",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
}
```

- `npm run <스크립트명>`으로 실행 가능
  - `npm run dev` → live-server 실행
- `npm start`는 특별히 run을 생략 가능
  - `npm start` → node index.js 실행

<br />

#### dependencies (의존성 정보)

실제 서비스 실행에 필요한 패키지 정보이다.

```json
{
  "dependencies": {
    "express": "^4.19.2"
  }
}
```

- 예 : `express`, `react`, `axios` 등

<br />

#### devDependencies (의존성 정보)

개발할 때만 필요한 패키지 정보이다. 빌드 도구, 테스트 도구 등을 포함하며 실제 배포 시에는 포함되지 않는다.

```json
{
  "devDependencies": {
    "eslint": "^9.12.0"
  }
}
```

<br />

#### 기타 정보

```json
{
  "keywords": ["node", "npm", "example"],
  "author": "홍길동",
  "license": "MIT"
}
```

- `"keywords"` : 검색에 도움되는 키워드 배열
- `"author"` : 작성자 정보
- `"license"` : 라이센스 정보

<br />

### package-lock.json

`package.json`과 함께 자동 생성되는 파일이다. **정확한 버전 정보**와 **의존성 트리(누가 어떤 버전을 쓰는지)를** 기록(스냅샷)해둔다. 팀원들이 `npm install` 했을 때 똑같은 버전의 패키지를 설치할 수 있다.

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "lockfileVersion": 3,
  "requires": true,
  "packages": {
    "": {
      "name": "my-project",
      "version": "1.0.0",
      "dependencies": {
        "express": "^4.19.2"
      }
    },
    "node_modules/express": {
      "version": "4.19.2",
      "resolved": "https://registry.npmjs.org/express/-/express-4.19.2.tgz",
      "integrity": "sha512-abc123xyz...",
      "dependencies": {
        "accepts": "~1.3.8",
        "body-parser": "1.20.2"
      }
    },
    "node_modules/accepts": {
      "version": "1.3.8",
      "resolved": "https://registry.npmjs.org/accepts/-/accepts-1.3.8.tgz",
      "integrity": "sha512-def456uvw...",
      "dependencies": {
        "mime-types": "~2.1.34"
      }
    }
  }
}
```

쉽게 말해, `package.json`은 "무엇이 필요하다"를 기록하고, `package-lock.json`은 "정확히 어떤 버전을 쓰고 있다"를 기록한다고 생각하면 이해하기 쉽다.

- `package.json` → "나는 express가 필요해"
- `package-lock.json` → "지금 설치한 express는 4.19.2고, 그 안에 accepts 1.3.8도 같이 깔려 있어"

<br />

`package.json`과 `package-lock.json`에 기록이 남아야 나중에 다른 사람이 이 프로젝트를 클론이나 다운로드했을 때 `npm install`만 실행하면 같은 패키지를 똑같이 설치할 수 있다.




<br />
<br />




## 시맨틱 버전 관리 방식

버전 정보는 **메이저 버전 번호**, **마이너 버전 번호**, **패치 버전 번호**로 구성된다.

`Major.minor.patch` = `1.0.7`

- `Major` : **하위 버전과 호환되지 않는** 수정 사항이 생겼을 때 올린다.
- `minor` : **하위 버전과 호환되는** 수정 사항이 생겼을 때 올린다.
- `patch` : **기능에 버그를 해결**했을 때 올린다.

<br />

### 표기법

|  표기법    | 설명                              |
| :-------: | :-------------------------------- |
| >version  | 명시된 version보다 높은 버전      |
| >=version | 명시된 version과 같거나 높은 버전 |
| <version  | 명시된 version보다 낮은 버전      |
| <=version | 명시된 version과 같거나 낮은 버전 |
| ~version  | 명시된 version과 근사한 버전      |
| ^version  | 명시된 version과 호환되는 버전    |
|  @latest  | 최신 버전을 설치하라는 의미       |
|   @next   | 실험적인 버전                     |

<br />

#### ~(틸트)와 ^(캐럿)의 차이

~(틸트)는 `패치` **버전 범위 내**에서 업데이트한다.

- ~0.2.1 → 0.2.`1` <= version < 0.3.`0`
  - 0.2.`1`, 0.2.`2`, 0.2.`3`, ... , 0.2.`9`

^(캐럿)은 `마이너` **버전 범위 내**에서 업데이트한다.

- 패치 버전 업데이트도 포함
- ^2.2.1 → 2.`2`.1 <= version < 3.`0`.0
  - 2.`2`.1, 2.`3`.1, 2.`4`.1, ... , 2.`9`.9