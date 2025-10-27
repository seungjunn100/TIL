# DOM ( Document Object Model )

- [DOM](#dom)
- [요소 노드 접근](#요소-노드-접근)
  - [id 속성을 이용한 접근](#id-속성을-이용한-접근)
  - [class 속성을 이용한 접근](#class-속성을-이용한-접근)
  - [태그 이름을 이용한 접근](#태그-이름을-이용한-접근)
  - [CSS 선택자를 이용한 접근](#css-선택자를-이용한-접근)
- [노드 탐색 접근](#노드-탐색-접근)
  - [공백 텍스트 노드](#공백-텍스트-노드)
  - [자식 노드 탐색 접근](#자식-노드-탐색-접근)
  - [부모 노드 탐색 접근](#부모-노드-탐색-접근)
  - [형제 노드 탐색 접근](#형제-노드-탐색-접근)
- [요소 노드 내부 컨텐츠 제어](#요소-노드-내부-컨텐츠-제어)
  - [nodeValue](#nodevalue)
  - [textContent](#textcontent)
  - [innerText](#innertext)
  - [innerHTML](#innerhtml)
  - [outerHTML](#outerhtml)
  - [insertAdjacentHTML(position, string)](#insertadjacenthtmlposition-string)
- [DOM 제어](#dom-제어)
  - [노드 생성](#노드-생성)
  - [노드 추가, 삽입, 이동](#노드-추가-삽입-이동)
  - [노드 교체](#노드-교체)
  - [노드 삭제](#노드-삭제)
  - [노드 복사](#노드-복사)
- [속성(Attribute) 제어](#속성attribute-제어)
- [스타일(Style) 제어](#스타일style-제어)
  - [인라인 스타일 제어](#인라인-스타일-제어)
  - [클래스(class) 제어](#클래스class-제어)
  - [모든 CSS 스타일 확인](#모든-css-스타일-확인)




<br />
<br />
<br />
<br />
<br />




## DOM

브라우저의 렌더링 엔진은 HTML 문서를 로드한 후 파싱하여 브라우저가 이해할 수 있는 구조로 구성하여 메모리에 적재하는데 이를 `DOM(Document Object Model)`이라 한다. 여기서 구성된 구조는 모든 요소와 요소의 속성, 컨텐츠를 각각의 **객체로 만들어 부자 관계를 표현할 수 있는 구조**로 `DOM Tree`라고 한다.

이 `DOM`은 자바스크립트를 통해 동적으로 제어할 수 있는데, 일반적으로 프로퍼티와 메서드를 갖는 자바스크립트 객체로 제공된다. 이를 `DOM API`라고 부른다. 즉, `DOM API`는 `DOM`에 접근하고 변경할 수 있는 프로퍼티와 메서드의 집합이다.

#### HTML 문서
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <style>
    .red  { color: #ff0000; }
    .blue { color: #0000ff; }
  </style>
</head>
<body>
  <div>
    <h1>Cities</h1>
    <ul>
      <li id="one" class="red">Seoul</li>
      <li id="two" class="red">London</li>
      <li id="three" class="red">Newyork</li>
      <li id="four">Tokyo</li>
    </ul>
  </div>
</body>
</html>
```

#### DOM Tree
![DOM Tree](../../src/images/dom-tree.png)

위 사진(PoiemaWeb | DOM 참조)에서 보듯이 `DOM Tree`는 각각의 노드(객체)로 구성된다. 노드의 종류는 12가지 정도가 있는데, 이 중에서 대표적을 4가지 종류로 구성된다.

- 문서노드(document node) : 문서 전체를 대표하는 최상위 노드
- 요소노드(element node) : HTML 태그
- 속성노드(attribute node) : 태그의 속성
- 텍스트노드(text node) : 태그 내의 텍스트를 표현하는 최종 노드




<br />
<br />
<br />
<br />




## 요소 노드 접근

HTML의 구조나 내용 또는 스타일 등을 자바스크립트를 통해 동적으로 제어하려면 먼저 요소 노드에 접근해야한다. 접근 방법에는 여러가지 방법이 있다. 그리고 요소 노드에 접근할 땐 문서 전체에서 접근할 수 있고, 지정한 요소 노드를 통해서 접근할 수도 있다.

<br />

### id 속성을 이용한 접근

HTML에서 해당 `id 속성 값을 가진 요소 노드`를 찾아서 **반환**한다. 여러개가 선택된 경우, 첫번째 요소만 반환한다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>쇼핑목록</title>
</head>
<body>
  <h1>쇼핑 목록</h1>
  <p>마트에서 사야할 목록</p>
  <ul id="buy-list" class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
</body>
</html>
```

```javascript
const buyList = document.getElementById('buy-list');
console.log(buyList);
/*
  <ul id="buy-list" class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
*/
```

<br />

### class 속성을 이용한 접근

HTML에서 해당 `class 속성 값을 가진 모든 요소 노드`를 찾아서 유사 배열 객체(HTMLCollection) 형태로 **반환**한다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>쇼핑목록</title>
</head>
<body>
  <h1>쇼핑 목록</h1>
  <p>마트에서 사야할 목록</p>
  <ul class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
  <ul class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
  <ul class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
</body>
</html>
```

```javascript
// <ul class="list"> 요소 노드가 하나만 있을 경우
const list = document.getElementsByClassName('list');
console.log(list); // HTMLCollection [ul.list]

// <ul class="list"> 요소 노드가 여러개가 있을 경우
const list = document.getElementsByClassName('list');
console.log(list); // HTMLCollection(3) [ul.list, ul.list, ul.list]

// 여러개가 있을 경우 인덱스로 요소 노드를 선택할 수 있다.
const list = document.getElementsByClassName('list')[0];
console.log(list);
/*
  <ul class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
*/
```

<br />

### 태그 이름을 이용한 접근

문서 전체 또는 지정한 요소 노드에서 `태그명에 해당하는 하위 모든 요소 노드`를 유사 배열 객체(HTMLCollection) 형태로 **반환**한다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>쇼핑목록</title>
</head>
<body>
  <h1>쇼핑 목록</h1>
  <p>마트에서 사야할 목록</p>
  <ul id="buy-list" class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
  </ul>
</body>
</html>
```

```javascript
// 문서 전체
const liList = document.getElementsByTagName('li');
console.log(liList); // HTMLCollection(7) [li, li, li, li, li, li, li]

// 지정한 요소 노드
const buyList = document.getElementById('buy-list');
const liList = buyList.getElementsByTagName('li'); // HTMLCollection(3) [li, li, li]
```

<br />

### CSS 선택자를 이용한 접근

#### document.querySelector(selector)

`CSS에서 사용하는 노드 선택 구문인 셀렉터를 사용하여 지정한 셀렉터에 해당하는 요소 노드`를 찾아서 **반환**한다. 여러개가 선택된 경우, 첫번째 요소만 반환한다.

#### document.querySelectorAll(selector)

`지정한 셀렉터의 요소 노드`를 찾아서 유사 배열 객체(NodeList) 형태로 **반환**한다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>쇼핑목록</title>
</head>
<body>
  <h1>쇼핑 목록</h1>
  <p>마트에서 사야할 목록</p>
  <ul class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
  <ul id="buy-list" class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
</body>
</html>
```

```javascript
const buyList = document.querySelector('#buy-list');
console.log(buyList);
/*
  <ul id="buy-list" class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
*/

// 여러개가 선택된 경우, 첫번째 요소만 반환한다.
const buyList = document.querySelector('.list');
console.log(buyList);
/*
  <ul class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
*/

// 여러개가 선택된 경우, 첫번째 요소만 반환한다.
const liList = document.querySelector('li');
console.log(liList);
/*
  <li>두부</li>
*/

// 다양한 셀렉터 사용 가능
const liList = document.querySelector('#buy-list > li:nth-child(2)');
console.log(liList);
/*
  <li>계란</li>
*/


// querySelectorAll
const buyList = document.querySelectorAll('#buy-list');
console.log(buyList); // NodeList [ul#buy-list.list]

const buyList = document.querySelectorAll('.list');
console.log(buyList); // NodeList(2) [ul.list, ul#buy-list.list]

// 여러개가 있을 경우 인덱스로 요소 노드를 선택할 수 있다.
const buyList = document.querySelectorAll('.list')[0];
console.log(buyList);
/*
  <ul class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
*/

const liList = document.querySelectorAll('li');
console.log(liList); // NodeList(9) [li, li, li, li, li, li, li, li, li]

// 여러개가 있을 경우 인덱스로 요소 노드를 선택할 수 있다.
const liList = document.querySelectorAll('li')[0];
console.log(liList);
/*
  <li>두부</li>
*/

// 지정한 요소 노드
const buyList = document.querySelector('#buy-list');
const buyliList = buyList.querySelectorAll('li');
console.log(buyliList); // NodeList(3) [li, li, li]
```




<br />
<br />




## 노드 탐색 접근

요소 노드에 접근한 다음 해당 요소 노드를 기점으로 `DOM tree`의 노드를 옮겨 다니며 부모, 형제, 자식 노드 등을 탐색하여 접근할 수 있다.

<br />

### 공백 텍스트 노드

HTML 마크업을 할 때 요소 사이의 스페이스, 탭, 줄바꿈(개행) 등의 공백 문자는 공백 텍스트 노드를 생성한다. 노드를 탐색할 때 공백 텍스트 노드를 탐색하는 걸 주의해야 한다.

```html
<ul id="buy-list" class="list">
  <li>두부</li>
  <li>계란</li>
  <li>라면</li>
</ul>
```

`<ul id="buy-list" class="list">` 태그 다음에 `<li>두부</li>` 요소 노드가 아니라, 엔터와 탭을 이용해 생긴 공백에 대한 `공백 텍스트 노드`가 생성된다.

<br />

### 자식 노드 탐색 접근

```html
<ul id="buy-list" class="list">
  <li>두부</li>
  <li>계란</li>
  <li>라면</li>
</ul>
```

```javascript
// #buy-list
const buyList = document.getElementById('buy-list');
```

#### childNodes

`텍스트 노드를 포함한 모든 자식 노드`를 탐색하여 유사 배열 객체(NodeList) 형태로 **반환**한다.

```javascript
console.log(buyList.childNodes);
// NodeList(7) [text, li, text, li, text, li, text]
// 여기서 text의 값은 "\n    " 줄바꿈과 스페이스의 공백 문자를 포함하는 텍스트 노드이다.
```

#### children

`자식 요소 중에서 Element type 요소 노드`만 탐색하여 유사 배열 객체(HTMLCollection) 형태로 **반환**한다.

```javascript
console.log(buyList.children); // HTMLCollection(3) [li, li, li]
```

#### firstChild, lastChild

텍스트 노드를 포함한 모든 자식 요소 노드 중 `첫번째 자식 노드 또는 마지막 자식 노드`를 **탐색하여 반환**한다.

```javascript
console.log(buyList.firstChild); // #text, "\n    " 공백 텍스트 노드를 반환한다.

console.log(buyList.lastChild); // #text, "\n  " 공백 텍스트 노드를 반환한다.
```

#### firstElementChild, lastElementChild

자식 요소 중 `Element type 요소 노드`에서 `첫번째 자식 요소 노드 또는 마지막 자식 요소 노드`를 **탐색하여 반환**한다.

```javascript
console.log(buyList.firstElementChild); // <li>두부</li>

console.log(buyList.lastElementChild); // <li>라면</li>
```

#### 자식 요소 노드 존재 확인

```javascript
// hasChildNodes(), 텍스트 노드를 포함하여 자식 요소 노드의 존재 확인
console.log(buyList.hasChildNodes()); // true

// childElementCount, 텍스트 노드를 포함하지 않고 자식 요소 노드의 존재 확인
console.log(buyList.childElementCount); // 3

// children.length, 텍스트 노드를 포함하지 않고 자식 요소 노드의 존재 확인
console.log(buyList.children.length); // 3
```

<br />

### 부모 노드 탐색 접근

```html
<ul id="buy-list" class="list">
  <li>두부</li>
  <li>계란</li>
  <li>라면</li>
</ul>
```

```javascript
// #buy-list
const buyList = document.getElementById('buy-list');

// <li>두부</li>
const firstLi = buyList.firstElementChild;
```

#### parentNode

모든 부모 노드를 탐색할 수 있으며, `부모 노드`를 **탐색하여 반환**한다. `<html>`의 부모인 `#document`(문서 전체)도 반환한다.

```javascript
console.log(firstLi.parentNode);
/*
  <ul id="buy-list" class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
*/
```

#### parentElement

부모가 요소인 경우에만 탐색할 수 있으며, `부모 요소 노드`만 **탐색하여 반환**한다.

```javascript
console.log(firstLi.parentElement);
/*
  <ul id="buy-list" class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면</li>
  </ul>
*/
```

<br />

### 형제 노드 탐색 접근

```html
<ul id="buy-list" class="list">
  <li>두부</li>
  <li>계란</li>
  <li>라면</li>
</ul>
```

```javascript
// #buy-list
const buyList = document.getElementById('buy-list');

// <li>두부</li>
const firstLi = buyList.firstElementChild;
```

#### previousSibling

부모 노드가 같은 **텍스트 노드를 포함한 형제 노드 중에서** 자신의 `이전 형제 노드`를 **탐색하여 반환**한다.

```javascript
console.log(firstLi.previousSibling); // #text, "\n    " 공백 텍스트 노드를 반환한다.
```

#### nextSibling

부모 노드가 같은 **텍스트 노드를 포함한 형제 노드 중에서** 자신의 `다음 형제 노드`를 **탐색하여 반환**한다.

```javascript
console.log(firstLi.nextSibling); // #text, "\n    " 공백 텍스트 노드를 반환한다.
```

#### previousElementSibling

부모 노드가 같은 **형제 요소 노드 중에서** 자신의 `이전 형제 노드`를 **탐색하여 반환**한다.

```javascript
console.log(firstLi.previousElementSibling); // null, 앞에 형제 요소 노드가 없다.
```

#### nextElementSibling

부모 노드가 같은 **형제 요소 노드 중에서** 자신의 `다음 형제 노드`를 **탐색하여 반환**한다.

```javascript
console.log(firstLi.nextElementSibling); // <li>계란</li>
```




<br />
<br />




## 요소 노드 내부 컨텐츠 제어

```html
<ul id="buy-list" class="list">
  <li>두부</li>
  <li>계란</li>
  <li>라면 <span hidden>안성탕면</span></li>
  <!-- <span hidden> 요소는 브라우저상에서 보이지 않는다. -->
</ul>
```

<br />

### nodeValue

요소의 텍스트는 텍스트 노드에 저장되어 있다. 이 텍스트에 접근하기 위해서는 다음과 같은 수순이 필요하다.

```javascript
// 요소 노드를 선택한다.
const liElem = document.querySelectorAll('#buy-list > li')[1];
console.log(liElem); // <li>계란</li>

// 텍스트 노드를 선택한다.
const liElemTextNode = liElem.firstChild;
console.log(liElemTextNode); // "계란"

// 텍스트 노드의 값에 접근할 수 있다.
console.log(liElemTextNode.nodeValue); // 계란

// 텍스트 내용 수정도 가능하다.
liElemTextNode.nodeValue = '새우';
console.log(liElem); // <li>새우</li>
console.log(liElemTextNode.nodeValue); // 새우
```

<br />

### textContent

요소의 텍스트 노드의 값에 접근하거나 수정할 수 있다.

```javascript
// 요소 노드를 선택
const liElem = document.querySelectorAll('#buy-list > li')[2];
console.log(liElem); // <li>라면 <span hidden>안성탕면</span></li>

// 텍스트 노드의 값에 접근
console.log(liElem.textContent); // 라면 안성탕면

// 텍스트 내용 수정
liElem.textContent = '국수';
console.log(liElem); // <li>국수</li>
console.log(liElem.textContent); // 국수
```

<br />

### innerText

요소의 텍스트 노드의 값에 접근하거나 수정할 수 있다. 하지만, `hidden` 속성을 가진 요소는 조회하지 않는다. 이러한 이유로 잘 사용되지 않는다.

```javascript
// 요소 노드를 선택
const liElem = document.querySelectorAll('#buy-list > li')[2];
console.log(liElem); // <li>라면 <span hidden>안성탕면</span></li>

// 텍스트 노드의 값에 접근
console.log(liElem.innerText); // 라면

// 텍스트 내용 수정
liElem.innerText = '국수';
console.log(liElem); // <li>국수</li>
console.log(liElem.innerText); // 국수
```

<br />

### innerHTML

해당 요소의 모든 자식 요소를 포함하는 모든 컨텐츠에 접근하거나 수정할 수 있다. `요소 자신은 제외`한다.

```javascript
// 요소 노드를 선택
const buyList = document.querySelector('#buy-list');
console.log(buyList);
/*
  <ul id="buy-list" class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면 <span hidden>안성탕면</span></li>
  </ul>
*/

// 공백 텍스트 노드, 요소 노드를 포함한 내부의 모든 컨텐츠에 접근할 수 있다.
console.log(buyList.innerHTML);
/* 

    <li>두부</li>
    <li>계란</li>
    <li>라면 <span hidden>안성탕면</span></li>
  
*/

// 텍스트 노드의 부모 요소 노드
const lastLi = buyList.lastElementChild;
console.log(lastLi); // <li>라면 <span hidden="">안성탕면</span></li>
console.log(lastLi.innerHTML); // 라면 <span hidden="">안성탕면</span>
```

<br />

### outerHTML

해당 요소의 모든 자식 요소를 포함하고 `요소 자신까지 포함`한 컨텐츠에 접근하거나 수정할 수 있다.

```javascript
// 요소 노드를 선택
const buyList = document.querySelector('#buy-list');
console.log(buyList);
/*
  <ul id="buy-list" class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면 <span hidden>안성탕면</span></li>
  </ul>
*/

// 자신을 포함한 공백 텍스트 노드, 요소 노드를 포함한 컨텐츠에 접근할 수 있다.
console.log(buyList.outerHTML);
/* 
<ul id="buy-list" class="list">
    <li>두부</li>
    <li>계란</li>
    <li>라면 <span hidden="">안성탕면</span></li>
  </ul>
*/

// 텍스트 노드의 부모 요소 노드
const lastLi = buyList.lastElementChild;
console.log(lastLi); // <li>라면 <span hidden="">안성탕면</span></li>
console.log(lastLi.outerHTML); // <li>라면 <span hidden="">안성탕면</span></li>
```

<br />

### insertAdjacentHTML(position, string)

매개변수로 전달 받은 **문자열을 HTML로 파싱하고 그 결과로 생성된 노드**를 `DOM tree`의 **지정된 위치에 삽입**한다. 첫번째 매개변수는 삽입 위치, 두번째 매개변수는 문자열을 받는다.

```html
<!-- 매개변수로 올 수 있는 삽입 위치 값 -->

<!-- beforebegin -->
<li>
  <!-- afterbegin -->
  두부
  <!-- beforeend -->
</li>
<!-- afterend -->
```

```javascript
// 요소 노드를 선택
const firstLi = document.querySelector('#buy-list > li:first-child');
console.log(firstLi); // <li>두부</li>

firstLi.insertAdjacentHTML('beforeend', ' <span>순두부</span>');
console.log(firstLi); // <li>두부 <span>순두부</span></li>
```




<br />
<br />




## DOM 제어

새로운 노드를 생성하여 **DOM을 제어**할 수 있다. DOM을 제어해 새로운 노드를 추가하거나 삭제하면 **리플로우와 리페인트가 발생하여 성능에 영향**을 준다. 성능 최적화를 위해 주의해서 다루는게 좋다.

<br />

### 노드 생성

`createElement(tagName)` : 지정한 태그명으로 **요소 노드를 생성**한다.

`createTextNode(text)` : 지정한 내용으로 **텍스트 노드를 생성**한다.

`createAttribute(attributeName)` : 지정한 속성명으로 **속성 노드를 생성**한다.

```javascript
// <li> 요소 노드 생성
const elemNode = document.createElement('li');

// '아이언맨' 텍스트 노드 생성
const textNode = document.createTextNode('아이언맨');

// 'class' 속성 노드 생성
const attrNode = document.createAttribute('class');
```

<br />

### 노드 추가, 삽입, 이동

`요소노드.appendChild(Node)` : 지정한 노드를 요소 노드의 **마지막 자식 노드로 추가**한다.

`요소노드.insertBefore(Node, targetNode)` : 추가할 노드(Node)를 요소 노드의 자식중 **지정한 노드의 앞에 삽입**한다.

```html
<ul id="movies" class="list">
  <li>어벤저스</li>
  <li>다크나이트</li>
  <li>미션임파서블</li>
</ul>
```

```javascript
const movieList = document.querySelector('#movies');
const elemNode = document.createElement('li');
const textNode = document.createTextNode('아이언맨');

// appendChild - 추가
elemNode.appendChild(textNode); // <li>아이언맨</li>
movieList.appendChild(elemNode);
/*
<ul id="movies" class="list">
  <li>어벤저스</li>
  <li>다크나이트</li>
  <li>미션임파서블</li>
  <li>아이언맨</li>
</ul>
*/

// insertBefore - 삽입
movieList.insertBefore(elemNode, movieList.firstChild);
/*
<ul id="movies" class="list">
  <li>아이언맨</li>
  <li>어벤저스</li>
  <li>다크나이트</li>
  <li>미션임파서블</li>
</ul>
*/
```

`appendChild`로 추가해준 요소 노드가 있고, `insertBefore`로 삽입해준 요소 노드가 있는데 총 2 곳에 추가되는 것이 아닌 위치만 바뀐 채로 나온다. 그 이유는 `elemNode`는 하나의 노드 객체이기 때문에 `DOM tree` 내에서 동시에 두 위치에 존재할 수 없다. 그래서 처음에 `appendChild`로 추가해준 요소노드가 `insertBefore` 메서드로 인해 지정한 위치에 삽입, 즉, `이동`한거라 볼 수 있다.

#### 속성 값을 추가하는 방법

```javascript
const attrNode = document.createAttribute('class');
const elemNode = document.createElement('li');

attrNode.value = 'highlight'; // class="highlight"
elemNode.setAttributeNode(attrNode); // <li class="highlight"></li>

// setAttribute 메서드로 간편하게 가능
elemNode.setAttribute('class', 'highlight'); // <li class="highlight"></li>
```

<br />

### 노드 교체

`요소노드.replaceChild(newChild, oldChild)` : 요소 노드의 자식 노드인 `oldChild` 노드를 `newChild` 노드로 **교체**한다.

```html
<ul id="movies" class="list">
  <li>어벤저스</li>
  <li>다크나이트</li>
  <li>미션임파서블</li>
</ul>
```

```javascript
const movieList = document.querySelector('#movies');

const newChild = document.createElement('li');
newChild.textContent = '토르'; // <li>토르</li>

const oldChild = movieList.firstElementChild; // <li>어벤저스</li>

movieList.replaceChild(newChild, oldChild);
/*
<ul id="movies" class="list">
  <li>토르</li>
  <li>다크나이트</li>
  <li>미션임파서블</li>
</ul>
*/
```

노드를 교체할 때 주의할점이 있다면, **교체할 노드가 요소 노드인지 공백 텍스트 노드인지 정확히 지정**해줘야 한다.

<br />

### 노드 삭제

`요소노드.removeChild(childNode)` : **지정한 자식 노드를 삭제**한다.

`요소노드.remove()` : **자신을 삭제**한다.

```html
<ul id="movies" class="list">
  <li>어벤저스</li>
  <li>다크나이트</li>
  <li>미션임파서블</li>
</ul>
```

```javascript
const movieList = document.querySelector('#movies');

// <li>다크나이트</li> 자식 노드 삭제
movieList.removeChild(movieList.firstElementChild.nextElementSibling);

// <li>미션임파서블</li> 자신을 삭제
movieList.lastElementChild.remove();

console.log(movieList);
/*
<ul id="movies" class="list">
  <li>어벤저스</li>
</ul>
*/
```

<br />

### 노드 복사

`요소노드.cloneNode([deep: true | false])` : **지정한 노드를 복사하여 생성**한다.
  - 매개변수 deep에 `true`를 전달하면, **모든 자손 노드를 포함**하여 복사 생성한다.
  - 매개변수 deep에 `false`를 전달하면, **지정한 요소 노드 자신만**을 복사 생성한다.
  - 기본값은 `false`

```html
<ul id="movies" class="list">
  <li>어벤저스</li>
  <li>다크나이트</li>
  <li>미션임파서블</li>
</ul>
```

```javascript
const movieList = document.querySelector('#movies');
const firstLi = movieList.firstElementChild; // <li>어벤저스</li>

// false
const cloneFalse = firstLi.cloneNode(); // <li></li>
cloneFalse.textContent = '헐크'; // <li>헐크</li>
movieList.appendChild(cloneFalse);
/*
<ul id="movies" class="list">
  <li>어벤저스</li>
  <li>다크나이트</li>
  <li>미션임파서블</li>
  <li>헐크</li>
</ul>
*/

// true
const cloneTrue = movieList.cloneNode(true);
movieList.appendChild(cloneTrue);
/*
<ul id="movies" class="list">
  <li>어벤저스</li>
  <li>다크나이트</li>
  <li>미션임파서블</li>
  <li>헐크</li>
  <ul id="movies" class="list">
    <li>어벤저스</li>
    <li>다크나이트</li>
    <li>미션임파서블</li>
    <li>헐크</li>
  </ul>
</ul>
*/
```




<br />
<br />




## 속성(Attribute) 제어

`Attribute`는 HTML 요소의 **동작을 제어하기 위한 추가적인 정보를 제공**한다. 그리고 HTML 요소는 여러개의 속성을 가질 수 있다. HTML 문서가 파싱될 때 HTML 요소의 `Attribute`는 `Attribute 노드`로 변환되어 요소 노드와 연결된다. `Attribute`의 갯수만큼 노드가 생성된다.

`Element.getAttribute(attributeName)` : 속성 **값을 참조**한다.

`Element.setAttribute(attributeName, value)` : 속성 **값을 변경**한다.

`Element.hasAttribute(attributeName)` : 속성 **값을 가지고 있는지 확인**한다.

`Element.removeAttribute(attributeName)` : 속성 **값을 제거**한다.

```html
<a href="https://www.naver.com/">네이버</a>

<img src="https://shop-phinf.pstatic.net/20240829_79/1724913716663qTrqm_PNG/11281302375656299_1436107326.png?type=f320_320" 
width="160" 
format="png" 
data-age="6" 
data-user-name="user">

<input type="text" name="userName">
```

```javascript
// 표준 속성 접근
console.log(a.href); // https://www.naver.com/
console.log(img.src); // https://shop-phinf.pstatic.net/202 ... 320
console.log(img.width); // 160
console.log(input.type); // text
console.log(input.name); // userName

// 비표준 속성을 추가해서 사용해도 문제없이 동작은 하지만, 권장되진 않는다.
console.log(img.format); // undefined, 비표준 속성은 속성에 접근할 수 없다.
console.log(img.getAttribute('format')); // png, 메서드로 접근할 수 있다.

// 권장되는 표준적인 커스텀 속성을 사용하는 것이 좋다.
// data-* 속성을 사용
console.log(img.getAttribute('data-age')); // 6
console.log(img.getAttribute('data-user-name')); // user

// dataset 객체의 속성으로 접근 가능
console.log(img.dataset.age); // 6
console.log(img.dataset.userName); // user

// 속성 추가도 가능
img.dataset.address = '서울시';

// 속성 값을 가지는지 확인
console.log(img.hasAttribute('data-address')); // true

// 속성 값을 제거
img.removeAttribute('data-address');
console.log(img.hasAttribute('data-address')); // false
```




<br />
<br />




## 스타일(Style) 제어

요소 노드의 `인라인 스타일`을 제어하거나, CSS class로 미리 작성하여 `class 속성`으로 스타일을 제어할 수 있다. `class 속성`을 사용하면 재사용성과 성능, 유지보수 측면에서 더 좋기 때문에 이 방법을 권장한다.

<br />

### 인라인 스타일 제어

```html
<div class="box red"><h1>Hello World~!</h1></div>
```

```javascript
const box = document.querySelector('.box');

// Element.style : HTML 요소의 인라인 style 정보가 객체로 저장되어 있다.
console.log(box.style); // CSSStyleDeclaration {accentColor: '', additiveSymbols: '', …}

// Element.style.속성명 형태로 사용한다.
box.style.color = 'blue'; // 변경
box.style.width = '100px'; // 추가
box.style.hight = '100px'; // 추가

// '-' 케밥 케이스는 카멜 케이스로 적용된다.
box.style.backgroundColor = 'yellow';

// 모든 스타일을 한번에 바꿀 수 있다.
box.style.cssText = 'color: black; font-size: 24px; background-color: pink;';
```

<br />

### 클래스(class) 제어

```html
<div class="box red"><h1>Hello World~!</h1></div>
```

```javascript
const box = document.querySelector('.box');

// Element.className : class 값을 공백으로 구분된 문자열로 반환한다.
console.log(box.className); // box red
box.className = box.className.replace('red', 'blue'); // 교체 후 반환 값을 다시 대입
console.log(box.className); // box blue

// Element.classList : class 속성의 정보를 갖는 유사 배열 객체를 반환한다.
console.log(box.classList); // DOMTokenList(2) ['box', 'blue', value: 'box blue']

// 유용한 메서드들을 제공한다.
// add(...className) : 1개 이상의 속성 값을 추가한다.
box.classList.add('foo');
console.log(box.className); // box blue foo
box.classList.add('big', 'small');
console.log(box.className); // box blue foo big small

// remove(...className) : 1개 이상의 속성 값을 제거한다.
box.classList.remove('foo');
console.log(box.className); // box blue big small
box.classList.remove('big', 'small');
console.log(box.className); // box blue

// item(index) : 인덱스에 해당하는 class를 반환한다.
let item1 = box.classList.item(0); // box
console.log(item1); // box
let item2 = box.classList.item(1); // blue
console.log(item2); // blue

// contains(className) : 전달받은 값과 일치하는 class의 존재 여부를 확인한다.
item1 = box.classList.contains('box');
console.log(item1); // true
item2 = box.classList.contains('red');
console.log(item2); // false

// replace(oldClassName, newdClassName) : 기존 class를 새로운 class로 변경한다.
box.classList.replace('blue', 'red');
console.log(box.className); // box red

// toggle(className) : 전달한 값이 존재하면 제거하고, 존재하지 않으면 추가한다.
box.classList.toggle('foo');
console.log(box.className); // box red foo
box.classList.toggle('foo');
console.log(box.className); // box red
```

<br />

### 모든 CSS 스타일 확인

style 프로퍼티는 인라인 스타일만 반환한다. 그래서 클래스를 적용한 스타일이나 상속을 통해 적용된 스타일, 외부 CSS 파일 등의 스타일은 참조할 수 없다.

HTML 요소에 적용되어 있는 모든 CSS 스타일을 참조해야 할 경우 `getComputedStyle` 메서드를 사용한다.

```html
<head>
  <style>
    .box::after {
      content: ' World~!';
    }
  </style>
</head>
<body>
  <span class="box">Hello</span>
</body>
```

```javascript
const box = document.querySelector('.box');

const computedStyle = window.getComputedStyle(box, '::after');
console.log(computedStyle.content); //  World~!
```