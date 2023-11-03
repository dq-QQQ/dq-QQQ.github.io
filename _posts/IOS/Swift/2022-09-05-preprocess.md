---
title: 스위프트의 전처리
categories:
  - SWIFT
excerpt: "스위프트에서 전처리를 해보자:)"
date: 2022-09-05
tags:
- iOS
- swift
---



# 개요

---

컴파일 하기 전에 처리되는 전처리문을 사용해보겠다.


<br />
<br />

---

# 전처리

---

컴파일러가 소스 코드를 컴파일 하기 전에 전처리 명령문을 처리하는 것을 말한다.

Objective-C 컴파일러는 전처리기를 내장하고 있으나 Swift 컴파일러는 전처리기를 내장하고 있지 않다.

따라서 컴파일 속성, 조건 컴파일 블록과 언어 자체 기능으로 처리한다.

```swift
#if condition
    statement
#endif
```

swift는 플랫폼 상태 함수를 제공하며 다음과 같다.

<br />
<br />

---

# os()

---

컴파일 되는 운영체제를 말한다.

파라메터로 전달할 수 있는 값은 `OSX`, `macOS`, `iOS`, `tvOS`, `watchOS`, `Linux`이다.

```swift
#if os(OSX) || os(macOS)
    print("macBook")
#elseif os(iOS)
    print("iPhone")
#endif
```

<br />
<br />

---

# arch()

---

컴파일 되는 플랫폼을 말한다.

파라메터로 전달할 수 있는 값은 `x86_64`, `arm`, `arm64`, `i386`이다.


```swift
#if arch(x86_64)
    print("intel mac")
#elseif arch(arm)
    print("M1 mac")
#endif
```

<br />
<br />

---

# swift()

---

컴파일 되는 swift 버전을 말한다.

파라메터로 >=연산자와 버전 번호를 전달한다.


```swift
#if swift(>=4.0)
    print("swift4")
#elseif swift(3.0)
    print("swift3")
#endif
```
