








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
즉시실행함수 `()();`도 같은 원리

`<script async src="./script2.js"></script>`
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