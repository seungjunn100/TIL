# HTTP ( HyperText Transfer Protocol )

- [HTTP 프로토콜]()
- [동작 방식]()
- [Request 메시지 구조]()
- [Response 메시지 구조]()
- [장점]()
- [참고]()
- [HTTP의 특징]()
- [HTTP 주요 메서드]()




<br />
<br />




## HTTP 프로토콜

`HTTP(HyperText Transfer Protocol)`는 웹 브라우저(클라이언트)와 웹 서버 간에 데이터를 주고받기 위한 텍스트 기반의 `프로토콜(통신 규약)`이다.

신뢰성이 높은 전송 계층인 TCP 기반으로 동작하며, 클라이언트와 서버는 먼저 TCP 연결을 수립한 뒤 에 메시지를 주고 받는다.

메시지는 여러 개의 패킷으로 나뉘어 전송되며, 수신 측은 이를 순서대로 재조합한다. 만약 패킷이 누락되면 재전송을 요청하기 때문에 손실 없는 통신이 가능하다.

HTTP는 요청과 응답이 완료되면 기본적으로 연결이 종료된다. 즉, 일회성 통신을 하며, 서버는 이전 요청의 상태를 기억하지 못한다. 그래서 필요한 정보를 보낼 때 한번에 같이 보내야 한다.

<br />

### 동작 방식

#### 요청(`Request`)

클라이언트(주로 브라우저)는 서버에 요청 메시지를 보낸다. 

요청에는 `필요한 자원(URL)`이나 `작업(GET, POST 등 요청 메서드)`이 포함된다.

#### 응답(`Response`)

서버는 요청 내용을 분석하여 `필요한 작업(파일 읽기, 데이터베이스 조회, 외부 시스템 연동 등)`을 수행한다.

작업 결과를 바탕으로 응답 메시지를 클라이언트에 전송한다.

#### 렌더링(`Rendering`)

클라이언트는 응답 데이터를 파싱하여 화면에 출력한다.

`HTTP/1.x`의 경우 기본적으로 비연결형(Connectionless) 통신을 하므로, 서버의 응답을 받은 후 클라이언트와 서버의 연결은 종료된다.




<br />
<br />




### `Request` 메시지 구조

```
GET /ch09/ex09-01.html HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: ko,en-US;q=0.9,en;q=0.8
Cache-Control: no-cache
Connection: keep-alive
Host: 127.0.0.1:8080
if-modified-since: Sun, 26 Oct 2025 09:13:15
If-None-Match: W/"191-19a1fcb18fe"
Referer: http://127.0.0.1:8080/ch09/ex09-01.html
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/141.0.0.0 Safari/537.36
...
```

<br />

### 요청 라인(Request Line)

```
GET /todolist HTTP/1.1
POST /todolist HTTP/1.1
```

<br />

### 요청 헤더 (Request Headers)

<br />

### 요청 바디 (Request Body)




<br />
<br />




### `Response` 메시지 구조









<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />


사이트 주소 = ip 주소 = 도메인 주소(naver.com)

안정성이 높은, 신뢰성이 중요한 통신에는 TCP 기반 프로토콜을 사용
게임은 거의 TCP 기반
데이터를 주고받을 때 수시로 확인

HTTP는 일회성 통신을 함, 이전 상태를 기억하지 못함, 이전 메모리를 버림
그래서 필요한 정보를 보낼 때 한번에 같이 보내야 한다.

q=0.9 선호도, 우선순위

Referer 유입 경로 확인

Content-Type: application/json - 보내는 형태

Response - 응답 바디

Response 메시지 구조
pc에서 스마트폰 모드에서 네이버를 접속했을 때 리디렉션

Accept-Ranges: bytes
클라이언트가 Range: bytes=1000-1999 형식으로 바이트 단위의 범위 요청 가능
스크롤시 부분적으로 렌더링할 수 있다?

api 프론트와 백엔드의 연결고리
api는 백엔드가 만든다.

API를 사용할땐
URL, Method를 확인 잘하기

"ok": 1, - 성공
"ok": 0, - 실패

포스트맨을 왜 사용하는걸까
포스트맨은 통신하는걸 UI적으로 확인하기 편하게 해준다.
백엔드가 만든 API를 통해 서버 통신을 하는 방법을 보기위해..?

Ajax
a 앵커태그를 이용해 페이지를 옮길 때 기사의 내용만 바뀌고 나머지 부분은 바뀌지가 않을땐 내용만 바꾸는게 효율적이다.. 그게 아니라면 페이지를 옮길 때 매번 똑같은 부분도 다시 다운로드 받고하면 요청도 많고 서버용량?도 많이 사용하게 된다.
- 페이지 이동이나 새로고침 없이 서버에 요청을 보내고 DOM API를 이용해 화면을 갱신

open 메서드 async false - send(data)는 동기가 됨
async true - send(data)는 비동기가 됨

response.ok - 200번대

XMLHttpRequest는 Promise 나오기 전에 나와 비동기는 콜백방식으로 사용해야함

xhr.open('get', url, false); // 네트워크에서 쓰로틀링을 활용해 비교해보자
동기방식은 이미지 요청을 누르고 나서 다른 작업을 하려고 이벤트를 실행하면 이미지를 요청받아서 이미지를 로드하는 실행이 끝난 뒤에 다음 이벤트가 진행이된다.
xhr.open('get', url, true); // 네트워크에서 쓰로틀링을 활용해 비교해보자
비동기 방식은 이미지 요청을 누르고 나서 다음 이벤트를 예약해놓을 수 있다.

axios
시간을 설정할 수 있다.
npm init -y
npm i axios
"moduleResolution": "bundler", // import시 모듈 해석 방식 지정 (node_modules 폴더에서 검색)

투두리스트 타입ts - 투두리스트 API 비교해보면서 확인

인터셉터 - 가공
ok 1, 0 => true, false