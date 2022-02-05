---
title: Typescript 시작하기
date: 2021-04-14 23:18:01
permalink: /:short_year-:month-:day/:title
categories: [web/network, frontend]
tags: [typescript, ts, 타입스크립트]
---



# 타입스크립트 fundamentals - 타입, 함수, 인터페이스, enum, 클래스


## 1. 기본타입

변수선언방식 변수명 : 타입 = 값;

```tsx
let str: string = 'hi'
let num: number = 10;
let isLoggedIn: boolean = false;
```

### Array

요소의 집합

```tsx
let arr: number[] = [1, 2, 3];
arr[2] = 100;

// 타입이 다르므로 에러
arr[2] = 'hi';
```

### Tuple

**길이가 고정**되고 요소 **타입이 지정**된 배열

```tsx
let tuple: [string, number] = ['hi', 10];

//길이가 고정되기때문에 에러뜸
tuple[5] = 'hello';
// number타입에 string 할당 x 에러
tuple[1] = 'hi';

```

### Enum

**상수**들의 집합이다.

```tsx
enum Avengers { Capt, IronMan, Thor }
let hero: Avengers = Avengers.Capt;

console.log(hero); // 0

//읽기전용이라서 할당불가 에러
Avengers.Capt = 3;
```

### Any

자바스크립트의 변수랑 똑같다. 뭐든 할당 가능

```tsx
let str: any = 'hi';
let num: any = 10;
let arr: any = ['a', 2, true];

//any라서 num에 'hi' 할당 가능
num = 'hi';
```

### Void

undefined와 null만 할당가능하다. 일반적으로 반환하지 않는 **함수**에서 사용

```tsx
let unuseful: void = undefined;
function notuse(): void {
  console.log('sth');
}
```

### never

에러를 throw 하거나 절대 반환하지 않는 함수(무한루프일때 쓰이네요)

```tsx
function neverEnd(): never {
  while (true) {

  }
}

function error(message: string): never {
    throw new Error(message);
}
```

## 2. 함수

### 함수의 기본적인 타입 선언

자바스크립트와의 차이점은 **매개 변수**와 **반환 값**에 타입 부여

```tsx
function sum(a: number, b: number): number {
	return a + b;
}
```

### 함수의 인자

전달 인자의 수가 더 많거나 적거나 하면 당연히 안되겠죠? 당연히 타입도 다르면 안되요

```tsx
function sum(a: number, b: number): number {
  return a + b;
}
sum(10, 20); // 30
sum(10, 20, 30); // error, too many parameters
sum(10); // error, too few parameters
```

### 선택적 매개변수

하지만 매개변수에 ?를 달아주면 그 전달인자를 넘기지 않아도 됩니다.

```tsx
function sum(a: number, b?: number): number {
  return a + b;
}
sum(10, 20); // 30
sum(10, 20, 30); // error, too many parameters
sum(10); // 10
```

```tsx
// error 필수 매개변수가 선택적 매개변수 
// 선택적 매개변수가 앞에 있으면 안됩니다.
function sum(a?: number, b: number): number {
  return a + b;
}
```

기본값도 설정해 줄 수 있습니다.

```tsx
function sum(a: number, b = 100): number {
  return a + b;
}
sum(10, undefined); // 110
sum(10, 20, 30); // error, too many parameters
sum(10); // 110
```

### 인터페이스

인터페이스는 상호간의 정의한 약속이나 규칙을 의미한다.

객체의 속성과 속성타입

함수의 매개변수나 반환타입

배열과 객체를 접근하는 방식

클래스

logAge 메소드는 age라는 속성을 갖고 number타입을 갖는 객체를 받는것을 약속했다.

```tsx
let person = { name: 'Capt', age: 28 };

function logAge(obj: { age: number }) {
  console.log(obj.age); // 28
}
logAge(person); // 28
```

```tsx
interface personAge {
  age: number;
}

function logAge(obj: personAge) {
  console.log(obj.age);
}
let person = { name: 'Capt', age: 28 };
logAge(person);
```

### 옵션속성

아까 매개변수때와 마찬가지로 ?를 붙혀주면 그 속성을 모두 다 꼭 사용하지 않아도 됩니다.

```tsx
interface CraftBeer {
  name: string;
  hop?: number;  
}

let myBeer = {
  name: 'Saporo'
};
function brewBeer(beer: CraftBeer) {
  console.log(beer.name); // Saporo
}
brewBeer(myBeer);
```

### 읽기 전용 속성

readonly가 붙은 속성은 읽는것만 된다.

```tsx
interface CraftBeer {
  readonly brand: string;
}

let myBeer: CraftBeer = {
  brand: 'Belgian Monk'
};
myBeer.brand = 'Korean Carpenter'; // error!
```

### 읽기 전용 배열

