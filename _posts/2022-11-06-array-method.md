---
layout: single
title: 배열 메서드 (Array Method)
---

### 배열 메서드

>배열은 사용 빈도가 높은 자료구조이므로 `배열 메서드`의 사용법을 잘 알아둘 필요가 있다.

>배열 메서드는 결과물을 반환하는 패턴이 두 가지이다.
>배열에는 **원본 배열을 직접 변경하는 메서드(mutator method)**와 **원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 메서드(accessor method)가 있다.**

<br/>

### 1) Array.isArray
>`Array.isArray` 메서드는 전달된 인수가 배열이면 `true`, 아니면 `false`를 반환한다.

```javascript
Array.isArray([]); // true
Array.isArray([1, 2, 3]); // true
Array.isArray(new Array()); // true

let arr = [1, 2, 3, 4, 5];

Array.isArray(arr); // true


Array.isArray(1); // false
Array.isArray({}); // false
Array.isArray('Array'); // false
```

<br/>

### 2) .indexOf
>`indexOf` 메서드는 원본 배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다.

>중복되는 여러 개의 요소가 있다면 첫번째로 검색된 요소의 인덱스를 반환한다.

>전달한 요소가 존재하지 않으면 -1을 반환한다.

```javascript
let arr = [1, 2, 2, 3];

arr.indexOf(2); // 1
arr.indexOf(4); // -1
arr.indexOf(2, 2); // 2
// 두 번째 인수는 검색을 시작할 인덱스다. 두 번째 인수를 생략하면 처음부터 검사한다.
```

`indexOf` 메서드를 사용해 배열에 특정 요소가 존재하는지 확인할 수 있다.
```javascript
let fruits = ['apple', 'banana', 'orange'];

if(fruits.indexOf('strawberry') === -1) {
  fruits.push('strawberry');
}

console.log(arr); // ['apple', 'banana', 'orange', 'strawberry']
```

<br/>

### 3) .icludes
>ES7에서 도입된 메서드이다. 원본 배열에서 인수로 전달된 요소를 검색하여 존재 여부를 `true`와 `false`로 반환한다.

```javascript
let fruits = ['apple', 'banana', 'orange'];

if(!fruits.includes('strawberry') {
  fruits.push('strawberry');
}

console.log(arr); // ['apple', 'banana', 'orange', 'strawberry']
```
<br/>

### 4) .push (mutator method)
>`push` 메서드는 인수로 전달받은 값을 **원본 배열의 `마지막 요소`로 추가하고 변경된 `length` 프로퍼티 값을 반환한다.**

>**`push` 메서드는 원본 배열을 직접 변경한다. (mutator method)**

```javascript
let arr = ['a', 'b'];

console.log(arr.push('c')); // 3
console.log(arr); // ['a', 'b', 'c']

console.log(arr.push('d', 'e')); // 5
console.log(arr) // ['a', 'b', 'c', 'd', 'e']
```
<br/>

>`push` 메서드는 성능 면에서 좋지 않다. 마지막에 추가할 요소가 하나 뿐이라면 `push` 메서드 대신 `length` 프로퍼티를 사용하여 직접 추가할 수도 있다. 이 방법이 더 빠르다.

```javascript
let arr = ['a', 'b'];

arr[arr.length] = 'c';
console.log(arr); // ['a', 'b', 'c']
```

<br/>

### 5) .pop (mutator method)
>`pop` 메서드는 원본 배열에서 **`마지막 요소`를 제거하고 `제거한 요소`를 반환한다.** 원본 배열이 빈 배열이면 `undefined`를 반환한다. `pop` 메서드는 원본 배열을 직접 변경한다.

>**`pop` 메서드는 원본 배열을 직접 변경한다. (mutator method)**

```javascript
let arr = [1, 2, 3];

console.log(arr.pop()); // 3
console.log(arr); // [1, 2]
```

<br/>

### 6) .unshift (mutator method)
>`unshift` 메서드는 인수로 전달받은 값을 **원본 배열의 `맨 앞`에 요소로 추가하고 변경된 `length` 프로퍼티 값을 반환한다.**

>**`unshift` 메서드는 원본 배열을 직접 변경한다. (mutator method)**

