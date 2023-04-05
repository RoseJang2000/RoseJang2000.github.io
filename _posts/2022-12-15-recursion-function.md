---
layout: single
title: 재귀 함수 (Recursion Function)
tags: [function, JavaScript]
categories: JavaScript
toc: true
toc_sticky: true
---

<br/>

# 재귀의 개념

## 재귀란 무엇일까?

> **재귀**: 원래의 자리로 되돌아가거나 되돌아옴.

재귀의 코드 예시

```js
function recursion() {
  console.log("This is");
  console.log("recursion!");
  recursion();
}
```

recursion 함수의 호출 결과

![001](/images/2022-12-15-recursion-function/001.png)

`recursion` 함수를 호출하자, 자기 자신을 끝없이 호출하며 같은 코드가 계속해서 실행된다. 이 `recursion` 함수처럼 자기 자신을 호출하는 함수를 재귀 함수라고 한다. 재귀 함수를 잘 활용하면 반복적인 작업을 해야하는 문제를 좀 더 간결한 코드로 풀어낼 수 있다.

<br/>

## 재귀로 문제 해결하기

```
문제: 자연수로 이루어진 배열을 입력받고, 리스트의 합을 리턴하는 함수 `arrSum`을 작성하라.
```

> 1. 문제를 좀 더 작게 쪼갠다.
> 2. 1번과 같은 방식으로, 문제가 더는 작아지지 않을 때 까지 가장 작은 단위로 문제를 쪼갠다.
> 3. 가장 작은 단위의 문제를 풂으로써 전체 문제를 해결한다.

#### 1. 문제를 작게 쪼개기

어떻게 `arrSum` 함수로 `[1, 2, 3, 4, 5]`의 합을 구하는 과정을 더 작게 쪼갤 수 있을까?<br/>

배열의 합을 구할 때 `[1, 2, 3, 4, 5]`의 합을 구하는 것보다 `[2, 3, 4, 5]`의 합을 구하는 것이 더 작은 문제이다.

```js
arrSum([1, 2, 3, 4, 5]) === 1 + arrSum([2, 3, 4, 5])
arrSum([2, 3, 4, 5]) === 2 + arrSum([3, 4, 5])
...
```

#### 2. 문제를 가장 작은 단위로 쪼개기

위에서 문제를 쪼갠 방식을 반복해서 계속 문제를 쪼개면 더이상 쪼갤 수 없는 상태에 도달한다.

```js
...
arrSum([3, 4, 5]) === 3 + arrSum([4, 5])
arrSum([4, 5]) === 4 + arrSum([5])
arrSum([5]) === 5 + arrSum([])
```

#### 3. 문제 해결하기

```js
function arrSum(arr) {
  // 빈 배열을 받았을 때 0을 리턴하는 조건문
  // 가장 작은 문제를 해결하는 코드 & 재귀를 멈추는 코드
  if (arr.length === 0) {
    return 0;
  }
  // 배열의 첫 요소 + 나머지 요소가 담긴 배열을 받는 arrSum 함수
  // 재귀를 통해 문제를 작게 쪼개나가는 코드
  return arr.shift() + arrSum(arr);
}
```

<br/>

## 재귀는 언제 사용하는 게 좋을까?

재귀는 다음과 같은 상황에서 매우 적합하다.

> 1. 주어진 문제를 비슷한 구조의 더 작은 문제로 나눌 수 있는 경우
> 2. 중첩된 반복문이 많거나 반복문의 중첩 횟수(number of loops)를 예측하기 어려운 경우

```js
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    for (let k = 0; k < n; k++) {
      for (let l = 0; l < n; l++) {
        for (let m = 0; m < n; m++) {
          for (let n = 0; n < n; n++) {
            for (let o = 0; o < n; o++) {
              for (let p = 0; p < n; p++) {
                // do something
                someFunc(i, j, k, l, m, n, o, p);
              }
            }
          }
        }
      }
    }
  }
}
```

모든 재귀 함수는 반복문으로 표현할 수 있다. 그러나 재귀를 적용할 수 있는 대부분의 경우에는, 재귀를 적용한 코드가 더욱 간결하고 이해하기 쉽다.

<br/>
