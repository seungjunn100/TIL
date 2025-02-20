# 객체(Object)
- 서로 연관있는 속성과 행동을 묶어 주기 위해 사용된다.
```javascript
// 순수 데이터 객체
let apple = {
	name: 'apple', // 속성(Property), 데이터
	color: 'red',
	display: ‘🍎’,
}

// 객체 축약 버전
const x = 0;
const y = 0;
const coordinate = { x, y } // { x: x, y: y };
console.log(coordinate); // { x: 0, y: 0 }

function makeObj(name, age) {
  return {
    name, // name: name,
    age, // age: age,
  };
}
console.log(makeObj('bbaek', '1995')); // { name: 'bbaek', age: '1995' }

// 객체 안의 함수
const apple = {
  name: 'apple',
  display: function () {
    console.log(`${this.name}: 🍎`);
  },
}
apple.display(); // apple: 🍎
```


<br />
<br />


## 객체 리터럴
```javascript
// Object literal { key: value }
// new Object()
// Object.create();
// key - 문자, 숫자, 문자열, 심볼
// value - 원시값, 객체(함수)
let apple = {
  name: 'apple', // 문자로 작성하는게 좋다.
  'hello-bye': '👋🏻', // 특수한 경우에만 작성
  0: 1,
  ['hello-bye1']: '👋🏻👋🏻',
}

// 속성, 데이터에 접근하는 방법
console.log(apple.name); // apple // 마침표 표기법 dot notation
console.log(apple['name']); // apple // 대괄호 표기법 Bracket notation
console.log(apple['hello-bye']); // 👋🏻
console.log(apple['hello-bye1']); // 👋🏻👋🏻
console.log(apple['0']); // 1

// 속성 추가
apple.emoji = '⭐️';
console.log(apple.emoji); // ⭐️
console.log(apple['emoji']); // ⭐️

// 속성 삭제
delete apple.emoji;
console.log(apple); // { '0': 1, name: 'apple', 'hello-bye': '👋🏻', 'hello-bye1': '👋🏻👋🏻' }
```


<br />
<br />


## 객체 동적으로 접근하기
```javascript
const obj = {
  name: 'bbaek',
  age: '1995',
}
// 코딩하는 시점에, 정적으로 접근이 확정됨
console.log(obj.name); // bbaek
console.log(obj.age); // 1995


// 동적으로 속성에 접근하고 싶을때 대괄호 표기법 사용!
function getValue(obj, key) { // 전달되는 속성에 따라서 값을 반환한다.
  return obj[key];
}
console.log(getValue(obj, 'name')); // bbaek


// 동적으로 속성 추가
function addKey(obj, key, value) {
  obj[key] = value;
}
addKey(obj, 'job', 'engineer');
console.log(obj); // { name: 'bbaek', age: '1995', job: 'engineer' }


// 동적으로 속성 삭제
function deleteKey(obj, key) {
  delete obj[key];
}
deleteKey(obj, 'job');
console.log(obj); // { name: 'bbaek', age: '1995' }
```


<br />
<br />


## 생성자 함수
```javascript
const apple = {
  name: 'apple',
  display: function () {
    console.log(`${this.name}: 🍎`);
  },
}

const orange = {
  name: 'orange',
  display: function () {
    console.log(`${this.name}: 🍊`);
  },
}

// 생성자 함수, 함수이름이 대문자로 시작
// 객체를 만들어 낼 수 있는 템플릿(양식)
// 데이터를 주입해서 객체를 생성할 수 있다.
function Fruit(name, emoji) {
  this.name = name; // this는 객체 자기 자신을 가르키고 name이라는 key가 만들어지고 name 인자로 전달된 값을 할당 받는다.
  this.emoji = emoji;
  this.display = () => {
    console.log(`${this.name}: ${this.emoji}`);
  }
  // return this; // 생성자 함수에서는 자동으로 return이 가능하므로 생략 가능
}

const apple = new Fruit('apple', '🍎');
const orange = new Fruit('orange', '🍊');

console.log(apple); // Fruit { name: 'apple', emoji: '🍎', display: [Function (anonymous)] }
apple.display(); // apple: 🍎
console.log(orange); // Fruit { name: 'orange', emoji: '🍊', display: [Function (anonymous)] }
orange.display(); // orange: 🍊
```