```javascript
let arr = [1, 2];

console.log(arr.unshift(0)); // 3
console.log(arr); // [0, 1, 2]
```

<br/>

### 7) .shift (mutator method)
>`shift` 메서드는 원본 배열에서 **`첫번째 요소`를 제거하고 제거한 요소를 반환한다.** 원본 배열이 빈 배열이면 `undefind`를 반환한다.

>**`shift` 메서드는 원본 배열을 직접 변경한다. (mutator method)**

```javascript
let arr = ['a', 'b', 'c'];

console.log(arr.shift()); // 'a'
console.log(arr); //['b', 'c']
```
<br/>

### 8) .concat (accessor method)
>**`concat` 메서드는 인수로 전달된 값들을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다.** 인수로 배열을 전달한 경우 배열을 해체하여 새로운 배열의 요소로 추가한다.

>**원본 배열은 변경되지 않는다. (accessor method)**

```javascript
let arr1 = [1, 2];
let arr2 = [3, 4];

let arr = arr1.concat(arr2);
console.log(arr); // [1, 2, 3, 4]

console.log(arr.concat(5)); // [1, 2, 3, 4, 5]
console.log(arr); // [1, 2, 3, 4]
```
<br/>

### 9) .splice (mutator method)
>원본 배열의 중간에 요소를 추가하거나 중간에 있는 요소를 제거하는 경우 `splice` 메서드를 사용한다.

>`splice` 메서드는 원본 배열을 직접 변경한다.

```javascript
let arr = [1, 2, 3, 4, 5];

console.log(arr.splice(1, 1)); // 2
console.log(arr); // [1, 3, 4, 5]

console.log(arr.splice(0, 2, 6)); // [1, 3]
console.log(arr); // [6, 4, 5]

console.log(arr.splice(0, 0, 1)); // []
console.log(arr); // [1, 6, 4, 5]
```
<br/>

### 10) .slice (accessor method)
>`slice` 메서드는 인수로 **전달된 범위의 요소들을 복사하여 배열로 반환한다.**

>**`slice` 메서드는 원본 배열을 변경하지 않는다. (accessor method)**

```javascript
let arr = [1, 2, 3, 4, 5];

console.log(arr.slice()); // [1, 2, 3, 4, 5]
console.log(arr.slice(0, 1)); // [1]
console.log(arr.slice(0, -1)); // [1, 2, 3, 4]
console.log(arr.slice(-2, -1)); // [4]

//원본 배열은 변경되지 않는다.
console.log(arr); // [1, 2, 3, 4, 5]
```

<br/>

### 11) .join
>`join` 메서드는 원본 배열의 모든 요소를 문자열로 변환한 후, 인수로 전달받은 문자열로 연결한 문자열을 반환한다. 구분자는 생략 가능하며 기본 구분자는 콤마(',')다.

```javascript
let arr = [1, 2, 3, 4];

console.log(arr.join()); // '1,2,3,4'
console.log(arr.join('-')); // '1-2-3-4'
console.log(arr.join('')); // '1234'
console.log(arr.join(':')); // '1:2:3:4'
```
<br/>

### 12) .reverse (mutator method)
>`reverse` 메서드는 원본 배열의 순서를 반대로 뒤집는다. 이 때 원본 배열이 변경된다.

```javascript
let arr = [1, 2, 3, 4];

console.log(arr.reverse()); // [4, 3, 2, 1]

//원본 배열이 변경된다
console.log(arr); // [4, 3, 2, 1]
```
<br/>

### 13) .fill (mutator method)
>`fill` 메서드는 인수로 전달받은 값을 배열의 요소로 채운다. 
>이 때 원본 배열이 변경된다.

```javascript
let arr = [1, 2, 3]

arr.fill(0);

console.log(arr); // [0, 0, 0]
```
>`두번째 인수`로 **요소를 채우기 시작할 인덱스**를, `세번째 요소`로 **요소 채우기를 멈출 인덱스**를 전달할 수 있다.

```javascript
let arr = [1, 2, 3]

arr.fill(0, 1);

console.log(arr); // [1, 0, 0]
```
```javascript
let arr = [1, 2, 3, 4, 5];

arr.fill(0, 1, 2);

console.log(arr); // [1, 0, 0, 4, 5]
```