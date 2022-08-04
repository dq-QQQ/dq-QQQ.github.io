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

스크롤


<br />

---

# 생성자

---

`init(_ axes: Axis.Set = .vertical, showsIndicators: Bool = true, content: () -> Content)`

* `axes` : 스크롤 뷰의 축. 기본은 세로
* `showsIndicators` : 옆에 스크롤 인디케이터, 디폴트는 true
* `content` : 스크롤 할 수 있는 뷰를 만드는 view builder

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


<br />

---

# 스크롤 뷰의 콘텐츠 크기

---

스크롤 뷰는 뷰의 크기 내에서 다 표현할 수 없는 콘텐츠도 스크롤을 통해 콘텐츠의 크기를 모두 표현할 수 있다.

텍스트나 버튼과 같이 확장성이 없는 뷰는 자신의 크기를 그대로 표현한다.

그러나 Color, Rectangle과 같이 크기를 지정하지 않으면 가능한 최대 크기로 확장하려는 속성을 가진 뷰는 어디까지 표현해야할 지 모른다.

그래서 `frame(idealWidth: ,idealHeight: `를 이용해서 조절한다.

ideal~는 개별적인 크기로 넣어도 ideal~의 크기를 모두 더하고 뷰의 개수만큼 나눈다.

<br />
<br />

---

# 스크롤뷰에서 콘텐츠 위치 조정

---

UIScrollView에서는 콘텐츠의 위치를 다루기 위해 ContentOffset을 이용한다.

그런데 ScrollView에서는 이 값을 제공하지 않으므로 자식뷰에서 부모뷰에 데이터를 전달할 수 있는 기능인 `PreferenceKey`를 이용하거나 스크롤뷰 내부에 `GeometryReader`의 글로벌 좌표를 이용한다.

```swift
ScrollView {
    GeometryReader {
        Rectangle()
            .fill(self.color(from: $0))
    }
    .frame(width: 150, height: 150)
}

func color(from proxy: GeometryProxy) -> Color {
    let yOffset = proxy.frame(in: .global).minY - 44
    let color  = min(1, 0.2 + Double(yOffset / 1000))
    return Color(hue: color, saturation: color, brightness: color)
}
```

GeometryProxy에서 .global 좌표를 기준으로 프레임 정보를 얻는다.

각 기기의 safeAreaInsets.top 값을 빼줘야 스크롤뷰를 기준으로 배치한다.


<br />
<br />

---

# 스크롤뷰 페이징

---

가로로 스크롤 하는 건 어따 써먹나 했는데 페이징에 많이 사용될듯하다.

`.onAppear{ UIScrollView.appearance().isPagingEnabled = true}`를 사용하면된다.

옆으로 스크롤을 부드럽게가 아니라 페이지를 하나하나 넘기는 것처럼 할 수 있다.


```swift
let colors: [Color] = [.red, .green, .blue]
    
    var body: some View {
        GeometryReader { proxy in
            ScrollView(.horizontal) {
                HStack() {
                    ForEach(colors.indices) { index in
                        Circle()
                            .fill(colors[index])
                            .overlay(Text("\(index)"))
                    }
                    .frame(width: proxy.size.width, height: proxy.size.height)
                }
            }
            .onAppear{ UIScrollView.appearance().isPagingEnabled = true} // 페이징 온
        }
    }
```