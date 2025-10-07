# 제어문 ( Control flow statement )

- [조건문](#조건문)
  - [if](#if)
  - [switch](#switch)
- [반복문](#반복문)
  - [for](#for)
  - [반복문 제어 (break, contunue)](#반복문-제어-break-contunue)
  - [while](#while)
  - [do-while](#do-while)




<br />
<br />




## 조건문

특정 조건일 때만 원하는 코드가 실행되도록 만들 수 있다.

<br />

### `if`

조건이 맞을 때만 해당 코드 블럭을 실행한다.

```javascript
// if (조건) { }
// if (조건) { } else { }
// if (조건-1) { } else if (조건-2) { } else { }
let fruit = 'apple';
if (fruit === 'apple') {
  console.log('🍎'); // 🍎
} else {
  console.log('🍊');
}

fruit = 'orange';
if (fruit === 'apple') {
  console.log('🍎');
} else {
  console.log('🍊'); // 🍊
}

fruit = 'pear';
if (fruit === 'apple') {
  console.log('🍎');
} else if (fruit === 'orange') {
  console.log('🍊');
} else {
  console.log('else'); // else
}

// 조건식의 조건이 맞지 않으면 false이므로 코드 블럭은 실행이 되지 않는다.
if (2 < 1) {
  console.log('출력 ❌');
}
```

<br />

#### `삼항 조건 연산자`

`if`문을 조금 더 심플하게 작성할 수 있는 방법이다.

```JavaScript
let fruit = 'orange';

// if - else 문
if (fruit === 'apple') {
  console.log('🍎');
} else {
  console.log('❌'); // ❌
}

// 삼항 조건 연산자
// 조건식 ? 표현식(참인 경우) : 표현식(거짓인 경우);
fruit === 'apple' ? console.log('🍎') : console.log('❌'); // ❌

// 다른 방식 표현
let result = fruit === 'apple' ? '🍎' : '❌';
console.log(result); // ❌
```

<br />

### `switch`

조건문이긴 하지만 `if`와는 조금 성격이 다르다.

```JavaScript
// if, else if, else if, ..., else 반복적으로 연결해서 사용해야 하는 경우
// 특정한 범위 안에 있는 조건에 한해서만 검사한다면, switch로 대체해서 깔끔하게 작성할 수 있다.
let day = 3; // 0: 월요일, 1: 화요일, ..., 6: 일요일
let dayName;
if (day === 0) {
  dayName = '월요일';
} else if(day === 1) {
  dayName = '화요일';
} else if(day === 2) {
  dayName = '수요일';
} else if(day === 3) {
  dayName = '목요일';
} else if(day === 4) {
  dayName = '금요일';
} else if(day === 5) {
  dayName = '토요일';
} else if(day === 6) {
  dayName = '일요일';
} else {
  console.log('해당하는 요일 없음!');
}
console.log(dayName); // 목요일

// switch
day = 4;
switch (day) {
  case 0:
    dayName = '월요일';
    break;
  case 1:
    dayName = '화요일';
    break;
  case 2:
    dayName = '수요일';
    break;
  case 3:
    dayName = '목요일';
    break;
  case 4:
    dayName = '금요일';
    break;
  case 5:
    dayName = '토요일';
    break;
  case 6:
    dayName = '일요일';
    break;
  default: // else 구문과 동일, 모든 조건에 해당하지 않는 경우에 코드를 실행
    console.log('해당하는 요일 없음!');
}
console.log(dayName); // 금요일

// 각각의 케이스는 해당 조건의 코드가 수행이 된 다음에 멈출 수 있도록 `break`를 걸어주는게 중요하다.
// 조건이 맞지 않으면 코드가 실행되지 않고 다음 조건으로 넘어가고, 조건이 맞아 코드가 실행이 되면 멈추고 다음 케이스를 확인하지 않는다.
```

<br />

#### `break`가 없는 경우

`break`가 없으면 조건이 맞아도 다음 케이스로 넘어가서 결국에는 마지막에 있는 케이스가 실행이 된다.

```JavaScript
let day = 4;
switch (day) {
  case 0:
    dayName = '월요일';
  case 1:
    dayName = '화요일';
  case 2:
    dayName = '수요일';
  case 3:
    dayName = '목요일';
  case 4:
    dayName = '금요일';
  case 5:
    dayName = '토요일';
  case 6:
    dayName = '일요일';
}
console.log(dayName); // 일요일
```

<br />

#### `break`를 사용하지 않아도 되는 경우

하나 이상의 여러가지 케이스가 동일한 코드를 수행해야 한다면 `break`를 사용하지 않아도 된다.

```JavaScript
let condition = 'good';
let text;

switch (condition) {
  case 'good':
  case 'okay':
    text = '좋음!';
    break;
  case 'bad':
    text = '나쁨!';
    break;
}

console.log(text); // 좋음!
```




<br />
<br />




## 반복문

반복적으로 동일한 코드가 실행되도록 만들 수 있다. 해당하는 조건식의 조건이 맞을 때까지 코드 블록을 실행한다.

<br />

### `for`

```JavaScript
// for (변수선언문; 조건식; 증감식;) { }
// 실행순서
// 1. 변수선언문을 수행하여 변수를 초기화한다.
// 2. 조건식의 값이 참이면 { } 코드 블럭을 실행한다.
// 3. 증감식을 수행하여 값을 증가시킨다.
// 4. 조건식이 거짓이 될 때까지 2번과 3번을 반복한다.
for (let i = 0; i < 5; i++) {
  console.log(i);
}
/*
0
1
2
3
4
*/

for (let i = 1; i < 5; i = i + 2) {
  console.log(i);
}
/*
1
3
*/

// 반복문 중첩
for (let i = 0; i < 5; i++) {
  for (let j = 0; j < 5; j++) {
    console.log(i, j);
  }
}
/*
i j
0 0
0 1
0 2
0 3
0 4
.
.
.
4 0
4 1
4 2
4 3
4 4
*/

// 무한루프
// 반복이 중지되지 않고 반복적으로 코드 블록이 무한히 실행되는 상태를 말한다. 
// 프로그램이 멈추지 않고 한 가지 동작만 계속 수행하게 되며, 
// 프로그램이 멈추거나 시스템 자원을 과도하게 사용하게 될 수 있다. 
// 조건식이 언젠가는 거짓이 되어 반복문이 중지 되도록 코드를 작성해주는 것이 좋다.
for (;;) {
  console.log('❗️'); // ❗️❗️❗️❗️❗️❗️❗️...
}
```

<br />

### 반복문 제어 (`break`, `contunue`)

반복문 안에서도 흐름을 제어할 수 있다.

#### `break`

특정한 조건에서 반복문을 그만두고 싶을 때 사용할 수 있다.

```JavaScript
for (let i = 0; i < 10; i++) {
  if (i === 7) {
    console.log('i가 7이 되었다!');
    break;
  }
  console.log(i);
}
/*
0
1
2
3
4
5
6
i가 7이 되었다!
*/
```

#### `continue`

`continue`가 나오는 순간 그 아래에 있는 코드들은 무시되고, 그 다음으로 바로 증액을 하고, 증액된 조건이 맞으면 코드 블럭을 실행한다.

```javascript
// 7이 되는 순간 7의 인덱스 값은 출력하지 않는다.
for (let i = 0; i < 10; i++) {
  if (i === 7) {
    console.log('i가 7이 되었다!');
    continue;
  }
  console.log(i);
}
/*
0
1
2
3
4
5
6
i가 7이 되었다!
8
9
*/

// 7이 되는 순간 continue 아래에 console.log를 모두 출력하지 않는다.
for (let i = 0; i < 10; i++) {
  if (i === 7) {
    continue;
    console.log('i가 7이 되었다.');
  }
  console.log(i);
}
/*
0
1
2
3
4
5
6
8
9
*/

// 인덱스 값 출력없이 진행하다가 7일 때만 해당 코드 블록을 출력한다.
for (let i = 0; i < 10; i++) {
  if (i === 7) {
    console.log('i가 7이 되었다.');
  }
  continue;
  console.log(i);
}
/*
i가 7이 되었다.
*/
```

<br />

### `while`

```JavaScript
// while (조건) { }
// 조건이 false가 될 때까지 { } 코드 블럭을 반복 실행한다.
// 변수를 초기화 하거나 증감하는 부분이 들어 있지 않으므로 따로 작성해줘야 한다.
let num = 5;

while (num >= 0) {
  console.log(num);
  num--;
}
/*
5
4
3
2
1
0
*/


// 무한루프
// 조건식은 항상 true이며 증감식이 따로 없어 i는 0에 머물고 1000에 도달 할 수 없어서 반복 수행한다.
let isActive = true;
let i = 0;

while (isActive) {
  console.log('still alive');
  if (i === 1000) {
    break;
  }
}
/*
still alive
still alive
still alive
.
.
.
*/

// 조건식이 언젠가는 끝날 수 있도록 만들어 줘야 한다❗️
while (isActive) {
  console.log('still alive');
  if (i === 1000) {
    break;
  }
  i++;
}
/*
still alive
still alive
still alive
.
.
.
still alive (1000개)
*/
```

<br />

### `do-while`

`while`은 조건이 `true`일 때만 동작하고, `false`일 때는 코드 블럭이 동작하지 않는다. 하지만,  `do-while`은 처음에 무조건 한 번 실행하고 나서 그 다음에 조건을 검사한다.

```JavaScript
// while
let isActive = false;
let i = 0;

while (isActive) {
  console.log('still alive');
  if (i === 1000) {
    break;
  }
  i++;
}
// 조건이 false이므로 동작하지 않는다.


// do-while
do {
  console.log('do-while still alive');
} while (isActive);
// do-while still alive
// 한 번 실행하고 나서 조건이 false이므로 동작하지 않는다.
```