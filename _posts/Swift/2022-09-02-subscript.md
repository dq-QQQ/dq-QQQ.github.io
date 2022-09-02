---
title: 스위프트 서브스크립트
categories:
  - SWIFT
excerpt: "스위프트의 서브스크립트를 공부해보자:)"
date: 2022-09-02
tags:
- iOS
- swift
---

# 개요


스위프트에서 처음본 서브스크립트 문법.

이게 뭘까?

<br />
<br />

---

# 서브스크립트

---

서브스크립트는 []와 첨자를 이용해서 인스턴스 속성에 접근할 수 있는 문법이다.

```swift
subscript(parameter) -> return {
  get {
  }
  set {
  }
}
```

서브스크립트는 클래스, 구조체, 열거형에서 사용할 수 있다. 서브스크립트는 이름없는 메소드로 볼 수 있다.

get은 필수 set은 낫 필수

파라메터 목록은 서브스크립트 문법으로 접근할 때 []사이에 전달하는 서브스크립트의 수와 자료형을 지정한다. 일반적으로 하나.

얘도 타입 서브스크립트라고 전역적으로 사용가능하게 할 수 있다.

<br />
<br />

---

# 예시

---

```swift
class HeadQuarters {
  private var squad: [SuperHero]
  
  init(heroes: [SuperHero]) {
    squad = heroes
  }
  
  subscript(index: Int) -> SuperHero? {
    get {
      if index < squad.count {
        return squad[index]
      }
      return nil
    }
    set {
      if let hero = newValue {
        if index < squad.count {
          squad[index] = hero
        } else {
          squad.append(hero)
        }
      } else {
      if index < squad.count {
       squad.remove(at: index)
      }
    } 
}
```
