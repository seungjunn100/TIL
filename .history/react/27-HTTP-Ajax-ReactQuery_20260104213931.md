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