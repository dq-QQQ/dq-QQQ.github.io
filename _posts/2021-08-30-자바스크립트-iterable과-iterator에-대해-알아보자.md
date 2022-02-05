---
title: 자바스크립트 iterable과 iterator에 대해 알아보자
date: 2021-08-30 23:18:01
permalink: /:short_year-:month-:day/:title
categories: [frontend, web/network]
tags: [javascript, iterable, iterator, ES6]
---

# 자바스크립트 iterable과 iterator에 대해 알아보자 
## 이터러블 (iterable)이란?

> 반복 가능한 객체 (ES2015에 추가된 문법)

객체의 `Symbol.iterator` 속성에 특정 형태의 함수가 들어있다면, 이를 ***반복 가능한 객체(iterable object)*** 혹은 줄여서 **iterable**이라 부르고, <u>해당 객체는 iterable protocol을 만족한다</u>고 말합니다.



### 이터러블의 조건 

1. 순회 할수 있는 데이터를 가지고 있어야한다. 
2. 전역 “well-known” symbol 인`Symbol.iterator` 을 메서드로 가지고 있어야한다. 또한 이 메서드는 #3 , #6 에 따라 구현되어야 한다.
3. `Symbol.iterator` 메서드는 **“iterator” 객체를 반환**해야합니다
4. “iterator” 객체는 **반드시 next 라고 하는 메서드를 가져야합니다.** (지난 Generator 포스팅에서 봤던 개념입니다.)
5. next 에는 #1에 저장되어있는 데이터에 접근 할 수 있어야합니다.
6. “iterator” 객체인 iteratorObj를 iteratorObj.next()하면 `{value:<stored data},done:false}` #1 데이터가 추출 되며 전부다 순회했을 경우 `{done:false}` 가 반환되도록 한다.



### 이터러블(iterable)이 사용되는 곳

- for... of 루프

```javascript
const iterable = [1,2,3]
for (let value of iterable) {
    console.log(value)
}
// 1, 2, 3
```



- destructuring

```javascript
// spread operator
let newIterable = [...iterable] // [1, 2, 3]

// destructuring
const [c1, c2] = 'hello';
```





## 이터러블(iterable)과 이터레이터(iterator)의 차이

- 이터러블: 순회할 수 있는 객체
- 이터레이터: next메소드를 호출하면 {done: boolean, value} 를 반환하는 오브젝트, 객체 그 자체

이터러블은 순회할 수 있는 모든 객체가 될 수 있다. 따라서 배열(Array), 문자열(string), 객체 등 다양한 것들이 될 수 있다. 이터레이터는 이터러블의 속성을 가진 바로 그 객체를 의미한다. 

이터레이터는 .next() 메소드를 반드시 갖는다. 즉, 앞 뒤로 바로 이전과 바로 다음 값만을 가져올 수 있다. 하지만 이터러블 중 하나인 배열은 인덱스로 랜덤 Access가 가능하다는 점에서 이터러블과 이터레이터의 차이를 알 수 있다.

물론 개념적으로 완전히 포괄하는 느낌은 아니지만, 사실상 배열은 언제든 이터레이터로 변환이 가능하다는 점에서 이터레이터가 이터러블을 포함하는 관계로 볼 수 있다.

| Iterable 이터러블       | Iterator 이터레이터                               |
| ----------------------- | ------------------------------------------------- |
| 랜덤 Access가 가능하다. | .next() 메소드, 바로 앞/뒤 값만을 가져올 수 있다. |
| 기능이 많다 -> 무겁다   | 기능이 배열에 비해 상대적으로 적다 -> 가볍다      |
| 메모리 사용량이 많다.   | 메모리 효율적이다.                                |



---

Ref.

https://helloworldjavascript.net/pages/260-iteration.html
