---
layout: single
title: React 이벤트 처리
tags: [React, event]
categories: React
toc: true
toc_sticky: true
---

# React 이벤트 처리

React의 이벤트 처리(이벤트 핸들링) 방식은 DOM의 이벤트 처리 방식과 유사하다. 단, 몇 가지 문법 차이가 있다.

- React에서 이벤트는 소문자 대신 카멜 케이스(camelCase)를 사용한다.
- JSX를 사용하여 문자열이 아닌 함수로 이벤트 처리 함수(이벤트 핸들러)를 전달한다.

Ex)

- HTML에서의 이벤트 처리 방식

```jsx
<button onclick="handdleEvent()">Event</button>
```

- React의 이벤트 처리 방식

```jsx
<button onClick={handleEvent}>Event</button>
```

## onChange

- `<input>`, `<textarea>`, `<select>` 와 같은 form 엘리먼트는 사용자의 입력 값을 제어하는 데 사용된다. React에서는 이런 **변경될 수 있는 입력 값**을 일반적으로 **컴포넌트의 state**로 관리하고 업데이트 한다.
- `onChange` 이벤트가 발생하면 `e.target.value` 를 통해 이벤트 객체에 담겨 있는 `input` 값을 읽어올 수 있다.

```jsx
function NameForm() {
  const [name, setName] = useState("");

  const hanndleChange = (e) => {
    setName(e.target.value);
  };

  return (
    <div>
      <input type="text" value={name} onChange={handdleChange}></input>
      <h1>{name}</h1>
    </div>
  );
}
```

## onClick

- `onClick` 이벤트는 말 그대로 사용자가 **click**이라는 행동을 하였을 때 발생하는 이벤트이다. `<a>` 태그를 통한 링크 이동 등과 같이 주로 사용자의 행동에 따라 애플리케이션이 반응해야 할 때 자주 사용하는 이벤트이다.

```jsx
function NameForm() {
  const [name, setName] = useState("");

  const hanndleChange = (e) => {
    setName(e.target.value);
  };

  return (
    <div>
      <input type="text" value={name} onChange={handdleChange}></input>
      <button onClick={() => alert(name)}>Button</button>
      <h1>{name}</h1>
    </div>
  );
}
```

> onClick 이벤트에 alert(name) 함수를 바로 호출하면 컴포넌트가 렌더링 될 때 함수 자체가 아닌 함수 호출의 결과가 onClick에 적용된다. 때문에 버튼을 클릭할 때가 아닌, 컴포넌트가 렌더링 될 때 alert가 실행되고 그 결과인 undefined가 적용되어 클릭 이벤트가 나타나지 않는다. 그래서 위와 같이 함수를 정의해야 한다.
