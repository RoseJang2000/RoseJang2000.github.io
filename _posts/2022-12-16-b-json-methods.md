---
layout: single
title: JSON.stringify(), JSON.parse()
tags: [JSON, method]
categories: JavaScript
---

<br/>

## 👉 JSON.stringify()

### ▶️ JSON.stringify() 란?

> JavaScript 값, 객체 → JSON 문자열로 변환

JSON의 일반적인 용도는 웹 서버와 데이터를 교환하는 것이다. 웹 서버에 데이터를 보낼 때 데이터는 문자열이어야 하므로, `JSON.stringify()`를 이용하여 객체를 문자열로 변환한다.<br/>

```js
JSON.stringify({ x: 5, y: 6 }); // '{"X":5,"y":6}'
JSON.stringify([3, 'false', false]) // '[3,"false",false]'
JSON.stringify(new Date(2006, 0, 2, 15, 4, 5)) // '"2006-01-02T06:04:05.000Z"'
```

<br/>

### ▶️ 규칙

- 배열이 아닌 객체의 속성들은 어떤 특정한 순서에 따라 문자열화 될 것이라고 보장되지 않는다. 같은 객체의 문자열화에 있어서 속성의 순서에 의존하지 않는다.
- `Boolean`, `Number`, `String` 객체들은 문자열화 될 때 전통적인 변환 의미에 따라 연관된 기본형(primitive) 값으로 변경된다.
- `undefined`, 함수, 심볼(symbol)은 변환될 때 생략되거나(객체 안에 있을 경우), `null`로 변환된다(배열 안에 있을 경우)
- 심볼을 키로 가지는 속성들은 `replacer` 함수를 사용하더라도 완전히 무시된다.
- 열거 불가능한 속성들은 무시된다.

```js
JSON.stringify({});                  // '{}'
JSON.stringify(true);                // 'true'
JSON.stringify('foo');               // '"foo"'
JSON.stringify([1, 'false', false]); // '[1,"false",false]'
JSON.stringify({ x: 5 });            // '{"x":5}'

JSON.stringify(new Date(2006, 0, 2, 15, 4, 5))
// '"2006-01-02T15:04:05.000Z"'

JSON.stringify({ x: 5, y: 6 });
// '{"x":5,"y":6}' or '{"y":6,"x":5}'
JSON.stringify([new Number(1), new String('false'), new Boolean(false)]);
// '[1,"false",false]'

// Symbols:
JSON.stringify({ x: undefined, y: Object, z: Symbol('') });
// '{}'
JSON.stringify({ [Symbol('foo')]: 'foo' });
// '{}'
JSON.stringify({ [Symbol.for('foo')]: 'foo' }, [Symbol.for('foo')]);
// '{}'
JSON.stringify({ [Symbol.for('foo')]: 'foo' }, function(k, v) {
  if (typeof k === 'symbol') {
    return 'a symbol';
  }
});
// '{}'

// Non-enumerable properties:
JSON.stringify( Object.create(null, { x: { value: 'x', enumerable: false }, y: { value: 'y', enumerable: true } }) );
// '{"y":"y"}'
```

<br/>

### ▶️ 직렬화 (serialize)

```js
const message = {
  sender: "김코딩",
  receiver: "박해커",
  message: "해커야 오늘 저녁 같이 먹을래?",
  createdAt: "2021-01-12 10:10:10"
}
```

```js
let transferableMessage = JSON.stringify(message)

console.log(transferableMessage) 
// '{"sender":"김코딩","receiver":"박해커","message":"해커야 오늘 저녁 같이 먹을래?","createdAt":"2021-01-12 10:10:10"}'

console.log(typeof(transferableMessage))
// 'string'
```

> **stringify 하는 이 과정을 직렬화(serialize)한다고 말한다.**

JSON으로 변환된 객체의 타입은 **문자열**이다. 발신자는 객체를 직렬화 한 문자열로 누군가에게 객체의 내용을 보낼 수 있다. 그렇다면 수신자는 이 문자열 메시지를 어떻게 다시 객체의 형태로 만들 수 있을까? `JSON.stringify()`와 정반대의 작업을 수행하는 `JSON.parse()`를 사용할 수 있다.

<br/>

## 👉 JSON.parse()

> JSON 문자열 → JavaScript 값, 객체로 변환

JSON의 일반적인 용도는 웹 서버와 데이터를 주고 받는 것이다. 웹 서버에서 데이터를 수신할 때 데이터는 항상 문자열이다. 가져온 데이터를 `JSON.parse()` 메서드를 사용해 JSON 문자열의 구문을 분석하고, 그 결과에서 JavaScript 값이나 객체를 생성한다.

```js
const json = '{"result":true,"count":42}';
const obj = JSON.parse(json);

console.log(obj); // Object { result: true, count: 42}
console.log(obj.count);	// 42
console.log(obj.result);	// true
```

```js
JSON.parse('{}');              // {}
JSON.parse('true');            // true
JSON.parse('"foo"');           // "foo"
JSON.parse('[1, 5, "false"]'); // [1, 5, "false"]
JSON.parse('null');            // null
```

#### ❌ 후행 쉼표 사용 불가

```js
JSON.parse('[1, 2, 3, 4, ]');	//SyntaxError
JSON.parse('{"foo" : 1, }');	//SyntaxError
```

<br/>

## 데이터 저장 예시

#### ex: localStorage에 데이터 저장

```js
// Storing data:
const myObj = {name: "John", age: 31, city: "New York"};
const myJSON = JSON.stringify(myObj);
localStorage.setItem("testJSON", myJSON);

// Retrieving data:
let text = localStorage.getItem("testJSON");
let obj = JSON.parse(text);
document.getElementById("demo").innerHTML = obj.name;
```

<br/>

## Reference

[MDN](https://developer.mozilla.org/ko/) :  [JSON.stringify](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify), [JSON.parse()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)

[JSON과 메서드](https://ko.javascript.info/json)

[W3Schools : JSON.stirngify](https://www.w3schools.com/js/js_json_stringify.asp)

[[JSON] JSON 이란 무엇인가? 간단 정리 및 예제를 통한 사용 방법](https://codingazua.tistory.com/4)