ReadonlyArray로 선언하면 배열 내용 변경 불가ReadonlyArray로 선언하면 배열 내용 변경 불가

```tsx
let arr: ReadonlyArray<number> = [1,2,3];
arr.splice(0,1); // error
arr.push(4); // error
arr[0] = 100; // error
arr = [10, 20, 30]; // error
```

객체 선언과 관련된 타입 체킹

```tsx
interface CraftBeer {
  brand?: string;
}

function brewBeer(beer: CraftBeer) {
  // ..
}
brewBeer({ brandon: 'what' }); // 속성이 다르니 에러뜹니다.
```

이러면 타입 체크를 무시한다.

```tsx
let myBeer = { brandon: 'what' }';
brewBeer(myBeer as CraftBeer);
```

### 함수 타입

함수 매개변수와 반환타입도 인터페이스 정의가 가능하다.

```tsx
interface login {
  (username: string, password: string): boolean;
}

let loginUser: login; // 함수 저장할 변수 선언
loginUser = function(id: string, pw: string) {
  console.log('로그인 했습니다');
  return true;
}
```

클래스 타입

자바의 인터페이스와 목적이 비슷한데

어떤 인터페이스를 implements한 클래스가 있다면

인터페이스의 메소드와 변수가 있다는 것을 보장한다.

```tsx
interface CraftBeer {
  beerName: string;
  nameBeer(beer: string): void;
}

class myBeer implements CraftBeer {
  beerName: string = 'Baby Guinness';
  nameBeer(b: string) {
    this.beerName = b;
  }
  constructor() {}
}
```

인터페이스 끼리 상속도 가능합니다.

```tsx
interface Person {
  name: string;
}
interface Drinker {
  drink: string;
}
interface Developer extends Person {
  skill: string;
}
let fe = {} as Developer;
fe.name = 'josh';
fe.skill = 'TypeScript';
fe.drink = 'Beer';
```

## 4. Enum

> 특정 값들의 **집합**을 의미하는 자료형으로 크게 {숫자형 이넘, 문자형 이넘} 두 가지가 있다

- Enum이라는 개념을 이해하기 어려웠던 이유는, javascript에는 enum이 없었기 때문이다. (하지만 검색해보니 C언어에서는 제공하는 것 같음.)

### 4-1. 숫자형 이넘

```tsx
enum Direction {
  Up = 1,
  Down,
  Left,
  Right
}
```

특이한 것은 이렇게 선언하면  양방향으로 호출할 수 있는 특이한 자료구조가 된다는 것이다.

```tsx
console.log(Direction[1])    // "Up"
console.log(Direction["Up"]) // 1
console.log(Direction[3])    // "Left"
```

이와 같이 숫자형 Enum에서 Direction.Up 으로 1값을 얻거나 반대로 Direction[1]로 "Up"값을 얻는 것을 **`리버스 매핑`** 이라고 한다.

이렇게 초기값을 선언해주면 1, 2, 3, 4 의 순서로 1씩 증가하며 할당된다. 만약,

```tsx
enum Direction {
	Up, 
	Down,
	Left,
	Right
}
```

으로 선언되었다면 Up - 0 , Down - 1, Left - 2, Right - 3이 된다.

### 4-2 숫자형 enum 사용

```tsx
enum Response {
  No = 0,
  Yes = 1,
}

function respond(recipient: string, message: Response): void {
  console.log(recipient, message)
}

respond("Captain Pangyo", Response.Yes);

--------------------
[LOG]: "Captain Pangyo",  1
```

### 4-3. 문자형 enum

> 문자형 이넘은 이넘 값 전부 다 특정 문자 또는 다른 이넘 값으로 초기화 해줘야 합니다.

```tsx
enum Direction {
    Up = "UP",
    Down = "DOWN",
    Left = "LEFT",
    Right = "RIGHT",
}
```

** 복합 enums **

문자와 숫자를 혼합하여 enum을 생성할 수 있으나, 권장하지 않는 방식!

```tsx
enum BooleanLikeHeterogeneousEnum {
    No = 0,
    Yes = "YES",
}
```

### 4-4. 런타임 시점에서의 이넘 특징

이넘은 런타임시에 실제 객체 형태로 존재합니다. 예를 들어 아래와 같은 이넘 코드가 있을 때

```tsx
enum E {
  X, Y, Z
}

function getX(obj: { X: number }) {
  return obj.X;
}
getX(E); // 이넘 E의 X는 숫자이기 때문에 정상 동작
-----
Quiz. 
getX(E)값을 변수에 넣어서 출력한다면, 얼마나 나올까?
```

### 4-5. 컴파일 시점에서의 이넘 특징

