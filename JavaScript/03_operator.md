# 연산자(Operator)


<br />


### 문(Statement)
- 코드에서 최소 실행할 수 있는 한줄의 단위

- `선언문`, `할당문`, `조건문`, `반복문`


<br />


### 표현식(Expressions)

- `값`으로 평가 될 수 있는 문

```javascript
1; // 숫자 리터럴 표현식
1 + 1; // 연산자 표현식
call(); // 함수 호출 표현식, 함수를 호출하면 특정한 값이 반환이 되므로
let b; // 선언문, 표현식 ❌
b = 2; // 할당문, 표현식
let a = (b = 2); // (b = 2)라는 표현식이 계산되어 a에 재할당이 되는 순서
```


<br />


### 리터럴(Literal)

- 코드에서 값을 나타내는 표기법

- `123`, `’123’`, `true`, `{}`, `[]`, `템플릿 리터럴`, `function() {}` (함수), `123n` (BigInt), `0b101` (Binary)


<br />
<br />


## 산술 연산자(Arithmetic Operator)
```javascript
// + 더하기
// - 빼기
// * 곱하기
// / 나누기
// % 나머지값
// ** 지수(거듭제곱)
console.log(5 + 2); // 7
console.log(5 - 2); // 3
console.log(5 * 2); // 10
console.log(5 / 2); // 2.5
console.log(5 % 2); // 1
console.log(5 ** 2); // 25, ES7 버전 이후
console.log(Math.pow(5, 2)); // 25, 거듭제곱, ES7 버전 이전

// + 연산자 주의점!
let text = '두 문장의' + '합';
console.log(text); // 두 문장의 합

text = '1' + 1; // 숫자와 문자열을 더하면 문자열로 반환된다.
console.log(text); // 11 - 문자열
```


<br />
<br />


## 단항 연산자(Unary Operator)
```javascript
// + 양
// - 음
// ! 부정
let a = 5;
a = -a;
console.log(a); // -5

a = -a;
console.log(a); // 5

a = -a; // -5
a = +a; // +(-5)
console.log(a); // -5 

let boolean = true;
console.log(boolean); // true
console.log(!boolean); // false
console.log(!!boolean); // true

// + 연산자를 쓰면 숫자가 아닌 타입들을 숫자로 변환하면 어떤 값이 나오는지 확인할 수 있다.
console.log(+false); // 0
console.log(+null); // 0
console.log(+''); // 0
console.log(+true); // 1
console.log(+'text'); // NaN
console.log(+undefined); // NaN

console.log(!!1); // true, !! - 값을 boolean 타입으로 변환
console.log(!1); // false, ! - 부정연산자
```


<br />
<br />


## 할당 연산자(Assignment Operator)
```javascript
// = 할당
let a = 1;
a = a + 2;
console.log(a); // 3

a += 2; // a = a + 2; 축약버전 
console.log(a); // 5

a -= 1; // 4
a *= 3; // 12
a /= 2; // 6
a %= 4; // 2
a **= 2; // 4
```


<br />
<br />


## 증감 연산자(Incremoent, Decrement Operator)
```javascript
let a = 0;
console.log(a); // 0
a++; // a = a + 1;
console.log(a); // 1
a-- // a = a - 1;
console.log(a); // 0

// 주의!
// a++(--) 필요한 연산을 먼저하고, 그 뒤에 값을 증가(감소)시킨다.
// ++(--)a 값을 먼저 증가(감소)시키고, 그 뒤에 필요한 연산을 한다.
a = 0;
let b = a++;
console.log(b); // 0, 할당 연산(=)이 먼저 진행 되어 0이 출력
console.log(a); // 1, 연산이 끝나고 값을 증가 시켰으므로 1이 출력

a = 0;
let b = ++a;
console.log(a); // 1, 값을 먼저 증가 시켰으므로 1이 출력
console.log(b); // 1, 값을 먼저 증가시키고, 연산을 하였으므로 1이 출력

a = 0;
console.log(a++); // 0, a = 0 이 먼저 출력이 된 후
console.log(a); // 1, ++ 연산자로 인해 증가 시킨 값이 출력이 된다.
```


