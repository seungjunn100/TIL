# HTTP 통신과 Ajax - Fetch, Axios

- [Fetch API를 이용한 렌더링](#fetch-api를-이용한-렌더링)
- [Axios 라이브러리를 이용한 렌더링](#axios-라이브러리를-이용한-렌더링)




<br />
<br />




## Fetch API를 이용한 렌더링

![Fetch API를 이용한 렌더링](../src/images/board-fetch-render.png)

### BoardInfo 컴포넌트

```tsx
function BoardInfo() {
  const [ data, setData ] = useState<BoardInfoView | null>(null);
  const [ isLoading, setIsLoading ] = useState(true);
  const [ error, setError ] = useState<Error | null>(null);

  const requestInfo = async () => {
    try {
      setIsLoading(true);
      const response = await fetch('https://fesp-api.koyeb.app/market/posts/6', {
        headers: {
          'client-id': 'openmarket',
        }
      });

      const jsonBody: ResData<BoardInfoRes> = await response.json();
      console.log(jsonBody);

      if (jsonBody.ok) {
        setData(jsonBody.item);
        setError(null);
      } else {
        throw new Error(jsonBody.message);
      }
    } catch(err) {
      setError(err as Error);
      setData(null);
    } finally {
      setIsLoading(false);
    }
  };

  useEffect(() => {
    requestInfo();
  }, []);

  return (
    <>
      { isLoading && <p>로딩중...</p> }

      { error && <p>{ error.message }</p> }

      {
        data && 
        <>
          <h2>{ data.title }</h2>
          <p>{ data.content }</p>
        </>
      }

      <CommentList />
    </>
  );
}
```

- `Fetch API`를 통해 `6`번 게시물의 데이터를 요청한다.
  
  - 헤더에 클라이언트 아이디를 추가해 어떤 클라이언트 측에서 요청을 보냈는지 식별할 수 있도록 한다.

- `fetch`의 응답은 `JSON` 형태의 문자열로 오기 때문에 자바스크립트 객체로 파싱해줘야 한다.

- 응답에 성공하거나 실패할 경우에 따라 상태 관리를 통해 렌더링을 다시 하거나 하지 않도록 관리할 수 있다.

- 이 모든 작업은 컴포넌트가 마운트 된 후에 `useEffect`에 의해 실행이 된다.

  - `BoardInfo` 컴포넌트에서는 `<CommentList />` 컴포넌트를 렌더해야 하기 때문에 아직 `useEffect`는 실행되지 않는다.

<br />

### CommentList 컴포넌트

```tsx
function CommentList() {
  const [ data, setData ] = useState<BoardReply[] | null>(null);
  const [ isLoading, setIsLoading ] = useState(true);
  const [ error, setError ] = useState<Error | null>(null);

  const requestCommentList = async () => {
    try {
      setIsLoading(true);
      const response = await fetch('https://fesp-api.koyeb.app/market/posts/6/replies', {
        headers: {
          'client-id': 'openmarket',
        }
      });

      const jsonBody: ResData<BoardReplyRes> = await response.json();
      console.log(jsonBody);

      if (jsonBody.ok) {
        setData(jsonBody.item);
        setError(null);
      } else {
        throw new Error(jsonBody.message);
      }
    } catch(err) {
      setError(err as Error);
      setData(null);
    } finally {
      setIsLoading(false);
    }
  }

  useEffect(() => {
    requestCommentList();
  }, []);

  const list = data?.map(reply => <li key={reply._id}>{ reply.content }</li>);

  return (
    <>
      { isLoading && <p>로딩중...</p> }

      { error && <p>{ error.message }</p> }
      
      {
        data && 
        <>
          <h3>댓글 목록</h3>
          <ul>
            { list }
          </ul>
        </>
      }

      <CommentNew reload={ requestCommentList } />
    </>
  );
}
```

- `Fetch API`를 통해 `6`번 게시물의 댓글들의 데이터를 요청한다.

- `BoardInfo` 컴포넌트와 동일하게 동작한다.

<br />

### CommentNew 컴포넌트

```tsx
function CommentNew({ reload }: { reload: () => void }) {
  const [ isLoading, setIsLoading ] = useState(false);
  const [ error, setError ] = useState<Error | null>(null);

  const requestAddComment = async (formData: FormData) => {
    try {
      setIsLoading(true);

      const jsonBody = Object.fromEntries(formData.entries());
      const response = await fetch('https://fesp-api.koyeb.app/market/posts/6/replies', {
        method: 'POST',
        headers: {
          'client-id': 'openmarket',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(jsonBody)
      });

      const jsonData: ResData<BoardReplyCreateRes> = await response.json();

      if (jsonData.ok) {
        console.log('등록 성공');
        reload();
        return true;
      } else {
        if (jsonData.errors) {
          throw new Error(jsonData.errors.content.msg)
        }
        throw new Error(jsonData.message);
      }
    } catch(err) {
      setError(err as Error);
      return false;
    } finally {
      setIsLoading(false);
    }
  }
  
  const handleAddComment = async (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    const formElem = event.currentTarget;
    const formData = new FormData(formElem);
    const result = await requestAddComment(formData);
    
    if (result) {
      formElem.reset();
    }
  }
  
  return (
    <>
      <h4>댓글 등록</h4>
      <form onSubmit={ handleAddComment }>
        <textarea name="content" rows={3} cols={30} placeholder="댓글 내용"></textarea>
        <br />
        <button type="submit" disabled={ isLoading }>등록</button>
        { error && <span>{ error.message }</span> }
      </form>
    </>
  );
}
```

- `Fetch API`를 통해 `6`번 게시물의 댓글을 등록하는 데이터를 요청한다.

- `textarea`에 내용을 입력하고 전송 버튼을 눌러 `submit` 이벤트를 발생시킨다.

  - `submit`의 기본 동작으로 새로고침이 발생하므로 막아줘야 한다.
  
- `event.currentTarget`는 `form` 요소를 가르킨다.

- `new FormData(formElem)`는 `form` 요소들의 `name`을 `key`로, 입력 값을 `value`로 담아준다.
  
  - `FormData`는 폼 데이터를 서버로 보내기 위한 표준 데이터 컨테이너이다.

  - `textarea`에 `댓글 등록`이라는 내용을 입력했다면, 
    
    - `"content" → "댓글 등록"` 데이터가 `FormData` 안에 들어간다.

- 게시물의 댓글을 요청을 보내려면 객체로 변환 후 `JSON` 형태로 바꾸어 `body`에 전달해줘야 한다.

  - `formData.entries()`에 의해 `"content" → "댓글 등록"` 데이터를 `["content", "댓글 등록"]` 형태로 내보낸다.

    - 여러 값들이 있다면 순서대로 쌍을 이루어 전달한다.
  
  - `Object.fromEntries()`에 의해 한 쌍을 이룬 값들을 모아서 일반 객체형태로 만든다.
  
    ```tsx
    jsonBody = {
      content: "댓글 등록",
      ...
    }
    ```

  - 마지막으로 객체를 `JSON` 형태로 바꾸어 `body`에 담아 요청한다.

  - `headers`에 `'Content-Type': 'application/json'` `JSON` 형태의 타입으로 보낸다고 지정해줘야 인식할 수 있다.

  ![댓글 등록](../src/images/board-fetch-post.png)

- 등록에 성공하면,

  -  댓글 리스트들을 다시 렌더링해주기 위해 `CommentList` 컴포넌트의 `API`에 요청을 다시 할 수 있도록 `props`로 전달 받아 `reload()`를 실행한다.

- `API`에 등록된 형식에 맞지않아 등록에 실패하면,

  - 실패했을 때의 데이터를 전달 받는데, 입력값에 따라 에러메세지를 출력할 수 있다.

    ![댓글 등록 실패](../src/images/board-fetch-error.png)

  - 어떤 에러가 올지 모르고 다양한 에러의 형식이 저장되어 있으므로 인덱스 시그니처를 활용하여 동적으로 속성을 정의할 수 있도록 타입을 설정해 주는 것이 좋다.

    ![댓글 등록 실패 타입](../src/images/board-fetch-error-type.png)

- 이렇게 마지막 컴포넌트가 마운트된 후에 앞에 정의했던 `useEffect`가 순차적으로 실행된다.




<br />
<br />




## Axios 라이브러리를 이용한 

### Axios Instance

```ts
import axios from "axios";

const API_SERVER = 'https://fesp-api.koyeb.app/market';

export function getAxiosInstance() {
  const instance = axios.create({
    baseURL: API_SERVER,
    timeout: 1000*10,
    headers: {
      'Content-Type': 'application/json',
      Accept: 'application/json',
      'Client-Id': 'openmarket',
    }
  });

  return instance;
}
```

- `API` 요청에 필요한 공통 옵션을 한 곳에서 관리하기 위한 파일이다.

- 각 컴포넌트에서 동일한 설정을 반복하지 않아도 되며,
  
  - 서버 주소나 헤더 변경 시 한 곳만 수정하면 되어 유지보수가 쉬워진다.

<br />

### BoardInfo 컴포넌트

![Axios BoardInfo 컴포넌트](../src/images/axios-boardinfo.png)

- `fetch API` 방법에서 아래의 코드만 바꿔주면 된다.

- `Axios`는 내부적으로 `JSON` 파싱을 자동으로 해준다.

<br />

### CommentList 컴포넌트

![Axios CommentList 컴포넌트](../src/images/axios-commentlist.png)

- `fetch API` 방법에서 아래의 코드만 바꿔주면 된다.

- `Axios`는 내부적으로 `JSON` 파싱을 자동으로 해준다.

<br />

### CommentNew 컴포넌트

![Axios CommentNew 컴포넌트](../src/images/axios-commentnew.png)

- `fetch API` 방법에서 아래의 코드만 바꿔주면 된다.

- `Axios`는 내부적으로 `JSON` 파싱을 자동으로 해준다.