---
layout: single
title: \[Main-Project\] ScrollToTop 컴포넌트
categories: Team_Project
tags: [project]
---

<br/>

`React Router`의 `navigate`나 `Link`를 사용해 다른 페이지로 이동할 때, 이전 페이지에서 스크롤을 내려놓은 상태로 다른 페이지로 이동하면 스크롤 위치가 그대로 유지되며 페이지 중간부터 보인다.<br/>
그래서 페이지 주소가 바뀔 때 마다 스크롤 위치를 페이지 최상단으로 변경하는 컴포넌트를 작성했다.<br/>

```javascript
// src/utils/ScrollToTop
import { useEffect } from "react";
import { useLocation } from "react-router-dom";

export default function ScrollToTop() {
  const { pathname } = useLocation();

  useEffect(() => {
    window.scrollTo(0, 0);
  }, [pathname]);

  return null;
}
```

<br/>

이 컴포넌트는 `react-router-dom`의 `useLocation`을 사용하였기 때문에 `BrowserRouter`의 범위 내에서 호출해야 한다. 메인프로젝트에서는 `App.tsx`파일에 `BrowserRouter`를 사용했기 때문에 `App.tsx`내에서 `ScrollToTop` 컴포넌트를 호출해주었다.

![](/images/2023-03-07-scroll-to-top/1.png)
