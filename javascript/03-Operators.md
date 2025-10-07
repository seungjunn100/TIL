# 연산자 ( Operators )

- [표현식](#표현식)
  - [문 ( Statement )](#문--statement)
  - [표현식 ( Expressions )](#표현식--expressions)
- [산술 연산자](#산술-연산자)
- [단항 연산자](#단항-연산자)
- [할당 연산자](#할당-연산자)
- [증가 & 감소 연산자](#증가--감소-연산자)
- [비교 연산자](#비교-연산자)
- [동등 & 일치 연산자](#동등--일치-연산자)
- [논리 연산자](#논리-연산자)
- [연산자 우선순위](#연산자-우선순위)




<br />
<br />




## 표현식

### 문 ( Statement )

코드에서 실행 가능한 `최소 단위`를 의미한다. `선언문`, `할당문`, `조건문`, `반복문` 등이 이에 해당한다.

```JavaScript
let a; // 선언문
a = 10; // 할당문
if (a > 5) { } // 조건문
for (let i=0; i<10; i++) { } // 반복문
```

<br />

### 표현식 ( Expressions )

`값`으로 평가될 수 있는 `문`을 의미한다.

```JavaScript
1; // 숫자 리터럴 표현식
a + 1; // 연산자 표현식
call(); // 함수 호출 표현식, 함수를 호출하면 특정한 값이 반환된다.
b = 2; // 할당문, 할당 표현식

let b; // 선언문, 값으로 평가될 수 없기 때문에 표현식 ❌
```




<br />
<br />




## 산술 연산자

```JavaScript
// + 더하기
// - 빼기
// * 곱하기
// / 나누기
// % 나머지 값
// ** 지수(거듭 제곱)
console.log(5 + 2); // 7
console.log(5 - 2); // 3
console.log(5 * 2); // 10
console.log(5 / 2); // 2.5
console.log(5 % 2); // 1
console.log(5 ** 2); // 25, 거듭제곱은 es7에서 추가 되었다.
console.log(5 ** 3); // 125
console.log(Math.pow(5, 2)); // 25, 그 전에는 Math.pow() 함수를 사용했다.

// + 연산자 주의점❗️
let text = '두 문장을' + ' 연결';
console.log(text); // 두 문장을 연결, 문자열
text = '1' + 1;
console.log(text); // 11, 숫자와 문자열을 더하면 문자열로 변환된다.
```




<br />
<br />




## 단항 연산자

```JavaScript
// + (양)
// - (음)
// ! (부정)
let a = 5;
a = -a;
console.log(a); // -5
a = -a;
console.log(a); // 5
a = +a;
console.log(a); // 5
a = -a; // -5
a = +a; // +(-5)
console.log(a); // -5

let boolean = true;
console.log(boolean); // true
console.log(!boolean); // false
console.log(!!boolean); // true
console.log(!1); // false, ! - 부정 연산자
console.log(!!1); // true, !! - 값을 불리언 타입으로 변환

// + 연산자를 사용하면, 숫자가 아닌 타입들을 숫자로 변화하면 어떤 값이 나오는지 확인할 수 있다.
console.log(+false); // 0
console.log(+null); // 0
console.log(+''); // 0
console.log(+true); // 1
console.log(+'text'); // NaN
console.log(+undefined); // NaN
```




<br />
<br />




## 할당 연산자

```JavaScript
let a = 1;
a = a + 2;
console.log(a); // 3

a += 2; // a = a + 2; 축약 버전
console.log(a); // 5

a -= 2;
console.log(a); // 3

a *= 2;
console.log(a); // 6

a /= 2;
console.log(a); // 3

a %= 2;
console.log(a); // 1

a **= 2;
console.log(a); // 1
```




<br />
<br />




## 증가 & 감소 연산자

```JavaScript
let a = 0;
console.log(a); // 0
a++; // a = a + 1;, 하나 증가해서 변수 자기 자신에게 다시 할당해준다.
console.log(a); // 1
a--; // a = a - 1;, 하나 감소해서 변수 자기 자신에게 다시 할당해준다.
console.log(a); // 0

// 주의❗️
// a++(a--) 필요한 연산을 하고, 그 뒤에 값을 증가(감소)시킴
// ++a(--a) 값을 먼저 증가(감소)하고, 필요한 연산을 함
a = 0;
let b = a++; // a의 현재 값(0)을 먼저 b에 할당하고, 그 뒤에 a 값을 증가시킨다.
console.log(b); // 0, 먼저 a의 현재 값을 할당 받아 0이 된다.
console.log(a); // 1, 그 뒤에 값을 증가 시킨다.

a = 0;
b = ++a; // a의 값이 먼저 증가하고 나서, b에 증가된 a의 값을 할당 받게 된다.
console.log(b); // 1

// 출력할 때도 동일하다.
// 필요한 연산을 하는데, 여기서는 출력이 먼저 되어 a의 값이 0이 되고 그 뒤에 값을 증가시켜 a를 출력해보면 증가된 값을 할당 받게된다.
a = 0;
console.log(a++); // 0
console.log(a); // 1
```




<br />
<br />




## 비교 연산자

```JavaScript
// > 크다.
// < 작다.
// >= 크거나 같다.
// <= 작거나 같다.
// 불리언 타입으로 반환한다.
console.log(3 > 2); // true
console.log(3 < 2); // false
console.log(2 > 3); // false
console.log(2 < 3); // true
console.log(3 >= 2); // true
console.log(3 >= 3); // true
console.log(3 >= 4); // false
console.log(2 <= 3); // true
console.log(3 <= 3); // true
console.log(4 <= 3); // false
```




<br />
<br />




## 동등 & 일치 연산자

```JavaScript
// == 값이 같다. (동등)
// != 같이 다르다.
// === 값과 타입이 둘다 같다. (일치)
// !== 값과 타입이 다르다.
console.log(2 == 2); // true
console.log(2 == 3); // false
console.log(2 != 2); // false
console.log(2 != 3); // true
console.log(2 == '2'); // true, 타입은 비록 다르지만 숫자와 문자열을 비교할 때 문자열 안에 있는 숫자가 숫자로 자동으로 변환이 된다.
console.log(2 === '2'); // false, 코딩을 할 때는 왠만하면 타입까지 함께 확인을 해주는게 좋다.⭐️
console.log(true == 1); // true
console.log(true === 1); // false
console.log(false == 0); // true
console.log(false === 0); // false

// 객체 비교
const obj1 = {
  name: 'js',
};
const obj2 = {
  name: 'js',
};
console.log(obj1 == obj2); // false, 두 변수에는 각 객체가 들어있는 각 메모리의 주소를 가지고 있으므로 값이 다르다.
console.log(obj1 === obj2); // false, 타입은 같지만, 값 자체가 다르다.
console.log(obj1.name == obj2.name); // true
console.log(obj1.name === obj2.name); // true

const obj3 = obj2;
console.log(obj2 == obj3); // true
console.log(obj2 === obj3); // true
console.log(obj2.name == obj3.name); // true
console.log(obj2.name === obj3.name); // true
// 변수의 값으로 같은 메모리 주소를 갖고 있으며, 같은 객체를 갖고 있으므로 모두 동일하다.
```




<br />
<br />




## 논리 연산자

```JavaScript
// && (and) - 모든 조건이 맞으면 ⭕
// || (or) - 하나의 조건만 맞아도 ⭕
// ! - 부정 (단항 연산자)
let num = 8;
if (num >= 0 && num < 9) {
  console.log('👍'); // 👍
}

num = 20;
if (num >= 0 || num < 9) {
  console.log('👍👍'); // 👍👍
}

num = 11;
if (num != 11) {
  console.log('👎'); // num이 11이 아닐 때만 출력 하는 조건이므로 출력되지 않는다.
}
num = 10;
if (num != 11) {
  console.log('👎'); // 👎
}

// 앞의 값이 참이면 뒤의 값을 반환
// 앞의 값이 거짓이면 앞의 값을 반환
console.log(true && true); // true
console.log(true && false); // false
console.log(false && true); // false
console.log(false && false); // false

// 앞의 값이 참이면 앞의 값을 반환
// 앞의 값이 거짓이면 뒤의 값을 반환
console.log(true || true); // true
console.log(true || false); // true
console.log(false || true); // true
console.log(false || false); // false
```




<br />
<br />




## 연산자 우선순위

```JavaScript
let a = 2;
let b = 3;
let result = a + b * 4;
console.log(result); // 14

// 원하는 연산 순서를 꼭 지키고 싶다면 ()를 사용, () - 우선 순위가 제일 높다.
result = (a + b) * 4;
console.log(result); // 20
result = ((a + b) * 4) / 5;
console.log(result); // 4

console.log(a); // 2
result = a++ + b * 4; // 14, a에는 a의 현재 값(2)을 받게되고, 문이 끝난 다음에 a = 3이 된다.
console.log(a); // 3
console.log(result); // 14
```