```tsx
enum LogLevel {
  ERROR, WARN, INFO, DEBUG
}

// 'ERROR' | 'WARN' | 'INFO' | 'DEBUG';
type LogLevelStrings = keyof typeof LogLevel;

function printImportant(key: LogLevelStrings, message: string) {
    const num = LogLevel[key];
    if (num <= LogLevel.WARN) {
       console.log('Log level key is: ', key);
       console.log('Log level value is: ', num);
       console.log('Log level message is: ', message);
    }
}
printImportant('ERROR', 'This is a message');

-------
[LOG]: "Log level key is: ",  "ERROR" 
[LOG]: "Log level value is: ",  0 
[LOG]: "Log level message is: ",  "This is a message"
```

### 4-6. Typescript enum을 사용하는 이유

Enum은 추상화의 수단이다.

다국어 코드 (Language Code)를 할당한다고 생각해보자

```tsx
type LanguageCode = 'ko' | 'en' | 'ja' | 'zh' | 'es'

const code: LanguageCode = 'ko'

console.log(code) // [LOG]: "ko"

하지만 
cost code: LanguageCode = 'hahahaha'
와 같이 코드를 짜면 typescript에서 에러로 표시해준다.
```

이것도 좋지만 데이터 양이 많아지면 가독성이 많이 떨어진다.

우리가 원하는 것은 korean을 검색하면 'ko'라는 코드가 나왔으면 하는 것이고 기존 방식으로는 다음과 같이 두 가지 방법이 있다.

```tsx
// 이렇게 하면 언어 코드가 위아래에 중복되고
const korean = 'ko'
const english = 'en'
const japanese = 'ja'
const chinese = 'zh'
const spanish = 'es'
type LanguageCode = 'ko' | 'en' | 'ja' | 'zh' | 'es'
let code: LanguageCode = english
console.log(code) // "en"
```

```tsx
// 이렇게 하면 코드가 너무 길어집니다
const korean = 'ko'
const english = 'en'
const japanese = 'ja'
const chinese = 'zh'
const spanish = 'es'
type LanguageCode = typeof korean | typeof english | typeof japanese | typeof chinese | typeof spanish
let code: LanguageCode = spanish
console.log(code) // "es"
```

이러한 이유 때문에 리터럴의 타입과 값에 이름을 붙인 `enum`을 활용하면 가독성을 크게 높일 수 있습니다.

```tsx
enum LanguageCode {
  korean = 'ko',
  english = 'en',
  japanese = 'ja',
  chinese = 'zh',
  spanish = 'es',
}
// 여기서 
// LanguageCode.korean === 'ko'
// (의미상) LanguageCode === 'ko' | 'en' | 'ja' | 'zh' | 'es'
const code: LanguageCode = LanguageCode.korean
console.log(code) // "ko"
```

### 4-7. Typescript enum을 사용하지 않는 이유

### Tree-shaking은 무엇인가요?

Tree-shaking이란 간단하게 말해 사용하지 않는 코드를 삭제하는 기능을 말합니다. 나무를 흔들면 죽은 잎사귀들이 떨어지는 모습에 착안해 Tree-shaking이라고 부릅니다. Tree-shaking을 통해 export했지만 아무 데서도 import하지 않은 모듈이나 사용하지 않는 코드를 삭제해서 번들 크기를 줄여 페이지가 표시되는 시간을 단축할 수 있습니다.

하지만 enum을 사용하게 되면 Tree-shaking이 되지 않습니다.

결론적으로  Tree-shaking 관점에서 보았을 때 아래와 같은 순서로 사용하시길 추천하며 글을 마치겠습니다.

> Union Types > const enum > enum

**정리**

- 같은 ‘종류’를 나타내는 여러 개의 숫자 혹은 문자열을 다뤄야 하는데, 
각각 적당한 이름을 붙여서 코드의 가독성을 높이고 싶다면 enum을 사용!

## 5. 연산자를 이용한 타입 정의

### 5-1. Union Type ( | )

유니온 타입(Union Type)이란 자바스크립트의 OR 연산자(||)와 같이 A이거나 B이다 라는 의미의 타입

```tsx
function logText(text: string | number) {
  // ...
}
```

- text는 string이거나 (OR || ) number이다. 즉, 둘 다 올 수 있다는 뜻.
- 이처럼 `|` 연산자를 이용하여 타입을 여러 개 연결하는 방식을 `유니온 타입 정의 방식` 이라 부른다.

```tsx
function getAge(age: number | string) {
  if (typeof age === 'number') {
    age.toFixed(); // 정상 동작, age의 타입이 `number`로 추론되기 때문에 숫자 관련된 API를 쉽게 자동완성 할 수 있다.
    return age;
  }
  if (typeof age === 'string') {
    return age;
  }
  return new TypeError('age must be number or string');
}
console.log(getAge(10))
console.log(getAge('Hello World'))
console.log(getAge(true))
--- 출력 ---
[LOG]: 10 
[LOG]: "Hello World" 
[LOG]: age must be number or string
```

