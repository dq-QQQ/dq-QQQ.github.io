---
title: 타입스크립트 실습 QUIZ
date: 2021-04-28 10:18:01
permalink: /:short_year-:month-:day/:title
categories: [web/network, frontend]
tags: [typescript, ts, 타입스크립트, quiz]
---
# 나를 위해 내가 직접 만든 QUIZ

## Q1. 다음 빈칸에 들어갈 알맞은 것은?

```jsx
function joinStudy(name: string, age: number): ( 빈칸 ) {
  if (age > 23) {
    console.log(name)
  }
}
joinStudy('John Doe', 35)
```



## Q2. 아래 arr는 숫자로 이루어진 배열이고 수정이 불가능하다. 이때 빈칸에 들어갈 것으로 가장 알맞은 것은?

```jsx
let arr: (      빈칸     ) = [1,2,3];
```



## Q3. OX퀴즈

- (   ) 클래스끼리는 상속이 가능하지만 인터페이스간에는 상속이 불가능하다.
- (   ) enum은 javascript로 컴파일 된 후에도 남아있다.



## Q4. 다음중 Capt 타입은 어떤 모습인가?

```jsx
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

```jsx
// Capt타입
{
	// 여기에 답안을 작성해주세요.
	
	
}
```



## Q5. 다음 빈칸에 들어갈 수 있는 것을 모두 작성해주세요.

```jsx
interface Animal{
  name: string;
	age: number,
  move: number;
}
interface Bird{
  name: string;
	age: number;
  fly: string;
}
function hawk(sth: Animal & Bird) {
 // 여기에 답안을 작성해주세요.
}
```



## Q6. 다음 코드가 console에 출력되는 결과는 무엇일까요?

```jsx
class Animal {
    name: string;
    constructor(theName: string) { this.name = theName; }
    move(distanceInMeters: number = 0) {
        console.log(`${this.name} moved ${distanceInMeters}m.`);
    }
}

class Snake extends Animal {
    constructor(name: string) { super(name); }
    move(distanceInMeters = 5) {
        console.log("Slithering...");
        super.move(distanceInMeters);
    }
}

class Horse extends Animal {
    constructor(name: string) { super(name); }
    move(distanceInMeters = 45) {
        console.log("Galloping...");
        super.move(distanceInMeters);
    }
}

let sam = new Snake("Sammy the Python");
let tom: Animal = new Horse("Tommy the Palomino");

sam.move();
tom.move(34);
```

```jsx
//답안

```



## Q7. 타입스크립트에서 어떠한 클래스 혹은 함수에서 사용할 타입을 그 함수나 클래스를 사용할 때 결정하는 프로그래밍 기법은?

- 



## Q8-1. 다음 두 가지 방법 중 어떤 방법이 컴포넌트 재사용성을 높일 수 있는 방법이라고 생각하는가? 그리고 그 이유는 무엇인가?

```jsx
// 1번
class Stack {
  private data: any[] = [];

  contructor() {}

  push(item: any): void {
    this.data.push(item);
  }

  pop(): any {
    return this.data.pop();
  }
}
```

```jsx
// 2번

class Stack<T> {
  private data: T[] = [];

  constructor() {}

  push(item: T): void {
    this.data.push(item);
  }

  pop() {
    return this.data.pop();
  }
}
```

- 



## 08-2. 마지막 로그에 찍히는 numberStack과 stringStack의 데이터를 표기하시오.

```jsx
class Stack<T> {
  private data: T[] = [];

  constructor() {}

  push(item: T): void {
    this.data.push(item);
  }

  pop() {
    return this.data.pop();
  }
}

const numberStack = new Stack<number>();
const stringStack = new Stack<string>();
numberStack.push(1);
numberStack.push(2);
numberStack.push(3);
stringStack.push('a');
stringStack.push('b');
numberStack.pop();
stringStack.pop();
console.log(numberStack);
console.log(stringStack);
```

```jsx
// stringStack
"data": [

]

// numberStack
"data": [

]
```



### 퀴즈에 대한 해설은 아래 노션 링크에서 확인할 수 있습니다!

[퀴즈 답안 보러가기](https://www.notion.so/Typescript-7b44163f91fc411e978ecc0c3f527173)

---

References.

https://typescript-kr.github.io/

https://joshua1988.github.io/ts/