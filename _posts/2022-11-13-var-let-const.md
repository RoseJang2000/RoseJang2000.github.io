---
layout: single
title: var, let, const
tags: [JavaScript]
categories: JavaScript
toc: true
toc_sticky: true
---

# var 키워드

> ES5까지는 변수를 선언할 수 있는 유일한 키워드였지만, 여러 단점이 있어 **`ES6`부터는 사용을 지양한다.**

## 특징

### - 변수의 중복선언 허용

> `var` 키워드로 선언한 변수는 `중복 선언`이 가능하다.

```javascript
var a = 10;
var b = 1;

var a = 20;
var b;

console.log(a); // 20
console.log(b); // 1
```

> 위와 같이 만약 동일한 이름의 변수가 이미 선언되어 있는 걸 모르고 변수를 `중복 선언` 하며 값까지 할당한다면 **먼저 선언된 함수의 값이 변경되는 문제가 발생한다.**

<br/>

### - 함수 레벨 스코프

> `var` 키워드로 선언한 변수는 `함수의 코드블록`만을 지역 스코프로 인정한다. 따라서 함수 외에 다른 코드블록 내에서 var 키워드로 변수를 선언해도 모두 전역 변수가 된다.

```javascript
var x = 1;

if (true) {
  var x = 10;
}

console.log(x); // 10
```

```javascript
var i = 10;

for (var i = 0; i < 5; i++) {
  console.log(i);
}

console.log(i); // 5
```

> 이로 인해 의도치 않게 변수가 중복 선언되는 경우가 발생한다.

<br/>

### - 변수 호이스팅

> var 키워드로 변수를 선언하면 변수 호이스팅에 의해 변수 선언문이 스코프의 선두로 끌어올려진 것 처럼 동작한다.

> 변수 `호이스팅`에 의해 var 키워드로 선언한 변수는 변수 선언문 이전에 참조할 수 있다. 단, **할당문 이전에 변수를 참조하면 언제나 `undefined`를 반환한다.**

```javascript
console.log(x); // undefined

x = 10;

console.log(x); // 10

var x;
```

> 변수 선언문 이전에 변수를 참조하면 호이스팅에 의해 에러는 발생하지 않지만, 프로그램의 흐름에 맞지 않고 문제를 발생시킬 여지를 남긴다.

<br/>

### - 전역객체

> var 키워드로 선언한 전역 변수와 전역 함수, 그리고 선언하지 않은 변수에 값을 할당한 암묵적 전역은 window 객체의 프로퍼티가 된다.

```javascript
var a = 1;
b = 2;

console.log(window.a); // 1
console.log(1); // 1

console.log(window.b); // 2
console.log(b); // 2
```

<br/><br/>

# let 키워드

> ES6에서 도입된 새로운 변수 선언 키워드이다.

## 특징

### - 변수 중복 선언 금지

> var 키워드와 다르게 `let` 키워드는 이름이 같은 변수를 `중복 선언`하면 `문법 에러`가 발생한다.
> 따라서 의도치 않게 먼저 선언된 변수 값이 재할당되는 부작용을 막을 수 있다.

```javascript
let a = 1;

let a = 10; // SyntaxError: Identifier 'a' has already been declared
```

<br/>

### - 블록 레벨 스코프

> `let` 키워드로 선언한 변수는 `모든 코드 블록`을 지역 스코프로 인정하는 `블록 레벨 스코프`를 따른다.

```javascript
let a = 1; // 전역 변수

{
  let a = 10; // 지역 변수
  let b = 2; // 지역 변수
}

console.log(a); // 1
console.log(b); // ReferenceError: b is not defined
```

<br/>

### - 변수 호이스팅

> let 키워드로 선언한 변수는 호이스팅이 발생하지 않는 것 처럼 동작한다.

```javascript
console.log(a); // ReferenceError: a is not defined

let a;
```

<br/>

> `var` 키워드는 암묵적으로 `선언 단계`와 `초기화 단`계가 **동시에** 진행되는 반면에, `let` 키워드로 선언한 변수는 **`선언 단계`와 `초기화 단계`가 분리되어 진행된다.**
>
> 자바스크립트 엔진에 의해 런타임 이전에 선언단계가 실행되지만, **초기화 단계는 변수 선언문에 도달해야 실행된다.**