<br />
<br />


## 비교 연산자(Relational Operator)
```javascript
// > 크다
// < 작다
// >= 크거나 같다
// <= 작거나 같다
console.log(2 > 3); // false
console.log(2 < 3); // true
console.log(2 <= 3); // true
console.log(3 <= 3); // true
console.log(2 >= 3); // false
```


<br />
<br />


## 연산자 우선순위(Operator Priority)
```javascript
let a = 2;
let b = 3;
let result = a + b;
console.log(result); // 5

result = a + b * 4; // (b * 4)의 계산이 먼저 진행, 계산식에서 *, / 가 먼저 계산이 된다.
console.log(result); // 14

result = (a + b) * 4; // 우선 순위를 두고 싶다면 ()를 이용하여 계산식을 작성해 준다.
console.log(result); // 20

result = a++ + b * 4;
console.log(result); // 14, a++은 먼저 a의 값이 할당되고 위의 계산식이 마친 후 나중에 증가하므로 아래의 결과로 확인 할 수 있다.

console.log(a); // 3

result = a + b * 4;
console.log(result); // 15
```
- [우선순위 참고](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operator/Operator_precedence)

<br />
<br />


## 동등 비교 관계 연산자(Equality Operator)
```javascript
// == 값이 같다.
// != 값이 다르다.
// === 값과 타입이 둘다 같다.
// !== 값과 타입이 다르다.
console.log(2 == 2); // true
console.log(2 != 2); // false
console.log(2 != 3); // true
console.log(2 == '2'); // true, 타입은 다르지만 값은 같다., 숫자와 문자열을 비교할 때 문자열 안에 있는 숫자가 숫자로 자동으로 변환이 되어  비교가 된다.
console.log(2 === '2'); // false, 코딩을 할때는 왠만하면 타입까지 확인 해주는것이 좋다! ⭐️
console.log(true == 1); // true
console.log(true === 1); // false
console.log(false == 0); // true
console.log(false === 0); // false

const obj1 = {
  name: 'js',
};
const obj2 = {
  name: 'js',
};
console.log(obj1 == obj2); // false, 메모리에서 객체 변수의 값(object)을 저장할 때 각기 다른 메모리 주소에 저장된 후 각기 다른 메모리의 주소값이 객체 변수의 값으로 들어가기 때문이다.
console.log(obj1.name == obj2.name); // true, 같은 문자열 타입을 가지고 있기 때문이다. 
console.log(obj1.name === obj2.name); // true, 같은 문자열 타입과 값을 가지고 있기 때문이다. 

let obj3 = obj2;
console.log(obj3 == obj2); // true, 같은 참조값(메모리 주소값)을 가지고 있기때문이다.
console.log(obj3 === obj2); // true, 같은 값과 같은 object 타입을 가지고 있기 때문이다.
```


<br />
<br />


## 논리 연산자(Logical Operator)
```javascript
// && 그리고
// || 또는
// ! 부정(단항연산자에서 온것)
// !! 불리언값으로 변환 (단항연산자 응용버전)

let num = 8;

if (num >= 0 && num < 9) { // 둘 다 true면 출력
  console.log('👍'); // 👍
}

if (num >= 0 || num > 20) { // 둘중 하나만 true여도 출력
  console.log('👍'); // 👍
}

if (!(num >= 0 || num > 20)) { // 전체를 부정할 수도 있다.
  console.log('👍');  // 값이 true인데 부정하여 출력 X
}

if (num != 8) { // num이 8이 아닐 때 출력
  console.log('👍'); // num = 8 이므로 출력 X
}

console.log(true && true); // true
console.log(true && false); // false
console.log(false && true); // false
console.log(false && false); // false

console.log(true || true); // true
console.log(true || false); // true
console.log(false || true); // true
console.log(false || false); // false

console.log(!'text'); // false
console.log(!!'text'); // true
```
