---
layout: single
categories: TypeScript
tags: [typescript, type]
title: \[TypeScript\] TypeScript 기본
toc: true
toc_sticky: true
---

<br/>

# TypeScript

## 타입스크립트란?

1. TypeScript는 JavaScript에 추가적인 구문을 추가하여 editor에서 초기에 오류를 잡을 수 있도록 지원한다.
2. TypeScript 코드는 JavaScript가 실행되는 모든 곳(브라우저, Node.js ...)에서 JavaScript로 변환될 수 있다.
3. TypeScript는 JavaScript를 이해하고 타입 추론(type inference)를 사용하여 추가 코드 없이도 훌륭한 도구를 제공한다.

<br/>

## 기본 타입

TypeScript는 JavaScript와 거의 동일한 데이터 타입을 지원하며, 열거 타입을 이용하여 더 편리하게 사용할 수 있다.

### Boolean

```typescript
let isCaptain: boolean = true;
isCaptain = false; // ok
isCaptain = "Gundogan"; // error | Type 'string' is not assignable to type 'boolean'.
```

`isLoading` 변수는 `boolean` 타입으로 지정되었기 때문에, 마지막 라인에서 다음과 같은 에러가 발생한다.<br/>
![](/images/2023-03-03-typescript-start/1.png)

### 숫자 (Number)

```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

### 문자열 (String)

```typescript
let color: string = "blue";
color = "red";
```

```typescript
let fullName: string = `Kevin De Bruyne`;
let age: number = 31;
let sentence: string = `Hello, my name is ${fullName}.
I'll be ${age + 1} years old next month.`;
```

### 배열 (Array)

배열 타입은 두 가지 방법으로 쓸 수 있다.

```typescript
let arr: number[] = [1, 2, 3, 4];
```

```typescript
// 제네릭 배열 타입
let arr: Array<number> = [1, 2, 3];
```

### 객체 (Object)

```typescript
const player: object = {
  name: "Kev",
};
```

#### 객체 속성별 타입 지정 및 옵션 속성

객체에 속성별로 타입을 지정할 경우, 들어오지 않은 속성이 있을 때 오류가 발생하는데,<br/>
선택적으로 사용하고 싶은 속성은 타입 지정 시 물음표를 붙여 옵션 속성으로 지정해주면 속성이 들어오지 않더라도 오류가 발생하지 않는다.<br/>
물음표는 아래 `age`는 `number` 혹은 `undefined`라는 일종의 단축어를 의미한다.

```typescript
const player: {
  name: string;
  backNumber: number;
  position: string;
  age?: number; // 이와 같이 물음표를 붙여주면 속성이 들어오지 않더라도 오류가 발생하지 않는다.
} = {
  name: "Kevin",
  backNumber: 17,
  position: "midfielder",
};
```

<br/>

## 타입 별칭 (Type Aliases)

타입 별칭은 특정 타입이나 인터페이스를 참조할 수 있는 타입 변수를 의미한다.<br/>
타입 별칭은 새로운 타입 값을 하나 생성하는 것이 아니라 정의한 타입에 대해 나중에 쉽게 참고할 수 있게 이름을 부여하는 것과 같다.

### 사용 예시

```typescript
// string 타입을 사용할 때
cosnt name: string = 'Phil';

type PlayerName = string;
const name: PlayerName = 'Foden';
```

```typescript
type Player = {
  name: string;
  backNumber: number;
  position: string;
  age?: number;
};

const playerKev: Player = {
  name: "De Bruyne",
  backNumber: 17,
  position: "Midfielder",
};

playerKev.age = 31; // ok
playerKev.team = "Manchester City"; // error | Property 'team' does not exist on type 'Player'.
```

```typescript
const Age = number;

type Player = {
  name: string;
  backNumber: number;
  position: string;
  age?: Age;
};
```

### 타입 별칭 vs 인터페이스

타입 별칭과 인터페이스의 가장 큰 차이점은 타입의 확장 가능/ 불가능 여부이다. 인터페이스는 확장이 가능한 데 반해 타입 별칭은 확장이 불가능하다. 따라서, 가능한 한 `type`보다는 `interface`로 선언해서 사용하는 것을 추천한다.

> [좋은 소프트웨어는 언제나 확장이 용이해야 한다는 원칙](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle)에 따라 가급적 확장 가능한 인터페이스로 선언하면 좋다.

## 함수의 리턴 타입 지정하기

```typescript
type Player = {
  name: string;
  backNumber?: number;
  position?: string;
  age?: number;
};

function playerMaker(name: string): Player {
  return {
    name,
  };
}

const playerRuben = playerMaker("Dias");
playerRuben.backNumber = 3; // ok
playerRuben.team = "Man City"; // error | Property 'team' does not exist on type 'Player'.
```

## 읽기 전용 (readonly)

읽기 전용 속성은 객체, 배열 등을 처음 생성할 때만 값을 할당하고 그 이후에는 변경할 수 없는 속성을 의미한다.<br/>
읽기 전용으로 객체, 배열을 선언하고 나서 수정하려고 하면 오류가 발생한다.

```typescript
type Player = {
  readonly name: string;
  backNumber?: number;
  position: string;
};

function PlayerMaker(name: string, position: string): Player {
  return {
    name,
    position,
  };
}

const player = playerMaker("Foden", "Midfielder");
player.position = "forward"; // ok
player.name = "Haaland"; // error | Cannot assign to 'name' because it is a read-only property.
```

```typescript
const players: ReadonlyArray<string> = ["De Bruyne", "Rodri", "Dias"];
players.push("Walker"); // error | Property 'push' does not exist on type 'readonly string[]'.
players.splice(0, 1); // error | Property 'splice' does not exist on type 'readonly string[]'. Did you mean 'slice'?
players[0] = "Bernardo"; // error | Index signature in type 'readonly string[]' only permits reading.
```

```typescript
const players: readonly string[] = ["Ake", "Akanji", "Laporte"];
players.push("Alvarez"); // error | Property 'push' does not exist on type 'readonly string[]'.
players.splice(0, 1); // error | Property 'splice' does not exist on type 'readonly string[]'. Did you mean 'slice'?
players[0] = "Grealish"; // error | Index signature in type 'readonly string[]' only permits reading.
```

## Tuple

튜플은 배열의 길이가 고정되고 각 요소의 타입이 지정되어 있는 배열 형식을 의미한다. 만약 정의하지 않은 타입, 인덱스로 접근할 경우 오류가 발생한다.

```typescript
const playerArr: [string, number, boolean] = ["Foden", 47, false];
playerArr[0] = 1; // error | Type 'number' is not assignable to type 'string'.

const playerArr: readonly [string, number, boolean] = ["Foden", 47, false];
playerArr[0] = 1; // error | Cannot assign to '0' because it is a read-only property.
```
