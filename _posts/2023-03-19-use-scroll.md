---
layout: single
title: \[Main-Project\] useScroll Hook
categories: Team_Project
tags: [project]
---

<br/>

메인 프로젝트에서 구현을 맡게된 페이지중에 메인페이지가 있다. 메인페이지는 서비스 소개와 페이지 이동 정도의 컨텐츠를 가지고 있는데, 그중 서비스 소개 부분에는 스크롤 애니메이션 이벤트를 사용할 예정이었기 때문에 스크롤 위치를 측정해줄 `useScroll` hook을 작성했다.
<br/>

```javascript
import { useState, useEffect } from "react";

export const useScroll = () => {
  const [scrollY, setScrollY] = useState(window.scrollY);

  const onScroll = () => {
    setScrollY(window.scrollY);
  };

  useEffect(() => {
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  }, []);

  return scrollY;
};
```

찾아본 예시에는 X축 스크롤까지 계산하는 예시들이 많았지만 나는 Y축 스크롤만 필요할 것 같아 Y축 스크롤만을 측정해주도록 코드를 작성했다.
<br/>

아래와 같이 불러온 후 스크롤에 따른 클래스명을 부여해 애니메이션 효과를 사용했다.

![](/images/2023-03-19-use-scroll/1.png)
![](/images/2023-03-19-use-scroll/2.png)
