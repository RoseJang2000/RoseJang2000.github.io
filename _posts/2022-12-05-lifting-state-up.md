---
layout: single
title: State 끌어올리기 (Lifting State Up)
tags: [React, state]
categories: React
---

<br/>

## 상태(State) 끌어올리기 (Lifting State Up)

단방향 데이터 흐름이라는 원칙에 따라 하위 컴포넌트는 상위 컴포넌트로부터 전달받은 데이터의 형태 혹은 타입이 무엇인지만 알 수 있다. 데이터가 state로부터 왔는지, 하드코딩으로 입력한 내용인지는 알지 못한다.<br/>

그러므로 하위 컴포넌트에서의 어떤 이벤트로 인해 상위 컴포넌트의 상태가 바뀌는 것은 마치 "역방향 데이터 흐름"과 같이 이상하게 들릴 수 있는데, React가 제시하는 해결책은 다음과 같다.<br/>

> 상위 컴포넌트의 "상태를 변경하는 함수" 그 자체를 하위 컴포넌트로 전달하고, 이 함수를 하위 컴포넌트가 실행한다.

여전히 단방향 데이터 흐름의 원칙에 부합하는 해결 방법이다. 이것을 "상태 끌어올리기"라고 한다.

<br/>

### 예제

예제 앱은 부모와 자식 컴포넌트가 하나씩 존재하는 트리 구조이다. 그리고, 상태를 변경시킬 수 있는 메서드가 존재한다고 생각할 때, 다음과 같은 구성을 가지게 될 것이다.<br/>

상태 변경 함수 `handleChangeValue`를 props로 부모 컴포넌트로부터 자식 컴포넌트에게 전달한다.

```javascript
import React, { useState } from "react";

export default function ParentComponent() {
  const [value, setValue] = useState("원래 값");
  
  const handleChangeValue = () => {
    setValue("달라진 값");
  }
  
  return (
  <div>
    <div>값은 {value} 입니다</div>
		<ChildComponent handleButtonClick={handleChangeValue} />
  </div>
  );
}
```

`<ChildComponent>`는 마치 고차 함수가 인자로 받은 함수를 실행하듯, props로 전달받은 함수를 컴포넌트에서 실행할 수 있게 된다.

```javascript
function ChildComponent({handleButtonClick}) {
  const handleClick = () => {
    handleButtonClick();
  }
  
  return (
  	<button onClick={handdleClick}>값 변경</button>
  )
}
```

필요에 따라 설정할 값을 콜백 함수의 인자로 넘길 수도 있다.

```javascript
function ParentComponent() {
  const [value, setValue] = useState("원래 값");

  const handleChangeValue = (newValue) => {
    setValue(newValue);
  };

  // ...생략...
}

function ChildComponent({ handleButtonClick }) {
  const handleClick = () => {
    handleButtonClick('자식 컴포넌트에서 바꾼 값')
  }

  return (
    <button onClick={handleClick}>값 변경</button>
  )
}
```

<br/>
