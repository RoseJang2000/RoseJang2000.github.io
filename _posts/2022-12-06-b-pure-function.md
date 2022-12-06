---
layout: single
title: 순수 함수(Pure Function)와 Side effect
tags: [JavaScript, function]
categories: JavaScript
---

<br/>

## 👉 Side Effect (부수 효과)

함수 내에서 어떤 구현이 함수 외부에 영향을 끼치는 경우, 해당 함수는 **Side Effect**가 있다고 이야기한다. <br/>

React에서는 컴포넌트 내에서 `fetch`를 사용해 API 정보를 가져오거나 이벤트를 활용해 DOM을 직접 조작할 때 **Side Effect**가 발생했다고 말한다.

<br/>

아래는 전역변수 `foo`를 `bar`라는 함수를 수정하는 예제이다.

```javascript
let foo = 'hello';

function bar() {
  foo = 'world';
}

bar();	// bar는 Side Effect를 발생시킨다.
```

<br/>

## 👉 Pure Function (순수 함수)

###  🧐 순수 함수란?

> 순수함수란, 오직 함수의 입력만이 함수의 결과에 영향을 주는 함수를 의미한다. 
>

- 함수의 입력이 아닌 다른 값이 함수의 결과에 영향을 미치는 경우, 순수 함수라고 부를 수 없다.
- 순수 함수는 입력으로 전달 된 값을 해치지 않는다.
- 같은 입력에 대해 같은 결과를 return한다.
- 함수 외부의 데이터나 함수에 전달된 데이터를 변경하지 않는다. 
  (Side Effect를 초래하지 않는다. 즉, 어떠한 외부 상태도 변환하지 않는다.)

<br/>

```javascript
function Upper(str) {
  return str.toUpperCase(); // toUpperCase 메서드는 원본을 수정하지 않는다. (Immutable)
}

upper('hello');	//'HELLO'
```

**순수 함수**에는 네트워크 요청과 같은 Side Effect가 없다. **순수 함수**의 특징 중 하나는, 어떠한 전달 인자가 주어질 경우 항상 똑같은 값이 리턴됨을 보장한다는 것이다. 그래서 예측 가능한 함수이기도 하다.

<br/>

### ❓ Question

> `Math.random()`은 순수 함수가 아니다. 그 이유는 무엇일까?

**순수 함수**의 특징 중 하나는, 같은 입력 값이 들어왔을 때, **항상 같은 출력 값이 나온다**는 것이다.

예를 들어 아래와 같은 함수를 정의했다고 생각해 보자.

```javascript
const double = x => x * 2;
```

위에서 정의된  `double` 함수는 순수 함수이다. `double(5)`는 얼마나 많이 호출하든 상관 없이 언제나 `10`이라는 동일한 결과를 출력할 것이다. 하지만 `Math.random()`의 경우에는 다르다.

```javascript
Math.random(); // => 0.4011148700956255
Math.random(); // => 0.8533405303023756
Math.random(); // => 0.3550692005082965
```

함수를 호출할 때 아무런 인자를 넘기지 않은 동일한 형태로 여러 번 호출했음에도 불구하고, 매번 다른 출력 값을 만들어낸다. 이것은 `Math.random()`함수가 순수하지 않다는 것을 의미한다.

<br/>

> 어떤 함수가 fetch API를 이용해 AJAX 요청을 한다고 가정했을 때, 이 함수는 순수 함수가 아니다. 그 이유는 무엇일까?

네트워크 통신이 이루어지는 것이기 때문에, 네트워크의 상황이나 서버 상태에 따라 응답 코드가 달라지고 따라서 **예측이 불가능하다.** 그렇기 때문에 순수 함수라고 말할 수 없다.

<br/>

### ➕ 추가로 알아둘 내용

- 순수 함수를 이용하여 구현할 수 있는 프로그램이라면, 순수 함수를 사용하는 것을 권장한다.
  순수 함수는 독립성이 있고, 리팩토링 하거나 다시 재구성하기도 쉽다.
- 순수함수는 함수 body 내에 있는 코드만 점검하면 되기 때문에 간결하게 코드를 작성하고 사고하는데 도움이 된다.
- 함수에 return 값이 존재하지 않는다는 것은 Side Effect를 유발한다는 것을 나타낸다.

<br/>

<hr/>

### Reference

- [자바스크립트 개발자라면 알아야 할 33가지 개념 #20 자바스크립트 : 순수함수](https://velog.io/@jakeseo_me/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%9D%BC%EB%A9%B4-%EC%95%8C%EC%95%84%EC%95%BC-%ED%95%A0-33%EA%B0%80%EC%A7%80-%EA%B0%9C%EB%85%90-20-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%88%9C%EC%88%98%ED%95%A8%EC%88%98)
- [Pure functions in JavaScript](https://www.nicoespeon.com/en/2015/01/pure-functions-javascript/)
- [Master the JavaScript Interview: What is a Pure Function?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976)

<br/>
