---
layout: single
title: \[Main-Project\] useWindowSize Hook
categories: Team_project
tags: [project]
toc: true
toc_sticky: true
---

<br/>

```typescript
import { useState, useEffect } from "react";

interface WindowSizeObj {
  windowWidth: number;
  windowHeight: number;
}

export const useWindowSize = (): WindowSizeObj => {
  const [windowSize, setWindowSize] = useState<WindowSizeObj>({
    windowWidth: window.innerWidth,
    windowHeight: window.innerHeight,
  });

  useEffect(() => {
    function handleResize() {
      setWindowSize({
        windowWidth: window.innerWidth,
        windowHeight: window.innerHeight,
      });
    }
    window.addEventListener("resize", handleResize);
    handleResize();
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return windowSize;
};
```
