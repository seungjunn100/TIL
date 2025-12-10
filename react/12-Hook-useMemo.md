# useMemo

- [useMemo](#usememo-1)




<br />
<br />




## useMemo

지정한 함수를 호출하여 반환받은 결과값을 내부에 저장(캐싱)하는 훅

- 비용이 큰 연산을 매 렌더링마다 다시 계산하지 않을 때 사용한다.

```tsx
const calculateValue = function () { };

const cachedValue = useMemo(calculateValue, dependencies);
```

- `calculateValue` : 저장할 값을 계산하여 반환하는 함수

- `dependencies` : 의존성 배열

  - 배열의 값이 변경되면 `calculateValue` 함수를 다시 호출하고,
    
    - 변경되지 않았다면 이전 계산값(캐시된 값)을 그대로 재사용한다.
  
  - 빈 배열을 지정하면 `calculateValue` 함수는 처음 렌더링될 때 1번만 호출된다.
  
    - 최초 렌더링된 후 계산된 값이 저장되어 리렌더링 되더라도 최초 캐싱된 값만 반환한다.

<br />

### 사용 예시

```tsx
// 지정한 수가 소수인지 여부를 반환
const isPrime = function(num: number){
  console.time('소요 시간');
  console.log('소수 판별 시작', num);

  let prime = true;

  for(let i=2; i<num; i++){
    if(num % i === 0){
      prime = false;
      break;
    }
  }

  console.log('소수 판별 결과', prime);
  console.timeEnd('소요 시간');

  return prime;
};

function App() {
  console.log('App 호출');
  useEffect(() => {
    console.log('App 마운트 완료');
  }, []);

  const [ username, setUsername ] = useState('GD');
  const [ num, setNum ] = useState(1);

  const prime = isPrime(num);

  return (
    <>
      <h1>05 useMemo - 함수의 반환값을 memoize</h1>
      <div>
        <input type="text" name="username" value={ username } onChange={ (e) => setUsername(e.target.value) } />가 좋아하는 숫자: 
        <input type="number" name="number" min="1" max="1000000007" value={ num } onChange={ (e) => setNum(Number(e.target.value)) } />
        <div>
          <span>{ username }가 좋아하는 숫자 { num }: 소수가 </span>
          { prime ? 
            <span style={{ color: 'blue' }}>맞습니다.</span>
          : 
            <span style={{ color: 'red' }}>아닙니다.</span>
          }
        </div>
      </div>
    </>
  )
}
```

- 숫자를 입력하는 `input`에 `상태값(num)`을 증가하거나 감소하면 리렌더링이 되는데,

  - 해당 상태값을 `isPrime` 함수의 인자로 전달해 소수 여부를 `boolean` 값으로 판별하고,

  - 반환 받은 `boolean` 값 `prime`에 따라 해당 태그가 리렌더링된다.

- 그리고, 이름을 입력하는 `input`에 상태값에 따라 리렌더링이 발생하는데,

  - 이 때도, `isPrime` 함수가 동작하여 소수 여부를 판별하게 된다.
  
  - 하지만, 이름을 입력할 때 `isPrime`이 동작하여 `prime` 값에 따라 리렌더링 될 필요는 없다.

- `prime` 값을 `useMemo`를 통해 `isPrime` 함수에서 반환받은 결과값으로 저장해두고 사용하면, 이름을 변경할 때 `isPrime` 함수는 동작하지 않아도 된다.

```tsx
// 지정한 수가 소수인지 여부를 반환
const isPrime = function(num: number){ ... };

function App() {
  ...

  // const prime = isPrime(num);
  
  const prime = useMemo(() => isPrime(num), [num]);

  ...
}
```

- 이름을 변경할 때 리렌더링이 되지만 메모이제이션에 의해 `isPrime` 함수는 동작하지 않고 캐싱된 값을 사용한다.

- 하지만 `dependencies`에 `num` 값을 할당해, `숫자(num)`를 입력하는 `input`요소에 의해 입력값이 바뀔 때는 `isPrime` 함수가 동작하고 새로운 값으로 다시 캐싱된다.