---
title: javascript 즉시실행함수(?) 일단 알아보자
date: 2021-09-16 23:18:01
permalink: /:short_year-:month-:day/:title
categories: [frontend, web/network]
tags: [javascript, 즉시실행함수]
---

# javascript 즉시실행함수란 무엇일까

> 즉시실행함수: 함수선언과 동시에 바로 실행이 되는 함수.

javascript는 일회성으로 사용되는 함수가 다른 언어에 비해 많은 편인데, 이를 효율적으로 진행하기 위해`익명함수`, `즉시실행함수` 등을 지원합니다.

당연히 단 한 번만 호출되고 실행됩니다.



## 즉시실행함수

```javascript
// 일반함수

function normal() {
    console.log('Hello World!');
}
normal();
```

```javascript
// 즉시실행함수 - 이름이 있으므로 "기명즉시실행함수"라고도 불린다.
(function immediate(){
    console.log('URGENT!!')
})();
```

위의 예시에서 보듯이 함수선언부분 전체를 괄호로 감싸고 그 뒤에 () 를 붙여서 바로 실행하도록 합니다.

사실 한 번만 호출되고 더 이상 호출되지 않기 때문에 함수의 이름이 필요하지 않습니다. 따라서 다음과 같이 쓸 수 있습니다.

```javascript
// Anonymous function - 이름이 없으므로 "익명즉시실행함수"라고도 불린다.
(function (){
    console.log('URGENT!!')
})();

// ES6
(()=> {console.log('URGENT!!')})();
```

일반적으로 즉시실행함수는 어차피 실행 선언 후 바로 사용되고 다시 사용되지 않으므로 ***익명함수***로 많이 쓰입니다.

하지만 ***기명함수***로 쓰이는 경우도 있는데, 바로 재귀함수입니다. 자기 자신을 다시 호출해야 하는데 이름이 없으면 호출할 수가 없으므로 재귀함수에서는 이름을 지어서 활용합니다.



### 함수 인자(arguments)는 어떻게 활용할까?

```javascript
(function sum(a, b){
    console.log(`The answer is ${a+b}`)
})(3, 5)
// "The answer is 8"


(function (arr){
    arr.map((item) => {
        console.log(item)
    })
})(["Hello", "World", "!"])
// "Hello"
// "World"
// "!" 
```

아래 예시와 같이 함수뒤에 붙여주는 괄호안에 인자를 넣어주면 즉시실행함수 내부에서 활용할 수 있다.

지금은 숫자 자료형을 넣어줬지만 배열도 가능합니다.


