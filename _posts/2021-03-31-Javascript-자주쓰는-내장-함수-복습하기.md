---
title: Javascript 자주쓰는 내장 함수 복습하기
date: 2021-03-31 23:18:01
permalink: /:short_year-:month-:day/:title
categories: [web/network, frontend]
tags: [javascript, js, vanillaJS, es6]
---



# 자주쓰는 JS 내장함수 :map, find, findIndex, filter, indexOf, splice, slice, shift & pop, join, reduce

## 1. map

map은 배열 안의 각 원소를 변환 할 때 사용 되며, 이 과정에서 새로운 배열이 만들어집니다. 배열.map()

```jsx
const array = [1, 2, 3, 4, 5, 6, 7, 8];
const square = n => n**2
const squared = array.map(square)
console.log(squared)

// [1,  4,  9, 16, 25, 36, 49, 64]
```

- map안에 들어가는 square같은 함수를 `변화함수`라고 한다.
- 변화함수를 쓰지 않고 바로 해도 된다

```jsx
const array = [1, 2, 3, 4, 5, 6, 7, 8];
const squared = array.map(n => n**2)
console.log(squared)
// 결과는 같다. [1,  4,  9, 16, 25, 36, 49, 64]
```

## 2. indexOf

indexOf 는 원하는 항목이 배열 내 몇번째 원소인지 찾아주는 함수입니다.

```jsx
const superheroes = ['아이언맨', '캡틴 아메리카', '토르', '닥터 스트레인지']
const index = superheroes.indexOf('토르')
console.log(index)
// 2
```

## 3. findIndex - 찾아낸 값의 index를 반환

배열 안에 있는 값이 객체이거나, 배열이라면 indexOf 로 찾을 수 없습니다. 이럴 때 findIndex를 사용합니다.

```jsx
// todos에서 id가 3인 객체가 몇 번째 인지 찾기

const todos = [
  {
    id: 1,
    text: '자바스크립트 입문',
    done: true
  },
  {
    id: 2,
    text: '함수 배우기',
    done: true
  },
  {
    id: 3,
    text: '객체와 배열 배우기',
    done: true
  },
  {
    id: 4,
    text: '배열 내장함수 배우기',
    done: false
  }
];

const index = todos.findIndex(todo => todo.id === 3);
console.log(index);

// 2
```

## 4. find - 찾아낸 값 자체를 반환

```jsx
const todos = [
  {
    id: 1,
    text: '자바스크립트 입문',
    done: true
  },
  {
    id: 2,
    text: '함수 배우기',
    done: true
  },
  {
    id: 3,
    text: '객체와 배열 배우기',
    done: true
  },
  {
    id: 4,
    text: '배열 내장함수 배우기',
    done: false
  }
];

const todo = todos.find(todo => todo.id === 3);
console.log(todo);

// {id: 3, text: "객체와 배열 배우기", done: true}
```

## 5. filter

특정 조건을 만족하는 값들만 따로 추출하여 새로운 배열을 만듭니다.

```jsx
const todos = [
  {
    id: 1,
    text: '자바스크립트 입문',
    done: true
  },
  {
    id: 2,
    text: '함수 배우기',
    done: true
  },
  {
    id: 3,
    text: '객체와 배열 배우기',
    done: true
  },
  {
    id: 4,
    text: '배열 내장함수 배우기',
    done: false
  }
];

const tasksNotDone = todos.filter(todo => todo.done === false);
console.log(tasksNotDone);
/* 
todo.done이 false인 {id: 4, text: '배열 내장함수 배우기', done: false} 
객체만 새로운 배열(taskNotDone) 안에 들어간다.
[ { id: 4, text: '배열 내장함수 배우기', done: false } ]

*/

//  이렇게 표현할 수도 있다.
const tasksNotDone = todos.filter(todo => !todo.done);
```

## 6. splice

배열에서 특정 항목을 제거할 때 사용된다. 인덱스 값으로 지우는 것이기 때문에 인덱스를 먼저 구하고 해당 인덱스로부터 몇 개나 지울 것인지 선택하여 여러값을 한 번에 지울 수 있다.

```jsx
const numbers = [10, 20, 30, 40];
const index = numbers.indexOf(30);
numbers.splice(index, 1);
console.log(numbers);

// 30의 index = 2이고 2번째 인덱스로부터 한 개의 값을 지우므로 30만 지워진다.
// [10, 20, 40]
```

## 7. slice

기존 배열에 변화를 일으키지 않고 슬라이싱 하여 새로운 배열을 생성한다.

```jsx
const numbers = [10, 20, 30, 40];
const sliced = numbers.slice(0, 2); // 0부터 시작해서 2전까지

console.log(sliced); // [10, 20]
console.log(numbers); // [10, 20, 30, 40]
```

## 8. shift & pop

shift는 배열의 첫 번째 값을 뽑아내고, pop은 맨 뒤의 값을 뽑아낸다. python과 비교하면 shift = pop(0), pop은 똑같다.

```jsx
const numbers = [10, 20, 30, 40];
const value = numbers.shift();
console.log(value); // 10
const value2 = numbers.pop();
console.log(value2); // 40
console.log(numbers); //[20, 30]
```

## 9. join

배열 안의 값들을 문자열 형태로 합쳐줍니다.

```jsx
const array = [1, 2, 3, 4, 5];
console.log(array.join()); // 1,2,3,4,5
console.log(array.join(' ')); // 1 2 3 4 5
console.log(array.join(', ')); // 1, 2, 3, 4, 5
```

## 10. reduce

배열의 각 요소에 대해 주어진 리듀서(reducer) 함수를 실행하고, 하나의 결과값을 반환합니다. 앞의 문장만 읽어서는 이해하기 어려운데, 내가 지정해준 함수를 실행 후 나온 결과값을 다시 파라미터로 사용하도록 합니다. 아래 예를 통해 이해해봅시다.

```jsx
// 기존 방식
const numbers = [1, 2, 3, 4, 5];

let sum = 0;
numbers.forEach(n => {
  sum += n;
});
console.log(sum);  //15

//reduce를 사용하는 방식
const numbers = [1, 2, 3, 4, 5];
let sum = array.reduce((accumulator, current) => accumulator + current, 0);

console.log(sum);  //15
const numbers = [1, 2, 3, 4, 5];
let sum = numbers.reduce((accumulator, current) => {
  console.log({ accumulator, current });
  return accumulator + current;
}, 0);

console.log(sum);

// 결과
{ accumulator: 0, current: 1 }
{ accumulator: 1, current: 2 }
{ accumulator: 3, current: 3 }
{ accumulator: 6, current: 4 }
{ accumulator: 10, current: 5 }
15
```



---

**references**

[LearnJS GitBook](https://learnjs.vlpt.us/basics/09-array-functions.html)