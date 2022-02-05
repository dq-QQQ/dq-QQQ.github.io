---
title: 자바스크립트 변수-var, let, const 꼭 알아야할 차이점
date: 2021-08-09 23:18:01
permalink: /:short_year-:month-:day/:title
categories: [frontend]
tags: [Javascript, let, var, const, 변수]
---

# 자바스크립트 변수 var, let, const 비교

유튜브 `코딩앙마 채널`의 자바스크립트 중급 1편 var, let, const를 보다가 좋은 내용이 있어 정리합니다.



## 호이스팅 

선언하기 전에 호출된 var변수가 오류가 나지 않는다는 것을 거의 모든 프론트엔드 개발자라면 알고 있을 것입니다. 그 이유는 바로 hoisting 때문인데, ES6 이후 나온 let이나 const 로 변수를 선언하는 것은 var와 달리 이것이 되지 않는다. 그렇다면 let은 호이스팅 되지 않는 것일까?라는 의문이 들었습니다.



### 💡 let도 hoisting된다.

<u>결론부터 말하자면 let도 호이스팅 됩니다</u>. 하지만 var처럼 동작하지 않는 이유는 `변수의 생성단계 3가지 ` **"선언"-"초기화"-"할당"** 의 진행과정이 다르기 때문이다.

| var                 | let       | const                         |
| ------------------- | --------- | ----------------------------- |
| 1. 선언 + 2. 초기화 | 1. 선언   | 1. 선언 + 2. 초기화 + 3. 할당 |
| -                   | 2. 초기화 |                               |
| 3. 할당             | 3. 할당   |                               |

위 표에서 보듯이 **세 가지 변수설정 타입은 모두 다른 과정을 통해 변수를 생성**합니다.

```javascript
// 1. var
console.log(name) // undefined
var name="홍길동"

// 2. let 
console.log(name) // Error: 레퍼런스 에러
let name="홍길동"

// 3. const
console.log(name) // Error
const name="홍길동"

// 4. const 추가
const name;
name="홍길동"
```

- var의 경우 아직 할당되지 않은 name을 먼저 호출하더라도 호이스팅된 변수명 name은 이미 알고 있으며 다만 해당 값은 undefined상태이다. 따라서 에러가 나지 않는다.

- let의 경우 호이스팅은 되므로 name변수를 아예 모르는 것은 아니나, 초기화(name에 undefined)가 되지않았으므로 name에 해당하는 레퍼런스가 없어 레퍼런스 에러가 난다.
- const의 경우 선언/초기화/할당 세 가지가 모두 한 번에 이뤄져야 하는데 그렇지 않았으므로 에러가 발생한다.
- const의 경우 선언과 동시에 할당까지 이뤄져야 한다. 따라서 4번처럼 생성만 해두고 나중에 할당하면 오류가 발생한다.



## 스코프

| var                                                          | let, const                                             |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| 함수 스코프                                                  | 블록 스코프                                            |
| function() 단위                                              | if, while, for, try/catch문 등                         |
| -> if문이나 while문 등 블록스코프 내에서 선언되어도 함수단위에서 호출이 가능함. <br />단, 함수단위를 넘어서는 곳에서의 호출은 안된다. | if문이나 while문등 선언된 블록 내에서만 호출이 가능함. |




---
Ref.

[유튜브 코딩앙마 채널](https://www.youtube.com/watch?v=ocGc-AmWSnQ&list=PLZKTXPmaJk8JZ2NAC538UzhY_UNqMdZB4)

