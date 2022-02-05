---
title: 자바스크립트 비동기의 꽃 async await 초스피드로 핵심만 체크
date: 2021-08-17 23:18:01
permalink: /:short_year-:month-:day/:title
categories: [frontend, web/network]
tags: [javascript, async, 비동기]
---

# 자바스크립트 비동기의 꽃 async await 초스피드로 알아보기

## :bulb: 핵심 체크 문답

### :one: asnyc await란? 

 자바스크립트 비동기 함수의 가독성을 높여주는 문법



### :two: async await의 장점은?

Promise 보다 **<u>간결</u>**하고 **<u>직관적</u>**이며 **<u>높은 가독성을 보여주는 장점</u>**이 있다.



### :three: Promise를 대체하는가?

**:no_good: NO!**   ***promise를 완전히 대체하지는 못한다***.

promise는 값으로 존재하여 더 다양한 범위에서 활용되는 반면, **<u>async await은 함수를 정의할 때에만 사용된다</u>**는 점에서 활용 범위가 promise보다는 작다.

async 함수의 반환값은 항상 `Promise`객체이다. 이 Promise객체는 **<u>상태와 반환값</u>**이 포함되어있다.



## :bulb: async await 병렬처리

```javascript
function asyncFunc1() {
    return new Promise(resolve => {
        console.log('처리중 1');
        setTimeout(() => {
            resolve(10);
        }, 1000)
    })
}
function asyncFunc2() {
    return new Promise(resolve => {
        console.log('처리중 2');
        setTimeout(() => {
            resolve(20);
        }, 1000)
    })
}

// 병렬처리 (O)
async function getData() {
    const p1 = asuncFunc1();
    const p2 = asyncFunc2();
    const data1 = await p1;
    const data2 = await p2;
    console.log({data1, data2});
} // 1초 후에 LOG: '처리중 1', '처리중 2'

// 병렬처리 (X)
async function getData() {
    const data1 = await asuncFunc1();
    const data2 = await asyncFunc2();
    console.log({data1, data2});
} // 1초 후에 LOG:: '처리중 1', 2초 후에 LOG:: '처리중 2'
```

- 병렬처리를 진행한 예를 보면 1초에 data1과 data2의 로그를 모두 볼 수 있다.
- 하지만 병렬처리를 진행하지 않은 예시처럼 코드를 작성하면 1초를 써서 data1을 받아오고 그 다음 또 다시 1초를 data2에 사용하기 때문에 총 2초가 걸리는 비효율이 발생한다.

---

Ref.

실전 자바스크립트 - 이재승