> 초기화 단계 실행 이전에 변수에 접근한다면 참조 에러가 발생한다.

```javascript
console.log(a); // ReferenceError: a is not defined

let a; // 변수 선언문에 도달해야 초기화 단계가 실행된다.
console.log(a); // undefined

a = 1; // 할당문에서 할당 단계가 실행된다.
console.log(a); // 1
```

> **`let` 키워드로 선언한 변수는 `스코프의 시작 지점`부터 초기화 단계 시작 지점(`변수 선언문`)까지 변수를 참조할 수 없다.** 이 구간을 **`일시적 사각지대(TDZ: Temporal Dead Zone)`**라고 부른다.

<br/>

> 자바스크립트는 모든 선언을 호이스팅 한다. 하지만 ES6에서 도입된 `let`, `const`, `class`를 사용한 선언문은 호이스팅이 발생하지 않는 것 처럼 동작한다.

<br/>

### - 전역객체

> `let` 키워드로 선언한 `전역 변수`는 전역 객체의 프로퍼티가 아니다.
> 즉, `window.a` 와 같이 접근할 수 없다. let 전역 변수는 보이지 않는 `개념적인 블록` 내에 존재하게 된다.

```javascript
var x = 1;
y = 2;
let z = 3;

console.log(window.x); // 1
console.log(x); // 1

console.log(window.y); // 2
console.log(y); // 2

console.log(window.z); // undefined
console.log(z); // 3
```

<br/><br/>

# const 키워드

> `const` 키워드는 `상수`를 선언하기 위해 사용한다.

## 특징

> `호이스팅`, `전역객체`, `블록 레벨 스코프` 등 대부분의 특징은 `let` 키워드와 동일하므로 다른 특징에 대해서 작성한다.

### - 선언과 초기화

> **`const` 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다.**

```javascript
const a = 1;

const b;	// SyntaxEror: Missing initializer in const declaration
```

> `const` 키워드로 선언한 변수는 `let` 키워드로 선언한 변수와 마찬가지로 `블록 레벨 스코프`를 가지며, 호이스팅이 발생하지 않는 것 처럼 동작한다.

```javascript
{
  console.log(a); // ReferenceError: Cannot access 'a' before initialization
  const a = 1;
  console.log(a); // 1
}

console.log(a); // ReferenceError: a is not defined
```

<br/>

### - 재할당 금지

> `var` 또는 `let` 키워드로 선언한 변수는 재할당이 자유롭지만,
> **`const` 키워드로 선언한 변수는 재할당이 금지된다.**

```javascript
const a = 1;
a = 2; // TypeError
```

<br/>

### - const와 객체

> `const` 키워드로 선언된 변수에 원시 값을 할당할 경우 값을 변경할 수 없다. 하지만 **`const` 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경할 수 있다.** 객체는 재할당 없이도 직접 변경이 가능하기 때문이다.

```javascript
const user = {
  name: 'John';
}

user.name = 'Tom';

console.log(user);	// {name: 'Tom'}
```

> **`const` 키워드는 재할당을 금지할 뿐 '불변'을 의미하진 않는다.**
> 새로운 값을 재할당 하는 것은 불가능하지만 프로퍼티 동적 생성, 삭제, 프로퍼티 값의 변경을 통해 객체를 변경하는 것은 가능하다.

<br/><br/>

# var, let, const

> 변수 선언에는 기본적으로 `const`를 사용하고 `let`은 재할당이 필요한 경우에 한정해 사용하는 것이 좋다. const 키워드를 사용하면 의도치 않은 재할당을 방지하기 때문에 더 안전하다.

- ES6 이후 `var` 키워드는 권장하지 않는다.
- 재할당이 필요한 경우에 한정해 `let` 키워드를 사용한다. 변수의 스코프는 최대한 좁게 만든다.

> 일단 최대한 `const` 키워드를 사용하고, 반드시 재할당이 필요하다면 그 때 `let`으로 변경해도 늦지 않다.
