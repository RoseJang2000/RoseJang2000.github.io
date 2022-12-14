---
layout: single
title: JSON.stringify(), JSON.parse()
tags: [JSON, method]
categories: JavaScript
---

<br/>

## π JSON.stringify()

### βΆοΈ JSON.stringify() λ?

> JavaScript κ°, κ°μ²΄ β JSON λ¬Έμμ΄λ‘ λ³ν

JSONμ μΌλ°μ μΈ μ©λλ μΉ μλ²μ λ°μ΄ν°λ₯Ό κ΅ννλ κ²μ΄λ€. μΉ μλ²μ λ°μ΄ν°λ₯Ό λ³΄λΌ λ λ°μ΄ν°λ λ¬Έμμ΄μ΄μ΄μΌ νλ―λ‘, `JSON.stringify()`λ₯Ό μ΄μ©νμ¬ κ°μ²΄λ₯Ό λ¬Έμμ΄λ‘ λ³ννλ€.<br/>

```js
JSON.stringify({ x: 5, y: 6 }); // '{"X":5,"y":6}'
JSON.stringify([3, 'false', false]) // '[3,"false",false]'
JSON.stringify(new Date(2006, 0, 2, 15, 4, 5)) // '"2006-01-02T06:04:05.000Z"'
```

<br/>

### βΆοΈ κ·μΉ

- λ°°μ΄μ΄ μλ κ°μ²΄μ μμ±λ€μ μ΄λ€ νΉμ ν μμμ λ°λΌ λ¬Έμμ΄ν λ  κ²μ΄λΌκ³  λ³΄μ₯λμ§ μλλ€. κ°μ κ°μ²΄μ λ¬Έμμ΄νμ μμ΄μ μμ±μ μμμ μμ‘΄νμ§ μλλ€.
- `Boolean`, `Number`, `String` κ°μ²΄λ€μ λ¬Έμμ΄ν λ  λ μ ν΅μ μΈ λ³ν μλ―Έμ λ°λΌ μ°κ΄λ κΈ°λ³Έν(primitive) κ°μΌλ‘ λ³κ²½λλ€.
- `undefined`, ν¨μ, μ¬λ³Ό(symbol)μ λ³νλ  λ μλ΅λκ±°λ(κ°μ²΄ μμ μμ κ²½μ°), `null`λ‘ λ³νλλ€(λ°°μ΄ μμ μμ κ²½μ°)
- μ¬λ³Όμ ν€λ‘ κ°μ§λ μμ±λ€μ `replacer` ν¨μλ₯Ό μ¬μ©νλλΌλ μμ ν λ¬΄μλλ€.
- μ΄κ±° λΆκ°λ₯ν μμ±λ€μ λ¬΄μλλ€.

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

### βΆοΈ μ§λ ¬ν (serialize)

```js
const message = {
  sender: "κΉμ½λ©",
  receiver: "λ°ν΄μ»€",
  message: "ν΄μ»€μΌ μ€λ μ λ κ°μ΄ λ¨Ήμλ?",
  createdAt: "2021-01-12 10:10:10"
}
```

```js
let transferableMessage = JSON.stringify(message)

console.log(transferableMessage) 
// '{"sender":"κΉμ½λ©","receiver":"λ°ν΄μ»€","message":"ν΄μ»€μΌ μ€λ μ λ κ°μ΄ λ¨Ήμλ?","createdAt":"2021-01-12 10:10:10"}'

console.log(typeof(transferableMessage))
// 'string'
```

> **stringify νλ μ΄ κ³Όμ μ μ§λ ¬ν(serialize)νλ€κ³  λ§νλ€.**

JSONμΌλ‘ λ³νλ κ°μ²΄μ νμμ **λ¬Έμμ΄**μ΄λ€. λ°μ μλ κ°μ²΄λ₯Ό μ§λ ¬ν ν λ¬Έμμ΄λ‘ λκ΅°κ°μκ² κ°μ²΄μ λ΄μ©μ λ³΄λΌ μ μλ€. κ·Έλ λ€λ©΄ μμ μλ μ΄ λ¬Έμμ΄ λ©μμ§λ₯Ό μ΄λ»κ² λ€μ κ°μ²΄μ ννλ‘ λ§λ€ μ μμκΉ? `JSON.stringify()`μ μ λ°λμ μμμ μννλ `JSON.parse()`λ₯Ό μ¬μ©ν  μ μλ€.

<br/>

## π JSON.parse()

> JSON λ¬Έμμ΄ β JavaScript κ°, κ°μ²΄λ‘ λ³ν

JSONμ μΌλ°μ μΈ μ©λλ μΉ μλ²μ λ°μ΄ν°λ₯Ό μ£Όκ³  λ°λ κ²μ΄λ€. μΉ μλ²μμ λ°μ΄ν°λ₯Ό μμ ν  λ λ°μ΄ν°λ ν­μ λ¬Έμμ΄μ΄λ€. κ°μ Έμ¨ λ°μ΄ν°λ₯Ό `JSON.parse()` λ©μλλ₯Ό μ¬μ©ν΄ JSON λ¬Έμμ΄μ κ΅¬λ¬Έμ λΆμνκ³ , κ·Έ κ²°κ³Όμμ JavaScript κ°μ΄λ κ°μ²΄λ₯Ό μμ±νλ€.

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

#### β νν μΌν μ¬μ© λΆκ°

```js
JSON.parse('[1, 2, 3, 4, ]');	//SyntaxError
JSON.parse('{"foo" : 1, }');	//SyntaxError
```

<br/>

## λ°μ΄ν° μ μ₯ μμ

#### ex: localStorageμ λ°μ΄ν° μ μ₯

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

[JSONκ³Ό λ©μλ](https://ko.javascript.info/json)

[W3Schools : JSON.stirngify](https://www.w3schools.com/js/js_json_stringify.asp)

[[JSON] JSON μ΄λ λ¬΄μμΈκ°? κ°λ¨ μ λ¦¬ λ° μμ λ₯Ό ν΅ν μ¬μ© λ°©λ²](https://codingazua.tistory.com/4)
