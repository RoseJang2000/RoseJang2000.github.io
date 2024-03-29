---
layout: single
title: 원시 값과 참조 값
tags: [JavaScript, type]
categories: JavaScript
toc: true
toc_sticky: true
---

> 자바스크립트가 제공하는 데이터 타입은 크게 `원시 타입(primitive type)`과 `참조 타입(reference type)`으로 구분할 수 있다.

<br/><hr/>

# 원시 타입 (primitive type)

## 원시 자료형

> `원시 값`, `원시 데이터 타입`은 객체가 아닌, 변수에 저장된 실제 값에 직접적으로 접근할 수 있는 단순한 데이터를 의미한다.

원시 타입에 해당하는 타입의 종류는 다음과 같다.

- Number
- String
- Boolean
- Null
- Undefined
- Biglnt
- Symbol
  <br/>

> `원시 값`을 `변수`에 할당하면 `변수`(확보된 메모리 공간)에는 `실제 값이 저장`된다.

```javascript
let a = 8;
let b;
b = "str";
```

<br/>

> `원시 값`은 `변경 불가능한 값(immutable value)`이다. 하지만 이것은 값에 대한 설명으로, `변수`에 값을 할당한 후 그것을 `재할당`하여 변수에 담긴 내용을 변경하는 것은 가능하다.

```javascript
let word = "hello world!";
word = "Hi there!";
/* 원시 값을 할당한 변수에 재할당하면 재할당 이전의 원시 값을 변경하는 것은 아니고, 
새로운 메모리 공간을 확보하고 재할당한 원시 값을 저장 후 변수가 새롭게 재할당한 값을 가리키는 것이다. */
```

> 변수의 상대개념인 상수는 재할당이 금지된 변수를 말한다. 변수는 언제든지 값을 변경할 수 있지만 상수는 단 한번만 할당이 가능하므로 변수 값을 변경할 수 없다.
> 하지만 상수와 변경 불가능한 값을 동일시 하는것은 곤란하다. 상수는 재할당이 금지된 변수일 뿐이다.

```javascript
const num1 = 123;
num1 = 456; // 에러 발생
```

<br/>

## 값 전달

> `원시 값`을 갖는 변수를 다른 변수에 할당하면 원본의 원시 값이 복사되어 전달된다.
> 말 그대로 `"값(value) 그대로" 저장, 할당되고 복사된다.`

```javascript
let a = 2;
let b;
b = a;

console.log(a, b); // 2 2
console.log(a === b); //true
```

> 이 때 변수 a와 b는 숫자 값 2를 갖는다는 점에서는 동일하다. 하지만 a와 b의 값 2는 `다른 메모리 공간`에 저장된 `별개의 값`이다.

<br/><br/><hr/>

# 참조 타입 (reference type)

## 참조 자료형

> `원시 값`을 할당한 변수는 `원시 값` 자체를 값으로 갖는다. 하지만 객체를 할당한 변수가 기억하는 메모리 주소를 통해 메모리 공간에 접근하면 **`참조 값(reference value)`** 에 접근할 수 있다.
> <br/> >`참조 값`은 `생성된 객체가 저장된 메모리 공간의 주소`이다.

> `참조 값`을 변수에 할당할 때는 `변수`에 값이 아닌 보관함의 `주소(reference)`를 저장한다.
> 그렇기 때문에 기존에 고정된 크기의 보관함이 아니라, 동적으로 크기가 변하는 특별한 보관함을 사용할 수 있다.

자바스크립트에서 원시 자료형이 아닌 모든 것은 참조 자료형이다. 아래 세 가지가 대표적인 참조 자료형이다.

- 배열 ([])
- 객체 ({})
- 함수(function(){})

<br/>

> 원시 값을 할당한 변수의 경우 "변수는 ~값을 갖는다"와 같이 표현하지만, 객체를 변수에 할당한 경우 "변수는 객체를 참조하고 있다" 또는 "변수는 객체를 가리키고 있다"라고 표현한다.

```javascript
let user = {
  name: 'John';
}

// user 변수는 객체 {name: 'John'}을 참조하고 있다.
```

> 원시 값은 `변경 불가능한 값`이므로 원시 값을 갖는 변수의 값을 변경하려면 재할당 밖에는 방법이 없다.
> 하지만 객체는 `변경 가능한 값`이기 때문에 객체를 할당한 변수는 재할당 없이 프로퍼티를 동적으로 추가하거나, 프로퍼티 값을 갱신하거나 프로퍼티를 삭제하는 등 객체를 직접 변경할 수 있다.

```javascript
// 프로퍼티 값 갱신
user.name = "Jack";

// 프로퍼티 동적 생성
user.age = 20;
user.adress = "Manhattan";

// 프로퍼티 삭제
delete user.adress;

console.log(user); // {name: 'Jack', age: 20}
```

<br/>

## 값 전달

> 원본 객체(배열)을 사본에 할당하면 원본의 참조 값을 복사해서 사본에 전달한다. 이 때 원본과 사본은 저장된 메모리 주소는 다르지만 동일한 참조 값을 갖는다.<br/>
> 원본과 사본이 모두 동일한 객체를 가르킨다. **두 개의 식별자가 하나의 객체(배열)을 공유한다**는 것을 의미한다.

> **따라서 원본 또는 사본 중 어느 한쪽에서 객체를 변경하면, 서로 영향을 주고받는다.**

```javascript
let colors = ["red", "green", "blue"];

let copy = colors;

copy.push("black");
colors.unshift("white");

console.log(colors); // ['white', 'red', 'green', 'blue', 'black']
console.log(copy); // ['white', 'red', 'green', 'blue', 'black']
```

<br/>

## 비교

> `=== 연산자`를 통해 `객체(배열)`등을 할당한 변수를 비교하면 `참조 값`을 비교하고, `원시 값`을 할당한 변수를 비교하면 `원시 값`을 비교한다.

```javascript
let user1 = { name: "John" };
let user2 = { name: "John" };

console.log(user1 === user2); // false
console.log(user1.name === user2.name); // true
```

> `user1`변수와 `user2`변수가 가리키는 객체는 내용은 같지만 다른 메모리에 저장된 별개의 객체이기 때문에 두 변수의 참조 값은 전혀 다른 값이다. 따라서 결과는 `false`이다.

> 하지만 `user1.name`과 `user2.name`은 프로퍼티 값을 참조하기 때문에 두 표현식 모두 원시 값 'John'으로 평가하여 결과는 `true`이다.
