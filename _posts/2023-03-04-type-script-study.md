---
layout: single
categories: TypeScript
tags: [typescript, type]
title: \[TypeScript\] any, unknown, void, never
toc: true
toc_sticky: true
---

<br/>

## any

> 아무 타입이나 될 수 있음.

```typescript
const anyArr: any[] = [1, 2, 3, 4];
const bArr: any = true;

// any는 이런 식으로 보호장치를 비활성화시키기 때문에 주의해서 사용해야 한다.
anyArr + bArr; // 허용됨
```

## unknown

> ex) API로부터 응답을 받는데 그 응답의 타입을 모른다면 unknown이라는 타입을 쓸 수 있다.

```typescript
let unknownA: unknown;

let examB = unknownA + 1; // 경고

if (typeof unknownA === "number") {
  // 이 범위 안에서는 unknownA가 number이기 때문에 아래 작업을 허용함.
  let examB = unknownA + 1;
}

unknownA.toUpperCase(); //경고

if (typeof unknownA === "string") {
  // 이 범위 안에서는 unknownA가 string이기 때문에 아래 작업을 허용함.
  unknownA.toUpperCase();
}
```

## void

> void는 아무것도 리턴하지 않는 함수를 대상으로 사용

```typescript
// Typescript는 이 함수가 아무것도 return하지 않는다는 것을 자동으로 인식.
function hello() {
  console.log("hello");
}

const funcA = hello();
funcA.toUpperCase();
```

## never

> 함수가 절대 return하지 않을 때 발생

```typescript
function helloWorld(): never {
  throw new Error("hello");
}

function hello2(name: string | number) {
  if (typeof name === "string") {
    return name.toUpperCase();
  } else if (typeof name === "number") {
    return name + 1;
  } else {
    // 타입이 올바르게 들어왔다면, 이 스코프 내의 코드는 절대 실행되지 않아야 한다
  }
}
```
