# 호이스팅 ( Hoisting )

`호이스팅`은 **끌어올리다라는 뜻**으로, 자바스크립트 엔진(Interpreter)에 의해 코드가 실행 되기 전에 호이스팅 단계를 거치는데, 이때 **변수나 함수의 선언문을 끌어 올리는 것을 의미**한다. 

`함수`는 코드의 제일 아래에다가 선언해도 호이스팅되어 최상단에서 호출이 가능해진다.

```javascript
// 원래 작성한 코드
console.log(add(10, 20)); // 30
function add(a, b) {
  return a + b;
}
console.log(add(30, 40)); // 70


// 호이스팅 단계
function add(a, b) {
  return a + b;
}
console.log(add(10, 20)); // 30
console.log(add(30, 40)); // 70
```

`변수`는 선언과 초기화를 분리한 후, 선언만 코드의 최상단으로 호이스팅한다.

`var`로 선언한 변수의 경우에는 선언만 되고 그 값은 `undefined`로 초기화 된다.

```javascript
// 원래 작성한 코드
console.log(a); // undefined
var a = 10;


// 호이스팅 단계
var a;
console.log(a); // undefined
a = 10;
```

`let`, `const`로 선언한 변수의 경우에는 호이스팅은 되지만, 초기화 전에 접근 불가능한 상태 `TDZ(Temporal Dead Zone)`가 되어 에러가 발생한다.

```javascript
// 원래 작성한 코드
console.log(b); // Cannot access 'b' before initialization
let b = 20;


// 호이스팅 단계
let b; // 선언만 되고 초기화되기 전에 TDZ 상태가 된다.

// TDZ(Temporal Dead Zone) ~
b = ...
// ~ TDZ(Temporal Dead Zone)

console.log(b); // Cannot access 'b' before initialization

b = 20;
console.log(b); // 20
```

`함수`는 정의 방식에 따라서도 약간의 차이가 있다. 함수 선언문만 호이스팅되며, 함수 표현식은 호이스팅되지 않는다.

```javascript
// var로 선언한 변수로써 호이스팅 단계에서 선언만 하고 undefined 값으로 초기화하여 함수를 실행할 수 없다.
console.log(add); // undefined
console.log(add(10, 20)); // add is not a function

var add = function(x, y){
  return x + y;
};

console.log(add(10, 20));


// const로 선언한 변수로써 초기화 전에 접근 불가능한 상태 TDZ(Temporal Dead Zone)가 되어 에러가 발생한다.
console.log(add); // Cannot access 'add' before initialization
console.log(add(10, 20)); // Cannot access 'add' before initialization

// 함수 표현식
const add = function(x, y){
  return x + y;
};

console.log(add(10, 20));
```




















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


이와 같은 문제 때문에 함수 표현식만을 사용할 것을 권고하고 있다. 함수 호이스팅이 함수 호출 전 반드시 함수를 선언하여야 한다는 규칙을 무시하므로 코드의 구조를 엉성하게 만들 수 있다고 지적한다.

또한 함수 선언문으로 함수를 정의하면 사용하기에 쉽지만 대규모 애플리케이션을 개발하는 경우 인터프리터가 너무 많은 코드를 변수 객체(VO)에 저장하므로 애플리케이션의 응답속도는 현저히 떨어질 수 있으므로 주의해야 할 필요가 있다.