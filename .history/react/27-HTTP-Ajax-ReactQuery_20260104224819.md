# HTTP 통신과 Ajax - React Query(Tanstack Query)

- [React Query(Tanstack Query)](#react-querytanstack-query)
- [React Query를 이용한 렌더링](#react-query를-이용한-렌더링)




<br />
<br />




## React Query(Tanstack Query)

- `API` 서버에서 가져온 데이터(서버 상태)를 대신 관리해주는 라이브러리이다.

- `API` 서버로부터 받아온 데이터를 자동으로 캐싱하고, 서버 상태와 클라이언트 상태를 동기화해준다.

- `API` 데이터를 직접 관리하면 로딩 상태, 에러 상태, 데이터 캐싱 등을 `useEffect`, `useState`, `axios/fetch`로 직접 코드를 작성해야 한다.

  - 코드의 양이 방대해지고, 버그가 발생할 확률이 높아지며 유지보수가 어려워진다.
  
  - 이러한 것들을 `React Query`가 대신 처리해준다.

<br />

### useQuery

- 서버에서 가져온 데이터를 상태처럼 관리해주는 훅이다.

  - 요청, 로딩, 에러, 캐싱, 재요청까지 한 번에 처리해준다.

- 응답받은 데이터는 자동으로 캐싱되며, 동일한 쿼리 요청 시 서버에 재요청하지 않고 캐싱된 데이터를 반환한다.

- 기본적으로 브라우저 포커스 복귀 시 자동으로 다시 요청한다.

<br />

#### 기본 사용 구조

```tsx
const { data, isLoading, error } = useQuery({
  queryKey: ['posts'],
  queryFn: () => axiosInstance.get<BoardListRes>('/posts'),
  select: (response) => response.data.item,
});
```

- `queryKey` (필수)

  - 쿼리를 식별하는 고유한 키 값
  - 동일한 `queryKey`를 사용하는 쿼리는 같은 요청으로 인식되어 캐시된 결과를 공유
  - 계층적 구조로 작성하여 관련된 쿼리를 그룹화 가능

- `queryFn` (필수)

  - 쿼리 실행 시 호출되는 함수로, `Promise`를 반환해야 함
  - 일반적으로 `axios`나 `fetch`를 사용한 `API` 호출 함수를 반환

- `select` (선택)

  - `queryFn`이 반환한 데이터를 변환하거나 필요한 필드만 추출하는 함수
  - `select` 함수가 반환한 값이 쿼리의 `data`로 설정됨

- `staleTime`

  - 데이터가 `fresh` 상태에서 `stale` 상태로 변경되는 시간 (밀리초, 기본값: 0)

- `gcTime`
  
  - 사용되지 않는 캐시 데이터가 메모리에서 제거되기까지의 시간 (기본값: 5분)

- 더 다양한 옵션 : https://tanstack.com/query/latest/docs/framework/react/reference/useQuery

<br />

#### useQuery가 반환하는 값

상태를 객체로 반환한다.

- `isLoading`: 쿼리가 처음 실행 중이거나 데이터가 없을 때 `true` (캐시된 데이터가 있으면 `false`)

- `isFetching`: 쿼리가 현재 실행 중일 때 `true` (백그라운드 재요청 포함)

- `error`: 쿼리 실행 중 발생한 에러 객체

- `data`: 쿼리 성공 시 받은 데이터 (초기에는 `undefined`)

- `status`: 쿼리 상태 (`pending`, `error`, `success`)

- 더 다양한 속성 : https://tanstack.com/query/latest/docs/framework/react/reference/useQuery

<br />

#### 캐시의 주요 상태

- 리액트 쿼리의 캐시는 쿼리의 생명 주기를 관리한다.

- `Fresh` (신선한 상태) : 데이터가 최신이라고 간주되는 상태

  ```tsx
  useQuery({
    queryKey: ['posts', 1],
    queryFn: () => axiosInstance.get<BoardListRes>('/posts'),
    staleTime: 1000 * 60, // 1분
  });
  ```

  - `staleTime` 동안 `fresh` 상태를 유지한다.
  - `fresh` 상태에서는 자동 `refetch`가 일어나지 않는다.
  - 같은 쿼리를 다른 컴포넌트에서 호출해도 네트워크 요청 없이 캐싱된 걸 반환한다.

- `Stale` (오래된 상태) : `staleTime`이 지난 후의 캐시 상태

  - 동일한 쿼리 요청 시 먼저 캐시된 데이터를 반환하고, 백그라운드에서 서버에 새로운 데이터를 요청한다.
  - 서버에서 데이터가 도착하면 캐시를 업데이트하고 컴포넌트를 리렌더링

- `Inactive`

<br />

### useMutation




<br />
<br />




## React Query를 이용한 렌더링

![Board React Query](../src/images/board-react-query.png)

### main 컴포넌트

```tsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.tsx'
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import { ReactQueryDevtools } from '@tanstack/react-query-devtools';

const queryClient = new QueryClient();

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <QueryClientProvider client={ queryClient }>
      <App />
      <ReactQueryDevtools />
    </QueryClientProvider>
  </StrictMode>,
)
```

#### `const queryClient = new QueryClient();`

- 리액트 쿼리의 데이터 캐시 저장소이다.

- 모든 쿼리의 요청 상태(`data`, `loading`, `error` 등)를 메모리에 저장한다.

- 쿼리 실행, 캐시 무효화, 재요청(`refetch`) 등의 작업을 조율한다.

<br />

#### `<QueryClientProvider client={ queryClient }>`

- 이 `Provider` 아래에 있는 모든 컴포넌트는 `queryClient`에 접근할 수 있다.

- 리액트 쿼리의 모든 훅(`useQuery`, `useMutation`, `useQueryClient` 등)은 내부적으로 `React Context`를 통해 `queryClient`에 접근할 수 있다.

<br />

#### `<ReactQueryDevtools />`

- 이 개발 툴을 사용하면 화면 하단에 개발자 패널이 뜨게 된다.

- 현재 활성화된 모든 쿼리의 상태를 실시간으로 볼 수 있다.

  - 각 쿼리의 `queryKey`
  - 캐시에 들어있는 데이터
  - `stale`, `fresh`, `inactive` 상태

- 수동으로 액션(`refetch`, `invalidate` , `reset` 등) 제어

<br />

### BoardList 컴포넌트

```tsx
const axiosInstance = getAxiosInstance();

function BoardList() {
  const { data, isLoading, error } = useQuery({
    queryKey: ['posts'],
    queryFn: () => axiosInstance.get<BoardListRes>('/posts'),
    select: (response) => response.data.item,
  });

  const list = data?.map(post => (
    <li key={ post._id }>
      <button onClick={ () => handleUpdatePost(post._id) }>{ post._id }. { post.title }</button>
    </li>
  ))

  const [ postId, setPostId ] = useState<number>(1);

  const handleUpdatePost = (id: number) => {
    setPostId(id);
  };

  return (
    <>
      <h1>게시물 목록</h1>

      { isLoading && <p>게시물 목록 로딩중...</p> }

      { error && <p>{ error.message }</p> }

      { data && 
        <ul>
          { list }
        </ul>
      }

      { postId && <BoardInfo postId={ postId } /> }
    </>
  );
}
```