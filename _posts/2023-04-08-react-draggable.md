---
layout: single
title: React Draggable 라이브러리 사용하기
categories: Notes
tags: [library, React]
toc: true
toc_sticky: true
---

<br/>

## 움직이는 컴포넌트를 만들고싶다!

프로필 페이지를 만드는 도중에 움직이는 윈도우 창같은 디자인을 만들고싶어 컴포넌트를 드래그할 수 있는 방법을 찾아보던 중<br/>
간단하게 드래그 가능한 컴포넌트를 구현할 수 있는 **`react-draggable`** 이라는 라이브러리를 발견해 사용해보았다.

## react-draggable 사용하기

### 설치

```zsh
npm install react-draggable
```

### 예제

```tsx
import Draggable from "react-draggable";
import { useRef } from "react";

const Terminal = () => {
  const dragRef = useRef<HTMLDivElement>(null);

  return (
    <Draggable nodeRef={dragRef}>
      <div className="container" ref={dragRef}>
        <div className="bar">bar</div>
      </div>
    </Draggable>
  );
};
```

`onDrag`, `onStart`, `onStop` 등의 이벤트도 있지만 나는 디자인, 애니메이션 등 없이 정말 윈도우 창처럼 움직여주기만 하면 됐기때문에 함수는 따로 작성하지 않고 `nodeRef` 속성만 먼저 추가해주었다.<br/>
드래그되길 원하는 엘리먼트에도 같은 `ref`를 설정해주어야 한다. 해당 코드만 작성해도 문제없이 컴포넌트는 잘 움직인다. 하지만...

![](/images/2023-04-08-react-draggable/1.gif)

![](/images/2023-04-08-react-draggable/2.gif)

나는 윈도우 창을 디자인하고싶었던 만큼 모든 부분이 아닌 회색 바 부분을 클릭하고 드래그했을때만 움직이길 원했고,<br/>
창 밖으로 컴포넌트가 벗어날 수 없도록 제어하고 싶었다.<br/>

## 속성

원하는 속성들을 추가하기 위해 [데모 예제](http://react-grid-layout.github.io/react-draggable/example/)와 [소스코드](https://github.com/react-grid-layout/react-draggable/blob/master/example/example.js)를 찾아봤는데 내가 원하는 속성도 찾았고, 그 외에도 x, y축중 한 방향으로만 드래그가 가능하다던지, 배경 요소를 벗어날 경우 스크롤이 생기게 한다던지 하는 다양한 속성들이 많이 있었다.<br/>
그치만 나는 내가 찾던 속성 두개만 추가하는걸로..

### 완성 코드

```tsx
import Draggable from "react-draggable";
import { useRef } from "react";

const Terminal = () => {
  const dragRef = useRef<HTMLDivElement>(null);

  return (
    <Draggable
      nodeRef={dragRef}
      handle=".bar" // "bar" class가 지정된 요소를 handle로 지정
      bounds="body" // body를 벗어나지 못하도록 설정
    >
      <div className="container" ref={dragRef}>
        <div className="bar">bar</div>
      </div>
    </Draggable>
  );
};
```

`handle` 속성에 `.bar`를 지정해 `bar` 클래스가 지정된 요소를 드래그했을때만 컴포넌트가 움직이도록 설정하고,<br/>
`bounds` 속성에 `body`를 주어 `body` 요소 밖으로 컴포넌트가 벗어나지 못하도록 했다.

![](/images/2023-04-08-react-draggable/3.gif)
(검은 부분 cursor 속성은 text로 따로 지정)

그럼 이렇게 회색 바 부분을 드래그할때만 움직이고, 창 밖으로 벗어나지 않는 컴포넌트를 만들 수 있다 😆