### 5-2. Intersection Type ( & )

여러 타입을 모두 만족하는 하나의 타입을 의미.

```tsx
interface Person {
  name: string;
  age: number;
}
interface Developer {
  name: string;
  skill: number;
}
type Capt = Person & Developer;
```

```tsx
// Capt의 타입은

{
  name: string;
  age: number;
  skill: string;
}
```

![Intersection Type](https://joshua1988.github.io/ts/assets/img/intersection-diagram.01f4fdfe.png)

### 5-3. Union Type을 쓸 때 주의할 점

```tsx
interface Person {
  name: string;
  age: number;
}
interface Developer {
  name: string;
  skill: string;
}
function introduce(someone: Person | Developer) {
  someone.name; // O 정상 동작
  someone.age; // X 타입 오류 -> 타입스크립트에서 빨간줄로 표시해줌
  someone.skill; // X 타입 오류 -> 타입스크립트에서 빨간줄로 표시해줌
}
```

유니온 타입은 A도 될 수 있고 B도 될 수 있는 타입이지라고 생각하면 파라미터의 타입이 Person도 되고 Developer도 될테니까 함수 안에서 당연히 이 인터페이스들이 제공하는 속성들인 age나 skill를 사용할 수 있겠지라고 생각할 수 있습니다. 

하지만, 타입스크립트 관점에서는 introduce() 함수를 호출하는 시점에 Person 타입이 올지 Developer 타입이 올지 알 수가 없기 때문에 어느 타입이 들어오든 간에 오류가 안 나는 방향으로 타입을 추론하게 됩니다.

따라서 위의 예시 같은 경우에는 의도와는 달리 [someone.name](http://someone.name) 만 정상적으로 작동하게 됩니다.

## 6. Class

### 6-1. Readonly

```tsx
class Developer {
    readonly name: string;
    constructor(theName: string) {
        this.name = theName;
    }
}
let john = new Developer("John");
john.name = "John"; // error! name is readonly.
console.log(john)
--- 출력 ---
[LOG]: Developer: {
  "name": "John"
}
```

### 6-2. Accessor

타입스크립트는 객체의 특정 속성의 접근과 할당에 대해 제어할 수 있습니다. 이를 위해선 해당 객체가 클래스로 생성한 객체여야 합니다. 아래의 간단한 예제를 봅시다.

```tsx
class Developer {
  name: string;
}
const josh = new Developer();
josh.name = 'Josh Bolton';
```

위 코드는 클래스로 생성한 객체의 `name` 속성에 `Josh Bolton`이라는 값을 대입한 코드입니다. 이제 `josh`라는 객체의 `name` 속성은 `Josh Bolton`이라는 값을 갖겠죠.

여기서 만약 `name` 속성에 제약 사항을 추가하고 싶다면 아래와 같이 `get`과 `set`을 활용합니다.

```tsx
class Developer {
  private name: string;
  
  get name(): string {
    return this.name;
  }

  set name(newValue: string) {
    if (newValue && newValue.length > 5) {
      throw new Error('이름이 너무 깁니다');
    }
    this.name = newValue;
  }
}
const josh = new Developer();
josh.name = 'Josh Bolton'; // Error
josh.name = 'Josh';
```

TIP!
get만 선언하고 set을 선언하지 않는 경우에는 자동으로 readonly로 인식됩니다.

### 6-3. Abstract Class

추상 클래스(Abstract Class)는 인터페이스와 비슷한 역할을 하면서도 조금 다른 특징을 갖고 있습니다. 추상 클래스는 특정 클래스의 상속 대상이 되는 클래스이며 좀 더 상위 레벨에서 속성, 메서드의 모양을 정의합니다.

```tsx
abstract class Developer {
  abstract coding(): void; // 'abstract'가 붙으면 상속 받은 클래스에서 무조건 구현해야 함
  drink(): void {
    console.log('drink sth');
  }
}

class FrontEndDeveloper extends Developer {
  coding(): void {
    // Developer 클래스를 상속 받은 클래스에서 무조건 정의해야 하는 메서드
    console.log('develop web');
  }
  design(): void {
    console.log('design web');
  }
}
const dev = new Developer(); // error: cannot create an instance of an abstract class
const josh = new FrontEndDeveloper();
josh.coding(); // develop web
josh.drink(); // drink sth
josh.design(); // design web
```




---
References
https://joshua1988.github.io/ts/

[TypeScript enum을 사용하는 이유](https://medium.com/@seungha_kim_IT/typescript-enum을-사용하는-이유-3b3ccd8e5552)

[TypeScript enum을 사용하지 않는 게 좋은 이유](https://engineering.linecorp.com/ko/blog/typescript-enum-tree-shaking/)

[C언어 Enum](https://dojang.io/mod/page/view.php?id=480)