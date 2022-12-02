---
layout: single
title: React State & Props
tags: [React, state, props]
categories: React
---



## **학습 목표**

- state, props의 개념에 대해서 이해하고, 실제 프로젝트에 바르게 적용할 수 있다.
- React 함수 컴포넌트(React Function Component)에서 state hook을 이용하여 state를 정의 및 변경할 수 있다.
- React 컴포넌트(React Component)에 props를 전달할 수 있다.
- 이벤트 핸들러 함수를 만들고 React에서 이용할 수 있다.
- 실제 웹 애플리케이션의 컴포넌트를 보고 어떤 데이터가 state이고 props에 적합한지 판단할 수 있다.
- 실제 웹 애플리케이션 개발 시 적합한 state와 props의 위치를 스스로 정할 수 있다.
- React의 단방향 데이터 흐름(One-way data flow)에 대해 자신의 언어로 설명할 수 있다.
- JSX 문법의 기본과 컴포넌트 기반 개발에 대해서 숙지한다.
- React Router DOM으로 React에서 SPA(Single-Page Application)을 구현할 수 있다.
- state hook을 이용하여, 컴포넌트에서 데이터를 변화시킬 수 있다.
- props를 이용하여, 부모 컴포넌트의 데이터를 자식 컴포넌트로 전달할 수 있다.
- 바람직한 컴포넌트 구조와 state와 props의 위치에 대해 고민한다.

---

## State

- 살면서 변할 수 있는 값
- 컴포넌트 사용 중 컴포넌트 내부에서 변할 수 있는 값

## Props vs State

- props는 외부로부터 전달받은 값
- state는 내부에서 변화하는 값

### ex )

- 이름 → props
- 성별 → props
- 나이 → state
- 현재 사는 곳 → state
- 취업 여부 → state
- 결혼/연애 여부 → state

---

# Props

## Props의 특징

- 컴포넌트의 속성(property)을 의미한다.
  → 성별이나 이름처럼 변하지 않는 **외부로부터 전달받은 값**으로, 웹 애플리케이션에서 해당 컴포넌트가 가진 속성에 해당한다.
- 부모 컴포넌트(상위 컴포넌트)로부터 전달받은 값이다.
  React 컴포넌트는 JavaScript 함수와 클래스로, props를 함수의 전달인자처럼 전달받아 이를 기반으로 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환한다. 따라서, 컴포넌트가 최초 렌더링 될 때 화면에 출력하고자 하는 데이터를 담은 초기값으로 사용할 수 있다.
- **객체 형태**이다.
- props는 읽기 전용이다.
  성별이나 이름처럼 외부로부터 전달받아 변하지 않는 값이기 때문에 **함부로 변경될 수 없는 읽기 전용(read-only)객체**이다.

## How to use props

1. 하위 컴포넌트에 전달하고자 하는 값과 속성을 정의한다.
2. props를 이용하여 정의된 값과 속성을 전달한다.
3. 전달받은 props를 렌더링한다.

- 

```jsx
function Parent() {
  return (
    <div className="parent">
      <h1>I'm the parent</h1>
      <Child text={"I'm the eldest child"} />
			// Parent 컴포넌트에서 Child 컴포넌트에 props 전달
      <Child />
    </div>
  );
}

function Child(props) {
  console.log("props : ", props);
  return (
    <div className="child">
      <p>{props.text}</p>
			// 객체 props의 text 전달받기
    </div>
  );
}
```

- props.children

```jsx
unction Parent() {
  return (
    <div className="parent">
        <h1>I'm the parent</h1>
        <Child>I'm the eldest child</Child>
				// 여는 태그와 닫는 태그 사이에 value를 넣어 전달
    </div>
  );
};

function Child(props) {
  return (
    <div className="child">
        <p>{props.children}</p>
				// 전달받기 위해 props.children 사용
    </div>
  );
};
```

```jsx
const App = () => {
  const itemOne = "React를";
  const itemTwo = "배우고 있습니다.";

  return (
    <div className="App">
      <Learn>{`${itemOne} ${itemTwo}`}</Learn>
    </div>
  );
};

const Learn = (props) => {
  return <div className="Learn">{props.children}</div>;
};
```

# State

> 애플리케이션의 “상태”

→ Toggle switch, Counter처럼 컴포넌트 내부에서 변할 수 있는 값. 
ex) 쇼핑몰 장바구니 체크박스와 같이 **컴포넌트 내에서 변할 수 있는 값, 즉 상태는 React state로 다뤄야 한다.**

## useState

- `useState` 를 사용하기 위해서는 React로 부터 `useState`를 불러와야 한다.

```jsx
import { useState } from "react";
```

- 이후 `useState`를 컴포넌트 안해서 호출한다. `useState`를 호출한다는 것은 “state”라는 변수를 선언하는 것과 같으며, 변수의 이름은 임의로 지정 가능하다. 일반적인 변쑤는 함수가 끝날 때 사라지지만, state 변수는 React에 의해 함수가 끝나도 사라지지 않는다.

```jsx
const [state 저장 변수, state 갱신 함수] = useState(상태 초기 값);
```

```jsx
function CheckboxExample() {
	// 1 => useState의 리턴값을 구조 분해 할당
	const [isChecked, setIsChecked] = useState(false);
	
	// 1번 코드를 풀어 쓴 것
	const stateHookArray = useState(false);
	const isChecked = stateHookArray[0];
	const setIsChecked = stateHookArray[1];
}
```

1. `isChecked` : state를 저장하는 변수
2. `setIsChecked` : state `isChecked` 를 변경하는 함수
3. `useState` : state hook
4. `false` : state 초기 값

- 이 state 변수에 저장된 값을 사용하려면 JSX 엘리먼트 안에 직접 불러서 사용한다.

```jsx
<span>{isChecked ? "Checked!!" : "Unchecked" }</span>
```

## State 갱신하기

- state를 갱신하려면 state 변수를 갱신할 수 있는 함수인 `setIsChecked` 를 호출한다.

```jsx
const handleChecked = (event) => {
    setIsChecked(event.target.checked);
  };
```

## 주의점

- React 컴포넌트는 state가 변경되면 새롭게 호출되고, 리렌더링 된다.
- React state는 상태 변경 함수 호출로 변경해야 한다. 강제로 변경을 시도하면, 리렌더링이 되지 않는다거나 state가 제대로 변경되지 않는다.

