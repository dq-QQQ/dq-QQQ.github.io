---
title: SwiftUI ObservableObject
categories:
  - SWIFTUI 
excerpt: "SwiftUI의 ObservableObject에 대해 공부해보자:)"
date: 2022-07-21
tags:
- SwiftUI
---



# 개요

SwiftUI의 뷰모델에서 많이 사용하는 ObservableObject에 대해서 알아보겠다.

[애플 공식문서](https://developer.apple.com/documentation/combine/observableobject)

<br />
<br />

---

# ObservableObject

---

```swift
class Contact: ObservableObject {
    @Published var name: String
    @Published var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    func haveBirthday() -> Int {
        age += 1
        return age
    }
}

@ObservableObject let john = Contact(name: "John Appleseed", age: 24)
cancellable = john.objectWillChange
    .sink { _ in
        print("\(john.age) will change")
}
print(john.haveBirthday())
// Prints "24 will change"
// Prints "25"
```

애플에서 제공한 위의 예시를 보면 class에서 @published와 ObservableObject가 특이하게 보인다.

ObservableObject로 선언된 클래스는 objectWillChange를 사용할 수 있다. 이름으로 알 수 있듯이 send를 이용해서 바뀌는 프로퍼티를 알려준다.

이것을 일일이 안해주려면 @published로 선언하면 된다. 그러면 값이 바뀌면 자동으로 알려준다.

그리고 해당 클래스를 ObservableObject로 선언하면 된다.
