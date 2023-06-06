---
layout: single
title: \[Main-Project\] TypeScript-React svg import 오류
categories: Team_project
tags: [project]
toc: true
toc_sticky: true
---

<br/>

# React + TypeScript에서 svg import 하는 방법

## `src/` 폴더 내에 `custom.d.ts` 파일을 생성한다.

```typescript
declare module "*.svg" {
  const content: any;
  export default content;
}
```

## tsconfig 파일을 수정해준다

```json
  "include": ["src", "src/custom.d.ts"]
```

## 이제 아래와 같이 svg를 import해 사용할 수 있다.

```tsx
import Battery from "assets/icons/battery.svg";
```

```tsx
<img src={Battery} alt='battery'>
```
