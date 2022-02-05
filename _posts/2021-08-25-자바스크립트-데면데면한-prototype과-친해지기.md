---
title: 자바스크립트 log찍으면 만나는 친한듯 친하지는않은  prototype 알아보기
date: 2021-08-25 23:18:01
permalink: /:short_year-:month-:day/:title
categories: [frontend, web/network]
tags: [javascript, prototype, object]
---

# 자바스크립트 log찍으면 만나는 친한듯 친하지는않은  prototype 알아보기

## :bulb: 핵심 체크 문답

## 1. prototype이란? 

자바스크립트의 모든 object에 있는 숨겨진 속성.



## 2. prototype에 접근하는 방법은?

1. getPrototypeOf()

   - prototype에 접근하는 가장 추천하는 방법

     ```javascript
     const example = {
         property: "Hello World"
     }
     Object.getPrototypeOf(example)
     ```

2. __ proto __ 사용 

   - 브라우저에서만 사용가능하다고 알려져있으나 사실상 거의 모든 자바스크립트 엔진에서 사용할 수 있다고 한다.



## 3. prototype 값을 변경하는 방법은?

1. setPrototypeOf()

2. __ proto __ 사용

   ```javascript
   // 1.
   Object.setPrototypeOf(example)
   
   // 2. 
   example.__proto__ = 'something'
   ```



## 4. prototype의 특징

- 체이닝

```javascript
const person = {
    name: "mike"
};
const programmer = {
    language: 'javascript'
}
const frontDev = {
    framework: 'react'
}
Object.setPrototypeOf(programmer, person);
Object.setPrototypeOf(frontDev, programmer);

// frontDev에는 name과 language속성이 없는 이 상황에서 console.log(frontDev.name, frontDev.language)를 하면? => mike javascript 출력
```

- frontDev에는 name과 language 속성이 없는데 어떻게 person과 programmer의 name과 language값을 출력했을까? 바로 prototype의 체이닝 특성때문이다.

- frontDev의 prototype은 "programmer"이고, programmer의 prototype은 "person"으로 연결되어있습니다.

- 즉 frontDev의 name과 language는 없지만, 해당 값을 출력하라고 하면 javascript는 내부에서 prototype으로 연결된 다른 Object들의 속성을 살펴봅니다.

- ```javascript
  frontDev.__proto__.proto__.name  // => mike	(from person)
  frontDev.__proto__.language 	// => javascript (from programmer)
  ```

