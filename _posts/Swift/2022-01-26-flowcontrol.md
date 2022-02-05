---
title: 스위프트의 흐름제어
categories:
  - SWIFT
excerpt: "스위프트에서의 조건문과 반복문을 공부해보자:)"
date: 2022-01-26 17:57
tags:
- iOS
- swift
---


# 개요

---

애플 공식 문서에서 조건문과 반복문을 다루는 부분의 이름이 Control Flow이다. 직역해서 흐름제어로 얘기하겠다.



<br />
<br />

---

# 조건문

---

조건문으로는 `if`와 `switch`가 있다. swift에만 있는 `guard` 구문이 있다.

C언어와 다른점으로는 소괄호가 없어도 된다는 것과 중괄호 후의 else 위치 정도이다.


<br />

---

## if

---

```swift
var temperature: Int = 0
if temperature < 10 {
  print("cold")
} else if temperature > 30 {
  print("hot")
} else
  print("good")
```

<br />

---

## switch

---

break는 선택사항이다.

break를 하지 않고 그다음 case문을 쓰고 싶다면 `fallthrough`를 사용한다.

```swift
var temperature: Int = 0
switch temperature {
case ..<10:
  print("cold")
case 10...30:
  print("good")
default:
  print("hot")
```

<br />

---

## guard

---

`quard`키워드 뒤에오는 조건문이 참일 때만 뒤의 코드가 실행된다.

false일 경우는 코드 흐름을 빠져나가는 return, break, continue, throw와 같은 키워드가 있어야한다.

guard 안에서 선언된 변수는 그 구문이 끝나도 유효하다.

```swift
func hi(name: String?) {
  guard let person = name, person != "kyujin" else {
    print("he is not kyujin")
    return
}

let result = "he is kyujin"
print(result)
```

<br />
<br />

---

# 반복문

---

for은 C언어와 다르다. 

while은 비슷하다.

do-while은 reapet-while로 사용할 수 있다.

C언어에서도 do-while은 잘안썻다.

<br />

---

# for-in

---

```swift

number: for i in 0...5 {
  print(i)
}

numebr2: while i < 5 {
  i += 1
  print(i)
}


let exFor: [String, Int] = ["kyujin": 25, "yunjin": 22]
for (name, age) in exFor {
  print("hello my name is \(name), age is \(age)")
}

var result: Int = 1
for _ in 1...3 {
  result *= 10 // 1000
}
