---
title: Swift 코테문제 풀이
categories:
  - SWIFTUI 
excerpt: "Swift로 코딩테스트 문제를 풀어보자:)"
date: 2022-07-31
tags:
- SwiftUI
---



# 개요

개발자를 준비한다면 필수적인 코딩테스트,,,

나는 iOS개발자가 되고 싶으니깐 swift로 코테준비해야겠다.

굳이 다른언어로 할 필요가 없으니...

<br />
<br />

---

# 알고리즘에 필요한 지식

---

<br />


## 사용자 입력받기

---

`readline()`하면 scanf와 같은 기능을 수행한다. readline의 리턴 타입은 String?이다.

`타입(readLine()!)!`을 사용하면 특정 타입으로 바로 받아올 수 있다.

`components(seperatedBy:" ")`와 `split(separator:)`수식어로 입력을 구분자를 기준으로 split해서 저장할 수 있다.

둘의 차이점으로는 components는 리턴값이 [String]이고 split은 리턴값이 [String.SubSequence]다


<br />

---

## 옵셔널 프린트

---

옵셔널 변수를 출력하면 `Optional(값)`이다. 그리고 `expression implicitly coerced from 'String?' to 'Any'`이라는 경고가 뜬다.

경고가 뜨게하기 싫으면 `as Any`로 캐스팅을 해주면 Optional(값)이 뜬다.

값만 출력하고 싶다면 다음 3가지 방법을 사용하면된다.

* Optional 바인딩
* !로 강제 값 추출
* ??로 nil값일 때 출력값 지정

<br />

---

## 빈배열 만들기

---

```swift
var emptyArray : [Int] = []
```

<br />

---

## 배열 0으로 초기화

---

꼭 숫자 아니어도 됨

"0"과 같이 Character형으로 줘도 된다.

```swift
var arr = Array(repeating: 0, count: 5)
```

<br />

---

## 이차원 배열 0으로 초기화

---

```swift
let arr2: [[Int]] = Array(repeating:Array(repeating:0, count: 5), count: 3)
```

<br />

---

## 배열 정렬

---

```swift
arr.sorted() // 오름차순
arr.sorted(by: >) // 내림차순 call by value
arr.sort() // call by reference
```


<br />

---

## 배열 역순

---

```swift
arr.reverse() // call by reference
arr.reversed()
```

<br />

---

## 배열 값 추가

---

```swift
arr.insert(10, at: 1) // 인덱스 1에 추가 
arr.append(0) // 맨뒤에 추가
```


<br />

---

## 배열 값 제거

---

```swift
arr.remove(at: 0) // at은 인덱스
arr.removeFirst() //맨앞에거 제거
arr.removeLast() // 맨뒤에거 제거
arr.removeAll() // 모두 제거
```


<br />

---

## 문자열 합치기

---


```swift
str.joined() // separator로 구분자 넣어줄 수 있음
str[0] + str[1]
```

<br />

---

## 문자열 치환

---

```swift
str.replacingOccurrences(of:, with:) // of를 with로 치환
```

<br />

---

## 문자열에서 문자 찾기

---

```swift
str.firstIndex(of: "a") // 못찾으면 nil
str.index(firstOf: "a")

```

<br />

---

## 문자열에서 특정 인덱스 접근

---

```swift
str.startIndex // 첫번째
str.index(str.startIndex, offsetBy: 1) // 두번째
str.index(before: str.endIndex) // 마지막
```


<br />
<br />

---

# 프로그래머스

---

<br />

## Level1

---

<br />
<br />


### 신고결과받기

---

#### -> [예제 코드](https://github.com/dq-qqq/SwiftUI_Example/tree/main/stack) <-
