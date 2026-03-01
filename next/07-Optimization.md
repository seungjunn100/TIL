# 최적화

- [이미지 최적화](#이미지-최적화)
- [스크립트 최적화](#스크립트-최적화)
  - [외부 스크립트](#외부-스크립트)
  - [인라인 스크립트](#인라인-스크립트)
- [정적 컨텐츠 최적화](#정적-컨텐츠-최적화)
  - [`public` 폴더](#public-폴더)
  - [폰트 최적화](#폰트-최적화)
  - [압축 및 캐싱](#압축-및-캐싱)




<br />
<br />




## 이미지 최적화

Next.js는 `Image` 컴포넌트를 통해 이미지를 자동으로 최적화한다.

- 장치 크기에 맞는 이미지를 자동으로 제공하며, `WebP`, `AVIF` 같은 최신 포맷으로 변환

- `width`, `height` 속성을 지정해 이미지 로딩 시 발생하는 레이아웃 이동(`CLS`) 방지

- 뷰포트에 들어올 때 이미지를 로드하는 지연 로딩(`lazy loading`) 기본 적용

- `placeholder="blur"` + `blurDataURL` 속성으로 저화질 이미지를 먼저 보여주고 점차 선명하게 전환 가능

<br />

외부 이미지를 사용할 경우 `next.config.ts`에 허용할 도메인을 명시해야 한다.

```ts
// next.config.ts
const nextConfig: NextConfig = {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'example.com',
        pathname: '/images/**',
      },
    ],
  },
};
```




<br />
<br />




## 스크립트 최적화

`Script` 컴포넌트로 외부 스크립트를 최적화해서 로딩할 수 있다.

<br />

### 외부 스크립트

`layout`에서 로딩하면 해당 레이아웃 안의 여러 페이지를 이동해도 스크립트는 한 번만 로드된다.

```tsx
// app/map/layout.tsx
import Script from 'next/script';

export default function MapLayout({ children }) {
  return (
    <>
      {children}
      
    </>
  );
}
```

작은 코드, 즉시 실행 필요, 외부 요청 없이 처리할 때 사용한다.

<br />

### 인라인 스크립트

`JavaScript` 코드를 직접 작성할 때 사용한다.

`id` 속성이 필수이며, 같은 `id`를 가진 스크립트는 중복 실행을 방지한다.

주의할 점은 인라인 스크립트는 클라이언트 컴포넌트에서만 사용 가능하다.

```tsx
'use client';
import Script from 'next/script';

export default function Banner() {
  return (
    <>
      배너 내용
      
        {`document.getElementById('banner').classList.remove('hidden')`}
      
    </>
  );
}
```

큰 라이브러리, 캐싱 활용, 별도 파일로 관리에 사용한다.




<br />
<br />




## 정적 컨텐츠 최적화

### `public` 폴더

`public` 폴더에 넣은 파일은 `/`로 시작하는 경로로 어디서든 접근 가능하다.

```
public/logo.png       →  /logo.png
public/images/bg.jpg  →  /images/bg.jpg
```

빌드 시 그대로 복사되어 배포되며, 서버/클라이언트 컴포넌트 모두에서 사용 가능하다.

<br />

### 폰트 최적화

`next/font`를 사용하면 폰트를 자동으로 최적화한다.

외부 폰트 서버로의 요청 없이 `self-hosting`으로 제공되며, 폰트 로딩 중 레이아웃이 흔들리는 현상(`layout shift`)을 방지한다.

```tsx
import { Inter } from 'next/font/google';

const inter = Inter({ subsets: ['latin'] });

export default function Layout({ children }) {
  return {children};
}
```

<br />

### 압축 및 캐싱

별도 설정 없이 자동으로 적용된다.

- `Gzip`, `Brotli` 압축으로 파일 크기를 줄여 전송 시간 단축

- 정적 파일에 `Cache-Control` 헤더를 자동 설정해 브라우저 캐싱 및 `CDN` 캐싱 지원

- 재방문 시 캐시된 파일을 사용해 네트워크 요청 최소화