---
layout: single
title: Effect Hook
tags: [React, Hook]
categories: React
toc: true
toc_sticky: true
---

<br/>

## 👉 React의 함수 컴포넌트

여태까지 학습한 React의 함수 컴포넌트는, props가 입력으로, JSX Element가 출력으로 나간다. 여기에는 그 어떤 Side Effect도 없으며, 순수 함수로 작동한다.

```jsx
function Singletweet({ writer, body, createdAt }) {
  return (
    <div>
      <div>{writer}</div>
      <div>{createdAt}</div>
      <div>{body}</div>
    </div>
  );
}
```

하지만 보통 React 애플리케이션을 작성할 때에는, AJAX 요청이 필요하거나 LocalStorage 또는 타이머와 같은 React와 상관 없는 API를 사용하는 경우가 발생할 수 있다. 이는 React의 입장에서는 전부 Side Effect이다. React는 Side Effect를 다루기 위한 Hook인 **Effect Hook**을 제공한다.

<br/>

### ▶️ React 컴포넌트에서의 Side Effect

- 타이머 사용 (setTimeout)
- 데이터 가져오기 (fetch API,localStorage)

<br/>

## 👉 Effect Hook

`useEffect`는 컴포넌트 내에서 Side Effect를 실행할 수 있게 하는 Hook이다.

```jsx
import React, { useState, useEffect } from "react";

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // 브라우저 API를 이용하여 문서 타이틀을 업데이트
    document.title = `You cliked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

위의 코드는 `useEffect`를 사용해 문서의 타이틀을 클릭 횟수가 포함된 문장으로 표현할 수 있도록 했다.<br/>

데이터 가져오기, 구독(subscription) 설정하기, 수동으로 React 컴포넌트의 DOM을 수정하는 것 까지 이 모든 것이 side effect이다.

<br/>

### ▶️ 언제 실행될까?

![001](/images/2022-12-06-c-effect-hook/001.png)

- 컴포넌트 생성 후 처음 화면에 렌더링(표시)
- 컴포넌트에 새로운 props가 전달되며 렌더링
- 컴포넌트의 상태(state)가 바뀌며 렌더링

이와 같이 매번 새롭게 컴포넌트가 **렌더링** 될 때 Effect Hook이 실행된다.

<br/>

### ▶️ Hook을 쓸 때 주의할 점

- #### **최상위에서만 Hook을 호출해야 한다.**

  **반복문, 조건문 혹은 중첩된 함수 내에서 Hook을 호출해선 안된다.** early return이 실행되기 전에 항상 React 함수의 최상위에서 Hook을 호출해야 한다. 이 규칙을 따르면 컴포넌트가 렌더링 될 때 마다 항상 동일한 순서로 Hook이 호출되는 것이 보장된다.
  이러한 점은 React가 `useState`와 `useEffect`가 여러 번 호출되는 중에도 Hook의 상태를 올바르게 유지할 수 있도록 해준다.

- #### 오직 React 함수 내에서 Hook을 호출해야 한다.

  **Hook을 일반적인 JavaScript 함수 내에서 호출해서는 안된다.** 대신 아래와 같이 호출할 수 있다.

  - React 함수 컴포넌트에서 Hook을 호출
  - Custom Hook에서 Hook을 호출

이 규칙을 지키면 컴포넌트의 모든 상태 관련 로직을 소스코드에서 명확하게 보이도록 할 수 있다.

<br/>

## 👉 조건부 effect 발생 (dependency array)

`useEffect`의 두번째 인자는 배열이다. 이 배열은 조건을 담고 있는데, 이때 조건은 `boolean` 형태의 표현식이 아닌 **어떤 값의 변경이 일어날 때**를 의미한다. 따라서, 해당 배열엔 **어떤 값**의 목록이 들어간다. 이 배열을 특별히 **종속성 배열 (dependency array)**이라고 부른다.<br/>

`useEffect`는 **화면에 첫 렌더링 될 때**, 그리고 **종속성 배열의 value 값이 바뀔 때**마다 실행된다.

<br/>

### 예제

```jsx
import { useEffect, useState } from "react";
import { getProverbs } from "./storageUtil";

export default function App() {
  const [proverbs, setProverbs] = useState([]);
  const [filter, setFilter] = useState("");
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("언제 effect 함수가 불릴까?");
    const result = getProverbs(filter);
    setProvervs(result);
  }, [filter]);

  const handleChange = (e) => {
    setFilter(e.target.value);
  };

  const handleCounterClick = () => {
    setCount(count + 1);
  };

  return (
    <div className="App">
      필터
      <input type="text" value={filter} onChange={handleChange} />
      <ul>
        {provervs.map((prvb, i) => (
          <Proverb saying={prvb} key={i} />
        ))}
      </ul>
    </div>
  );
}

function Proverb({ saying }) {
  return <li>{saying}</li>;
}
```

위 예제에는 다음과 같은 세 상태가 존재한다.

- 명언 목록 (`proverbs`)
- 필터링할 문자열 (`filter`)
- 카운트 (`count`)

위 예제는 `filter`가 변할 때에만 effect 함수가 실행된다. <br/>

카운트를 올리는 버튼은 컴포넌트의 상태가 바뀌고 업데이트 되지만, 아무리 버튼을 눌러도 effect 함수는 실행되지 않는다. 왜냐하면, 종속성 배열에는 `filter`만 존재하고 `count`는 존재하지 않기 때문이다.<br/>

#### ❓ 카운트 버튼을 눌렀을 때에도 effect 함수를 실행시키는 방법

```jsx
useEffect(() => {
  console.log("언제 effect 함수가 불릴까?");
  const result = getProverbs(filter);
  setProvervs(result);
}, [filter, count]);
```

useEffect의 **종속성 배열 (dependency array)**에 `count`를 추가해주면 `filter` 뿐만 아니라 `count`가 변경될 때에도 useEffect 함수가 실행된다.

<br/>

## 👉 단 한 번만 실행되는 Effect 함수

종속성 목록에 아무런 종속성도 없다면, 즉 두번째 인자인 종속성 배열을 **빈 배열** (`[]`)로 둘 경우에는 **컴포넌트가 처음 생성될 때만 effect 함수가 실행**된다.<br/>

이 경우는 두번째 인자를 아예 넘기지 않는 것과는 다르게 동작한다. 두번째 인자를 아예 넘기지 않은 경우에는 컴포넌트가 처음 생성되거나, props가 업데이트 되거나, state(상태)가 업데이트 될 때 effect 함수가 실행된다.

<br/>

### 예제

```jsx
useEffect(() => {
  console.log(몇 번 호출될까요?)
})
```

↳ ❌ 컴포넌트가 처음 생성되거나, state가 업데이트 될 때마다 실행된다.<br/>

```jsx
useEffect(() => {
  console.log(몇 번 호출될까요?)
}, [dep])
```

↳ ❌ `dep`이 업데이트 될 때마다 실행된다.<br/>

```jsx
useEffect(() => {
  console.log(몇 번 호출될까요?)
}, [])
```

↳ ✅ 컴포넌트가 처음 생성될 때만 함수가 실행된다.

<br/>
