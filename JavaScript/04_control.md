# 제어문(Control flow statement)
- 코드의 흐름을 제어한다.


<br />
<br />


## 조건문(Conditional statement)
- 특정한 조건일때만 코드 실행되도록 만들 수 있다.

- `if`
  ```javascript
  // if(조건) { }
  // if(조건) { } else { }
  // if(조건1) { } else if(조건2) { } else { }
  let fruit = 'apple';
  if (fruit === 'apple') {
    console.log('🍎'); // 🍎 출력
  }

  fruit = 'orange';
  if (fruit === 'apple') {
    console.log('🍎');
  } else {
    console.log('🍊'); // 🍊 출력
  }

  fruit = 'something';
  if (fruit === 'apple') {
    console.log('🍎');
  } else if (fruit === 'orange') {
    console.log('🍊');
  } else {
    console.log('!?'); // !? 출력
  }

  // if 안에는 true나 false로 평가될 수 있는 표현식이 들어갈 수 있다.
  if (false) {
    console.log('출력 X');
  }
  if (true) {
    console.log('출력 O');
  }

  // 삼항 조건 연산자(Ternary Operator)
  // 방법 - 1
  fruit === 'apple' ? console.log('🍎') : console.log('🍊'); // 🍎 출력
  // 방법 - 2
  let emoji = fruit === 'apple' ? '🍎' : '🍊'; // 🍎 출력
  console.log(emoji);
  ```

- `switch`
  ```javascript
  // if else if else if ... else
  let day = 4; // 0 : 월요일, 1 : 화요일, 2 : 수요일, ..., 6 : 일요일
  let dayName;
  if (day === 0) {
    dayName = '월요일';
  } else if (day === 1) {
    dayName = '화요일';
  } else if (day === 2) {
    dayName = '수요일';
  } else if (day === 3) {
    dayName = '목요일';
  } else if (day === 4) {
    dayName = '금요일';
  } else if (day === 5) {
    dayName = '토요일';
  } else if (day === 6) {
    dayName = '일요일';
  } else { // 모든 조건에 해당하지 않는 경우일 때 코드를 실행
    console.log('해당하는 요일이 없음!');
  }
  console.log(dayName); // 금요일

  // switch
  switch (day) {
    case 0:
      dayName = '월요일';
      break; 
      // 다음 코드를 확인하지 않도록 멈춰줘야 한다.
      // 브레이크문이 없을 경우 제일 마지막 코드가 실행이 된다.
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
    default: // 모든 조건에 해당하지 않는 경우일 때 코드를 실행
      console.log('해당하는 요일이 없음!');
  }
  console.log(dayName); // 금요일

  // break문 없어도 되는 경우
  let condition = 'bad'; // okay, good -> 좋음!, bad -> 나쁨!
  let text;
  switch (condition) {
    // 같은 코드를 실행해야할 때 break문은 한번만 사용하면 된다!
    case 'okay':
    case 'good':
      text = '좋음!';
      break;
    case 'bad':
      text = '나쁨!';
      break;
  }
  console.log(text); // 나쁨!
  ```


<br />
<br />


## 반복문(Loop statement)
- 반복적으로 동일한 코드를 실행시킬 수 있다.

- `for`
  ```javascript
  // for(변수선언문; 조건식; 증감식) { } // 해당하는 조건이 맞을때까지 코드를 실행해준다.
  // 실행순서
  // 1. 변수선언문을 실행하여 변수 초기화한다.
  // 2. 조건식의 값이 참이면 { } 코드블럭을 수행한다.
  // 3. 증감식을 수행한다.
  // 4. 조건식이 거짓이 될때까지 2번과 3번을 반복한다.

  for (let i = 0; i < 5; i++) {
    console.log(i);
  } // 0, 1, 2, 3, 4

  // 중첩
  for (let i = 0; i < 5; i++) {
    for (let j = 0; j < 5; j++) {
      console.log(i, j);
    }
  }
  // i, j
  // 0, 1
  // 0, 2
  // 0, 3
  // 0, 4
  // 1, 1
  // 1, 2
  // 1, 3
  // 1, 4
  // 2, 1
  // 2, 2
  // 2, 3
  // 2, 4
  // 3, 1
  // 3, 2
  // 3, 3
  // 3, 4
  // 4, 1
  // 4, 2
  // 4, 3
  // 4, 4

  // 무한루프
  // 다른 코드를 수행하지 않고 반복적으로 코드를 계속 출력하게 된다.
  // 조건문은 항상 거짓으로 될 수 있도록 루프가 언젠가는 종료가 되도록 코딩을 하는게 중요하다.
  for (;;) {
    console.log('😳');
  } // 😳, 😳, 😳, 😳, ...

  // 반복문 제어 : continue, break;
  for (let i = 0; i < 10; i++) {
    if (i === 5) {
      console.log('i가 5가 되었다.');
    }
    console.log(i);
  } // 0, 1, 2, 3, 4, i가 5가 되었다., 5, 6, 7, 8, 9

  for (let i = 0; i < 10; i++) {
    if (i === 5) {
      console.log('i가 5가 되었다.');
      break;
    }
    console.log(i);
  } // 0, 1, 2, 3, 4, i가 5가 되었다.

  for (let i = 0; i < 10; i++) {
    if (i === 5) {
      continue; // 아래에 있는 코드는 무시하고 다음 코드로 넘어간다.
      console.log('i가 5가 되었다.');
      break;
    }
    console.log(i);
  } // 0, 1, 2, 3, 4, 6, 7, 8, 9
  ```

- `while`
  ```javascript
  // while (조건) { }
  // 조건이 false가 될때까지 { } 코드블럭을 반복 실행한다.

  let num = 5;
  while (num >= 0) {
    console.log(num);
    num--;
  }
  // 5, 4, 3, 2, 1, 0

  let isActive1 = true; // while은 조건이 맞을 때에만 실행한다.
  let i = 0;
  while (isActive1) {
    console.log('아직 살아있다!');
    if (i === 1000) {
      // continue;
      break;
    }
    i++;
  }
  // 아직 살아있다!, 아직 살아있다!, ..., 아직 살아있다!
  ```

- `do-while`
  ```javascript
  // 일단 먼저 한번 실행하고 나서 while의 조건을 검사한다.
  let isActive2 = false; // 조건이 맞지 않으므로 isActive2는 실행되지 않아야 하지만, do-while문에 의해 한번은 실행이 된다.
  do {
    console.log('do-while 아직 살아있다!');
  } while(isActive2);
  ```