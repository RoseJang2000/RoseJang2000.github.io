---
layout: single
title: 시간 복잡도 (Time complexity)
categories: Algorithm
tags: [algorithm, time complexity]
---

<br/>

# Algorithm

## 알고리즘 이란?

알고리즘은 **어떤 문제를 해결하기 위해서 일련의 절차를 정의하고, 공식화한 형태로 표현한 일종의 문제 풀이 방법, 해**를 의미한다. 이런 알고리즘은 **프로그래밍에서는 input 값을 통해 output 값을 얻기 위한 계산 과정**을 의미한다.
주어진 문제를 해결할 때, 정확하고 효율적으로 값을 얻는 것이 필요하고 그때 바로 이 알고리즘이 사용된다. 문제 해결을 위한 단계들을 체계적으로 명시할 수 있는 상황이라면 그것은 알고리즘으로 충분히 풀어낼 수 있다고 볼 수 있다.

<br/>

# 시간 복잡도와 공간 복잡도

## 시간 복잡도 (Time Complexity)

![time complexity glaph](https://s3.ap-northeast-2.amazonaws.com/urclass-images/2joMl6zhB-1614944522453.png)

문제를 해결하기 위해 알고리즘의 로직을 코드로 구현할 때, 시간 복잡도를 고려한다는 것은 다음과 같은 의미이다.

> 입력값의 변화에 따라 연산을 실행할 때, 연산 횟수에 비해 시간이 얼만큼 걸리는가?

효율적인 알고리즘을 구현한다는 것은 바꾸어 말해 **입력값이 커짐에 따라 증가하는 시간의 비율을 최소화한 알고리즘**을 구성했다는 이야기이다. 그리고 이 시간복잡도는 주로 `빅-오 표기법`을 이용해 나타낸다.

### Big-O 표기법

<hr/>

시간 복잡도를 표기하는 방법은 다음과 같다.

- **Big-O**(빅-오)
- Big-Ω(빅-오메가)
- Big-θ(빅-세타)

위 세 가진 표기법은 시간 복잡도를 각각 최악, 최선, 중간(평균)의 경우에 대하여 나타내는 방법이다. 이 중에서 Big-O 표기법이 가장 자주 사용된다. 빅오 표기벅은 최악의 경우를 고려하므오, 프로그램이 실행되는 과정에서 소요되는 최악의 시간까지 고려할 수 있기 때문이다. `"최소한 특정 시간이 걸린다"` 혹은 `"이 정도 시간이 걸린다"`를 고려하는 것 보다 `"이 정도 시간까지 걸릴 수 있다"`를 고려해야 그에 맞는 대응이 가능하다.

#### O(1)

![시간 복잡도가 O(1)인 경우](https://s3.ap-northeast-2.amazonaws.com/urclass-images/xege67hpX-1614944829474.png)

Big-O 표기법은 `입력값의 변화에 따라 연산을 실행할 때, 연산 횟수에 비해 시간이 얼마만큼 걸리는가?`를 표시하는 방법이다. O(1)는 constant complexity라고 하며, 입력값이 증가하더라도 시간이 늘어나지 않는다. 다시 말해 입력 값의 크기와 관계 없이, 즉시 출력 값을 얻어낼 수 있다는 의미이다. O(1)의 시간 복잡도를 가진 알고리즘은 아래와 같다.

```javascript
function O_1_algorithm(arr, index) {
  return arr[index];
}

let arr = [1, 2, 3, 4, 5];
let index = 1;
let result = O_1_algorithm(arr, index);
console.log(result); // 2
```

위 알고리즘에선 입력값의 크기가 아무리 커져도 즉시 출력값을 얻어낼 수 있다.<br/>

#### O(n)

![시간 복잡도가 O(n)인 경우](https://s3.ap-northeast-2.amazonaws.com/urclass-images/wl87JX_j0-1614944852768.png)

O(n)은 linear comlexity라고 부르며, 입력 값이 증가함에 따라 시간 또한 `같은 비율`로 증가하는 것을 의미한다. 예를 들어 입력 값이 1일 때 1초의 시간이 걸리고, 입력 값을 100배로 증가시켰을 때 1초의 100배인 100초가 걸리는 알고리즘을 구현한다면, 그 알고리즘은 O(n)의 시간 복잡도를 가진다고 할 수 있다. O(n)의 시간 복잡도를 가진 알고리즘은 아래와 같다.

```javascript
function O_n_algorithm(n) {
  for (let i = 0; i < n; i++) {
    // do something for 1 second
  }
}

function another_O_n_algorithm(n) {
  for (let i = 0; i < 2n; i++) {
    // do something for 1 second
  }
}
```

`O_n_algorithm` 함수에선 입력값이 1 증가할 때마다 코드의 실행 시간이 1초씩 증가한다. 즉 입력값이 증가함에 따라 `같은 비율`로 걸리는 시간이 늘어나고 있다. 함수 `another_O_n_algorithm`은 입력값이 1 증가할 때마다 2초씩 실행시간이 증가한다. 이 알고리즘이 O(2n)으로 표현된다고 생각할 수 있지만, 이 알고리즘 또한 Big-O 표기법으로는 O(n)으로 표기한다. 입력값이 커지면 커질수록 계수의 의미가 점점 퇴색되기 때문에, 같은 비율로 증가하고 있다면 2배가 아닌 5배, 10배로 증가하더라도 O(n)으로 표기한다.<br/>

#### O(log n)

![시간 복잡도가 O(log n)인 경우](https://s3.ap-northeast-2.amazonaws.com/urclass-images/sXMI9zIhA-1614944910776.png)

O(log n)은 logarithmic complexity라고 부르면 Big-O 표기법중 O(1) 다음으로 빠른 시간 복잡도를 가진다. BST(Binary Search Tree), up&down 게임 등을 예로 들 수 있다.<br/>

#### O(n²)

![시간 복잡도가 O(n²)인 경우](https://s3.ap-northeast-2.amazonaws.com/urclass-images/-bqCNuama-1614944884289.png)

O(n²)은 quadratic complxity라고 부르며, 입력값이 증가함에 따라 시간이 n의 제곱수 비율로 증가하는 것을 의미한다.<br/>

예를 들어 입력값이 1일 경우 1초가 걸리던 알고리즘에 5라는 값을 주었더니 25초가 걸리게 된다면, 이 알고리즘의 시간 복잡도는 O(n²)라고 표현한다. O(n²)의 시간 복잡도를 가진 알고리즘은 아래와 같다.

```javascript
function O_quadratic_complexity(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      // do something for 1 second
    }
  }
}

function another_O_quadratic_algorithm(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      for (let k = 0; k < n; k++) {
        // do something for 1 second
      }
    }
  }
}
```

2n, 5n을 모두 O(n)이라고 표현하는 것 처럼, n³과 n⁵ 모두 O(n²)로 표기한다. n이 커지면 커질수록 지수가 주는 영향력이 점점 퇴색되기 때문에 이렇게 표기한다.<br/>

#### O(2n²)

![시간 복잡도가 O(2n²)인 경우](https://s3.ap-northeast-2.amazonaws.com/urclass-images/RHVH9dEGI-1614944959297.png)

O(2n²)은 exponential complexity라고 부르며 Big-O 표기법 중 가장 느린 시간 복잡도를 가진다. 구현한 알고리즘의 시간 복잡도가 O(2n²)이라면 다른 접근 방식을 고민해 보는 것이 좋다.

```javascript
function fibonacci(n) {
  if (n <= 1) {
    return 1;
  }
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

재귀로 구현하는 피보나치 수열은 O(2n²)의 시간 복잡도를 가진 대표적인 알고리즘이다. 브라우저 개발자 창에서 n을 40으로 두어도 수초가 걸리는 것을 확인할 수 있으며, n이 100 이상이면 평생 결과를 반환받지 못할 수도 있다.
<br/>

### 데이터 크기에 따른 시간 복잡도

<hr/>

일반적으로 코딩 테스트 문제를 풀 때에는 정확한 값을 제한된 시간 내에 반환하는 프로그램을 작성해야 한다. 그래서 컴파일러 혹은 컴퓨터의 사양에 따라 차이는 있겠지만, 시간제한과 주어진 데이터 크기 제한에 따른 시간 복잡도를 어림잡아 예측해 보는 것은 중요하다.<br/>

예를 들어 입력으로 주어지는 데이터에는 n만큼의 크기를 가지는 데이터가 있고, n이 1,000,000보다 작은 수일 때 O(n)혹은 O(nlogn)의 시간 복잡도를 가지도록 예측하여 프로그램을 작성할 수 있다. 여기서 n²의 시간 복잡도는 예측할 수가 없기 때문이다. n²의 시간 복잡도를 예측할 수 없는 이유는 실제 수를 대입해 계산해보면 유추할 수 있다. 1,000,000²은 즉시 처리하기에 무리가 있는 숫자이다. 그렇기 때문에 시간 복잡도를 줄이려고 노력해야 한다.<br/>

그러나 만약 n ≤ 500 으로 입력이 제한된 경우에는 O(n³)의 시간 복잡도를 가질 수 있다고 예측할 수 있다. 예측한 대로 O(n³)의 시간 복잡도를 가지는 프로그램을 작성한다면 문제를 금방 풀 수 있다면, 이때는 굳이 시간 복잡도를 O(log n)까지 줄이기 위해 끙끙댈 필요는 없다.<br/>

즉, 입력 데이터가 클 때는 O(n) 혹은 O(log n)의 시간 복잡도를 만족할 수 있도록 예측해서 문제를 풀어야 한다. 그러나 주어진 데이터가 작을 때는 시간 복잡도가 크더라도 문제를 풀어내는 것에 집중해야 한다.

대략적인 데이터 크기에 따른 시간 복잡도는 다음과 같다.

| **데이터 크기 제한** | **예상되는 시간 복잡도** |
| -------------------- | ------------------------ |
| n ≤ 1,000,000        | O(n) or O (logn)         |
| n ≤ 10,000           | O(n2)                    |
| n ≤ 500              | O(n3)                    |
