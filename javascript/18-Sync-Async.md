# 동기(Sync)와 비동기(Async)




<br />
<br />




## script 태그의 속성 async, defer

### 기본

```html
<script src="script.js"></script>
```

![parsing-default](../src/images/parsing-default.png)

**1.** HTML을 순차적으로 파싱하다가 스크립트 파일을 만나면 파싱을 중지한다.

**2.** 파싱을 중지하고 스크립트 파일을 다운로드 받는다. (동기 방식)

**3.** 다운로드가 끝나면 스크립트를 실행하고 완료되면 HTML 파싱을 재개한다.

스크립트를 다운로드받고 실행하는 시간동안 페이지 렌더링은 지연이 발생할 수 있다.

<br />

### async

```html
<script async src="script.js"></script>
```

![parsing-default](../src/images/parsing-async.png)

**1.** HTML 파싱과 스크립트 파일 다운로드를 병행한다. (비동기 방식)

**2.** 다운로드가 완료되면 파싱을 멈추고 스크립트를 실행한다.

**3.** 스크립트 실행이 완료되면 HTML 파싱을 재개한다.

여러 `async` 스크립트가 있을 때, 작성 순서와 상관없이 먼저 다운로드 완료된 것부터 실행한다. 그래서 실행 순서가 보장되지 않는다. 주로 HTML 구조나 다른 스크립트에 의존하지 않고, 혼자서 실행돼도 문제 없는 스크립트에 사용한다.

<br />

### defer

```html
<script defer src="script.js"></script>
```

![parsing-default](../src/images/parsing-defer.png)

**1.** HTML 파싱과 스크립트 파일 다운로드를 병행한다. (비동기 방식)

**2.** 다운로드가 완료되어도 파싱이 완료될 때까지 기다렸다가 실행한다.

여러 `defer` 스크립트가 있을 때, HTML에서 선언된 순서대로 실행한다. 그래서 실행 순서가 보장된다. 보통 DOM 조작 코드에 사용된다. 즉, 렌더링이 우선시 되는 경우에 주로 사용한다. 

그리고 `type="module"` 속성이 있으면 기본이 `defer` 속성으로 동작한다.

```html
<script type="module" src="script.js"></script>
```




<br />
<br />




## 일반 함수 (동기 방식)




<br />
<br />




## 비동기 함수


























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

프라미스 순차적으로 실행
함수 호출했다가 성공하면 콜백함수 실행..
순차적으로 실행하지 않는다면 all 메서드 - 전체가 성공하면 콜백함수 실행..
익스큐트 함수 = 프로미스의 콜백함수

async/await 방식 - 동기 함수 다루듯이 사용 가능

test() 함수는 비동기 함수

try...catch 문은 동기 방식

```
async function test(){
  try {
    const result1 = await p1();
    console.log('p1의 작업 결과.', result1);
    const result2 = await a1();
    console.log('a1의 작업 결과.', result2);
    const result3 = await p2();
    console.log('p2의 작업 결과.', result3);
    const result4 = await a2();
    console.log('a2의 작업 결과.', result4);
  } catch(error) {
    console.log('에러 발생.', error);
  }
}
```




즉시실행함수 `()();`도 같은 원리

`<script async src="./script2.js"></>`
파싱에 따라서 실행되는 순서가 달라진다.
async는 html 파싱이랑 동시에 파싱이 된다.
만약에 body 컨텐츠가 많으면 돔을 불러오기전에 실행되어 에러가 날 확률이 올라가고,
컨텐츠가 적으면 돔을 빠르게 불러와 에러가 나지않을 확률이 올라간다.


비동기 방식 두가지 방법

콜백함수를 전달해서.

프로미스를 사용해서 리턴받을 수 있는


```javascript
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title></title>
  </head>
  <body>
    <div class="container"></div>
  </body>

  <script>
    const productList = [
      { id: 1, name: "상의", price: 10000 },
      { id: 2, name: "자켓", price: 15000 },
      { id: 3, name: "청바지", price: 15000 },
      { id: 4, name: "반바지", price: 20000 },
      { id: 5, name: "모자", price: 25000 },
      { id: 6, name: "신발", price: 20000 },
      { id: 7, name: "가방", price: 20000 },
      { id: 8, name: "팔찌", price: 20000 },
      { id: 9, name: "핸드폰", price: 20000 },
    ];

    const productListTags = productList
      .map(
        (item) => `
  <div>
    <p>상품 번호 : ${item.id}</p>
    <p>상품 명 : ${item.name}</p>
    <p>상품 가격 : ${item.price.toLocaleString()}원</p>
  <hr/>
  </div>
`
      )
      .join("");

    const container = document.querySelector(".container");

    container.innerHTML = `${productListTags}`;
  </script>
</html>
```

```typescript
new Promise<T>(
  executor: (
    resolve: (value: T) => void,
    reject: (reason?: any) => void
  ) => void
)
```

executor 함수는 resolve, reject의 매개변수를 받는데, resolve, reject의 매개변수도 인자로 함수를 전달받는다.

then은 프로미스를 리턴한다. 그래서 자기 자신을 리턴한다. .then().then()... 가능

비동기 함수를 동기함수 처럼 결과를 받고싶으면 await를 사용
- 동작은 비동기로 동작..

f1()호출하면 Promise를 반환받는데 await를 붙이면 프로미스가 resolve가 될때까지.. 동기적으로.. 실행을 마친뒤 리턴하는 값을 받는다..?