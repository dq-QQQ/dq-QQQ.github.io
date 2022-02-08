---
title: SwiftUI 네비게이션 뷰
categories:
  - SWIFTUI 
excerpt: "SwiftUI의 네비게이션 뷰에 대해서 공부해보자:)"
date: 2022-02-08
tags:
- SwiftUI
---



# 개요

어플에서 네비게이션 뷰를 추가하는 방법에 대해서 알아보겠다.


[애플 공식문서](https://developer.apple.com/documentation/swiftui/navigationview)

<br />
<br />

---

# 네비게이션 뷰

---

네비게이션 스택을 이요해 컨텐츠 뷰들을 관리하는 컨테이너 뷰이다.

스택 구조의 네비게이션 계층을 구성하고 화면을 전환하는등 UI를 구성할 때 사용한다.


```swift
NavigationView {
  Image("SwiftUI")
}
```

<br />

---

## NavigationBarTitle

---

`NavigationBarTitle`수식어를 사용해서 제목을 추가해 줄 수 있다. 

매개변수로 제목에 적을 내용과 `displayMode`를 지정해 줄 수 있는데 기본값으로 할거면 생략해도 된다.

모드 종류로는 `.large`와 `.inline`이 있다.

```swift
NavigationView {
  Image("SwiftUI")
    .navigationBarTitle("내비게이션 바 타이틀")
}
```

<br />

---

## NavigationBarItems

---

`NavigationBarItems`수식어를 사용해서 아이템을 추가해 줄 수 있다. 

앱에 보면 설정 아이템이나 공유 아이템같은게 있다. 그런거 추가해주는 수식어이다.

매개변수로 leading은 앞쪽에 넣을 아이템 trailing에는 뒤쪽에 넣을 아이템을 넣으면 된다.

```swift
let trailingItem = HStack {
                      Button(action: { print("noitification") }) {
                        Image(systemName: "bell").imageScale(.large)
                      }
                      Button(action: { print("setting") }) {
                        Image(systemName: "gear").imageScale(.large)
                      }
                   }
return NavigationView {
  Image("SwiftUI")
    .navigationBarItems(trailing: trailingItem)
}
```

<br />

---

## NavigationLink

---

지정한 목적지로 이동할 수 있도록 만들어진 버튼으로, 뷰를 눌렀을 때 화면을 전환하는 기능이다.

```swift
NavigationLink(destination: Text("Destination View")) {
  Image("SwiftUI")
}
.navigationBarTitle("
