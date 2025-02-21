# CSS의 단위
- `px`, `%`, `em`, `rem`, `vw`, `vh`, `vmin`, `vmax`

<br />

## `px`
- CSS에서 사용하는 가장 기본적인 픽셀(화소) 단위이다.

- 브라우저의 크기가 변하여도 고정된 크기를 갖는 절대 단위이다.


<br />
<br />


## `%`
- 기준 : 부모 요소의 크기

- 요소의 크기를 부모 요소의 크기에 대한 백분율로 설정한다.

```html
<body>
  <div class="outBox">

    <div class="inBox">
    </div>

  </div>
</body>
```
```css
.outBox {
  width: 300px;
  height: 300px;
}

.inBox {
  width: 50%; /* 150px */
  height: 50%; /* 150px */
}
```


<br />
<br />


## `em`
- 기준 : 현재 요소 또는 상위 요소의 `font-size`

- 현재 요소의 `font-size`를 기준으로 계산된다.
  - 만약 `font-size`가 명시되지 않은 경우, 부모 요소의 `font-size`를 기준으로 한다.

- 계층적 상속의 영향을 받으므로, 부모 요소의 `font-size`가 증가하면 자식 요소의 크기도 증가한다.

```html
<body> <!-- font-size: 14px; -->
  <div class="outBox"> <!-- font-size: 1.2em; => font-size: 16.8px; -->

    <div class="inBox"> <!-- font-size: 1.2em; => font-size: 20.16px; -->
    </div>

  </div>
</body>
```
```css
body {
  font-size: 14px;
}

.outBox {
  font-size: 1.2em; /* 부모 요소 기준 - 14px * 1.2 = 16.8px */
  padding: 2em; /* 현재 요소 기준 - 16.8px * 2 = 33.6px */
}

.inBox {
  font-size: 1.2em; /* 부모 요소 기준 - 16.8px * 1.2 = 20.16px */
}
```


<br />
<br />


## `rem` (root em)
- 기준 : 루트 요소(`<html>`)의 `font-size`

- 요소의 `font-size`가 `<html>`의 `font-size`에 대해 상대적으로 계산된다.
  - `<html>`에 설정된 기본 `font-size`를 기준으로 하므로, 중첩된 요소에서도 계산이 일정하다.

- `<html>`에 `font-size` 미지정시 기본 크기인 16px로 지정된다.

```html
<body>
  <div class="outBox"> <!-- font-size: 1.2rem; => font-size: 19.2px; -->

    <div class="inBox"> <!-- font-size: 1.2rem; => font-size: 19.2px; -->
    </div>

  </div>
</body>
```
```css
.outBox {
  font-size: 1.2rem; /* 16px * 1.2 = 19.2px */
  padding: 2rem; /* 16px * 2 = 32px */
}

.inBox {
  font-size: 1.2rem; /* 16px * 1.2 = 19.2px */
}
```


<br />
<br />


## `vw` (Viewport Width), `vh` (Viewport Height)
- 뷰포트(브라우저)의 넓이 또는 높이를 기준으로 한다.
  - `1vw` = 뷰포트 넓이의 1/100
  - `1vh` = 뷰포트 높이의 1/100

- 주의점 : 100vw 지정시 스크롤바까지 넓이에 포함되므로 x축 스크롤이 생긴다.


<br />
<br />


## `vmin` (Viewport Minimum), `vmax` (Viewport Maximum)
- 뷰포트(브라우저)의 넓이 또는 높이를 기준으로 하는 최소, 최대 값

- 예제
  - 뷰포트 넓이 : 1200px, 뷰포트 높이 : 800px
    - `1vmin` = 8px, `1vmax` = 12px