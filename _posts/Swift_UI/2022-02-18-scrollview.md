---
title: SwiftUI ScrollView
categories:
  - SWIFTUI 
excerpt: "SwiftUI의 ScrollView에 대해서 공부해보자:)"
date: 2022-02-18
tags:
- SwiftUI
---



# 개요

SwiftUI에서 ScrollView에 대해서 알아보고 사용법을 익혀보겠다.

[애플 공식문서](https://developer.apple.com/documentation/swiftui/scrollview)


<br />
<br />

---

# ScrollView

---

ScrollView는 자신의 크기보다 더 큰 크기의 컨텐츠를 담아야 할 경우 스크롤을 통해 표현하는 컨테이너 뷰이다.


<br />

---

# 생성자

---

`init(_ axes: Axis.Set = .vertical, showsIndicators: Bool = true, content: () -> Content)`

* `axes` : 스크롤 뷰의 축. 기본은 세로
* `showsIndicators` : 옆에 스크롤 인디케이터

```swift
var body: some View {
    ScrollView {
        VStack(alignment: .leading) {
            ForEach(0..<100) {
                Text("Row \($0)")
            }
        }
    }
}
```

