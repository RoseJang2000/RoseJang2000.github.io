---
layout: single
title: React Modal 부모 요소 스크롤 막기
categories: React
tags: [react]
toc: true
toc_sticky: true
---

<br/>

# Modal 부모요소 스크롤 막기

프로젝트를 진행하며 모달 창을 만들 일이 많았는데, 만들고 보니 모달 창이 열렸을 때 뒷 화면이 여전히 스크롤 가능한 부분이 거슬렸다. 내가 다른 사이트를 이용할 때는 모달 창이 열리면 보통 부모 요소는 스크롤이 비활성화 되었던 기억이 나서, 모달 창을 열었을 때 부모 요소의 스크롤을 비활성화 시키는 방법을 찾아보았다.

```typescript
useEffect(() => {
  document.body.style.cssText = `
    position: fixed; 
    top: -${window.scrollY}px;
    overflow-y: scroll;
    width: 100%;`;
  return () => {
    const scrollY = document.body.style.top;
    document.body.style.cssText = "";
    window.scrollTo(0, parseInt(scrollY || "0", 10) * -1);
  };
}, []);
```

`useEffect`를 사용해 `body`의 css를 변경해 컴포넌트가 마운트될 때 배경 요소의 스크롤을 방지하고, `return`문 내의 코드를 이용해 컴포넌트가 언마운트될 때 다시 `body`의 cssText를 초기화 한 후 현재 스크롤 위치로 이동시킨다.

<br/>

나는 메인 프로젝트에서 모달 창이 꽤 많이 사용되었기 때문에 코드를 재사용하기 위해서 위 코드를 컴포넌트로 따로 파일을 나눠준 뒤 import해서 사용하였다.

```tsx
import { useEffect } from "react";

const ModalScrollDisable = () => {
  useEffect(() => {
    document.body.style.cssText = `
    position: fixed; 
    top: -${window.scrollY}px;
    overflow-y: scroll;
    width: 100%;`;
    return () => {
      const scrollY = document.body.style.top;
      document.body.style.cssText = "";
      window.scrollTo(0, parseInt(scrollY || "0", 10) * -1);
    };
  }, []);
  return null;
};

export default ModalScrollDisable;
```

```tsx
import ModalScrollDisable from "utils/ModalScrollDisable";

const FollowModal = () => {
  return (
    <>
      <ModalScrollDisable />
      <ModalContent>
        <div>모달 내용~~~</div>
      </ModalContent>
    </>
  );
};

export default FollowModal;
```

위와 같이 사용해주면 `FollowModal`이 열릴 때는 배경 요소의 스크롤이 비활성화되고, `FollowModal`이 닫힐 경우 다시 스크롤이 활성화된다.
