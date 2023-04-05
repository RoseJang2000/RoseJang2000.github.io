---
layout: single
title: 고차 함수 (Higher-order function)
tags: [JavaScript, higher-order function]
categories: JavaScript
toc: true
toc_sticky: true
---

<hr/>
<br/>

# 👉 일급 객체

- **일급 객체(first-class object)**란 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가리킨다. 보통 함수에 인자로 넘기기, 수정하기, 변수에 대입하기와 같은 연산을 지원할 때 일급 객체라고 한다.

- 다음과 같은 조건을 만족하는 객체를 일급 객체라 한다.
  > 1.  무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
  > 2.  변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
  > 3.  함수의 매개변수에 전달할 수 있다.
  > 4.  함수의 반환값으로 사용할 수 있다.
- _자바스크립트의 **함수**는 위의 조건을 모두 만족하므로 일급 객체다._

<br/>

# 👉 콜백 함수

```javascript
function repeat(n, f) {
  // 경우에 따라 변경되는 일을 f로 추상화, 외부에서 전달 받음
  for (let i = 0; i < n; i++) {
    f(i); // i 전달, f 호출
  }
}

let logAll = (i) => {
  console.log(i);
};

repeat(5, logAll); // 0 1 2 3 4

let logOdds = (i) => {
  if (i % 2) console.log(i);
};

repeat(5, logOdds); // 1 3
```

- repeat 함수는 내부 로직에 강력히 의존하지 않고 외부에서 로직의 일부분을 함수로 전달받아 수행하므로 더욱 유연한 구조를 가진다.

> 이처럼 **함수의 매개변수를 통해 다른 함수 내부로 전달되는 함수를 `콜백 함수(callback function)`라고 하며, 매개변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 `고차 함수(Higher-Order Function)`라고 한다.**

<br/>

# 👉 고차 함수

> **고차 함수**는 함수를 전달인자로 받거나 함수를 리턴하는 함수를 말한다.

- 자바스크립트의 함수는 일급 객체이므로 함수를 값처럼 인수로 전달할 수 있으며 리턴할 수도 있다.
- 고차 함수는 외부 상태의 변경이나 가변 데이터를 피하고 **불변성을 지향**하는 함수형 프로그래밍에 기반을 두고 있다.
- 함수형 프로그래밍은 **순수 함수를 통해 부수 효과를 최대한 억제**하여 오류를 피하고 프로그램의 안정성을 높이려는 노력의 일환이다.

<br/>

## ✔️ 내장 고차 함수

### ▶️ Array.prototype.sort

>

- `sort` 메서드는 배열의 요소를 정렬한다. **원본 배열을 직접 변경**하며 정렬된 배열을 반환한다.
- `sort` 메서드는 기본적으로 오름차순으로 요소를 정렬한다.

* 문자열을 정렬 할 경우 의도한 대로 잘 작동한다.

```javascript
const alpha = ["b", "d", "a", "e", "c"];

alpha.sort();
console.log(alpha); // ['a', 'b', 'c', 'd', 'e']
```

- 숫자 요소의 경우, 유니코드 코드 포인트의 순서를 따르기 때문에 의도한 대로 정렬이 이루어지지 않을 수 있다.

```javascript
let num = [40, 100, 1, 5, 2, 25, 10];

num.sort();
console.log(num); // [1, 10, 100, 2, 25, 40, 5]
```

- 따라서 숫자 요소를 정렬할 때는 `sort` 메서드에 **정렬 순서를 정의하는 비교 함수를 인수로 전달**해야 한다.

```javascript
let num = [40, 100, 1, 5, 2, 25, 10];

num.sort((a, b) => a - b);
console.log(num); // [1, 2, 5, 10, 25, 40, 100]
```

> 비교 함수는 양수나 음수 또는 0을 반환해야 한다. 리턴 값이 음수일 경우 비교 함수의 첫번째 인자를 우선으로 정렬하고, 양수일 경우 두번째 인수를 우선하여 정렬한다.

<br/>

### ▶️ Array.prototype.forEach

> - `forEach` 메서드는 `for`문을 대체할 수 있는 고차 함수다.

- `forEach` 메서드는 반복문을 추상화한 고차 함수로서 내부에서 반복문을 통해 자신을 호출한 배열을 순회하며 수행해야 할 일을 콜백 함수로 전달받아 반복 호출한다.

* `for`문 사용

```javascript
const num = [1, 2, 3];
const result = [];

for (let i = 0; i < num.length; i++) {
  result.push(num[i] ** 2);
}
console.log(result); // [1, 4, 9]
```

- `forEach`문 사용

```javascript
const num = [1, 2, 3];
const result = [];

num.forEach((el) => result.push(el ** 2));
console.log(result); // [1, 4, 9]
```

<br/>

### ▶️ Array.prototype.map

> `map` 메서드는 자신을 호출한 배열의 모든 요소를 순회하며 인수로 전달받은 콜백 함수를 반복 호출하고, **콜백 함수의 반환값들로 구성된 새로운 배열을 반환**한다.

```javascript
const num = [1, 2, 3];

const add1 = num.map((el) => el + 1);
const mul2 = num.map((el) => el * 2);

console.log(add1); // [2, 3, 4]
console.log(mul2); // [2, 4, 6]
```

```javascript
const user = [
  { name: "John", age: 30 },
  { name: "Cely", age: 20 },
  { name: "Michael", age: 45 },
];

const userName = user.map((el) => el.name);
console.log(userName); // ['John', 'Cely', 'Michael']
```

<br/>

### ▶️ Array.prototype.filter

> `filter` 메서드는 자신이 호출한 배열의 모든 요소를 순회하며 콜백 함수를 반복 호출하고, **콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 리턴한다.**

```javascript
const num = [1, 2, 3, 4, 5];

const odds = num.filter((el) => el % 2);
console.log(odds); // [1, 3, 5]
```

```javascript
const user = [
  { name: "John", age: 30 },
  { name: "Cely", age: 20 },
  { name: "Michael", age: 45 },
];

const legalDrinking = user.filer((el) => el >= 21);
console.log(legalDrinking); //	['John', 'Michael']
```

<br/>

### ▶️ Array.prototype.reduce

> `reduce` 메서드는 콜백 함수의 반환 값을 다음 순회 시 콜백 함수의 첫번째 인수로 전달하면서 콜백 함수를 호출하여 **하나의 결과값을 만들어 반환한다.**

- 배열 값들의 합

```javascript
const num = [1, 2, 3, 4, 5];

const sum = num.reduce((acc, cur) => acc + cur);
console.log(sum); // 15
```

- 배열 값들 중 최댓값

```javascript
const num = [1, 2, 3, 4, 5];

const max = num.reduce((acc, cur) => (acc > cur ? acc : cur));
console.log(max); // 5
```

<br/>
