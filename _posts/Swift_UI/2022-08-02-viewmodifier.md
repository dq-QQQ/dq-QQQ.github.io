---
title: SwiftUI ViewModifier
categories:
  - SWIFTUI 
excerpt: "SwiftUI의 ViewModifier에 대해 알아보자:)"
date: 2022-08-02
tags:
- SwiftUI
---



# 개요


SwiftUI에서 modifier는 뷰를 수식해줄 때 사용한다.

내가 커스텀해서 사용할 수 있는데 ViewModifier라고 한다.

[애플공식문서](https://developer.apple.com/documentation/swiftui/viewmodifier)

<br />
<br />

---

# ViewModifier

---

```swift
protocol ViewModifier {
    associatedtype Body: View
    func body(content: Self.Content) -> self.Body
    typealias Content
}
```

만약 뷰에 자주 적용되는 modifier를 세팅하고 싶을 때 유용하다.

아래의 코드처럼 들어오는 content에 따라 커스텀 수정자를 붙여준다.

커스텀 수정자는 ViewModifier 프로토콜을 따르는 구조체로 선언된다.

그러므로 필요한 곳에서 modifier() 메서드를 통해 적용할 수 있다.

```swift
struct StandardTitle: ViewModifier {
  func body(content: Content) -> some View {
    content
      .font(.largeTitle)
      .background(Color.white)
  }
}

Text("text")
  .modifier(StandardTitle())
```

<br />
<br />

---

# concat

---

두개의 ViewModifier를 하나로 합쳐서 사용할 수 있다.

`func concat<T>(_ modifier: T) -> ModifiedContent<Self, T>`


```swift
//위의 ViewModifier와 같은이름2가 있다고 생각해보자
Text("text")
    .modifier(StandardTitle()).concat(StandardTitle2())
```
