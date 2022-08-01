---
title: SwiftUI 운영체제와 버전 제한
categories:
  - SWIFTUI 
excerpt: "SwiftUI에서 운영체제와 OS 버전에 따라 코드를 작성해보자:)"
date: 2022-02-18
tags:
- SwiftUI
---



# 개요

SwiftUI에서는 특정 운영체제, 특정 운영체제 버전에서만 가능한 것들이 있다.

iOS13에서는 되는게 16에서는 안될 수가 있고 macOS에는 되는데 iOS는 안되는것이 있다.

그럼 버전별로 코드를 다르게 짜야하는데 방법을 알아보겠다.


<br />
<br />

---

# #available

---


코드안에서 특정 변수나 함수등을 분기하고 싶다면 이걸 사용하면 된다.

아래의 코드는 alert를 예시로 들었다.

iOS 15를 기준으로 사용법이 달라졌기에 이런식으로 코드를 분기해서 짰다.

```swift
if #available(iOS 15, *) {
            wholeView
            .alert(Text("주문 확인"), isPresented: $showingAlert, actions: {
                Button("취소") { }
                Button("확인") { orderViewModel.placeOrder(product: product, quantity: quantity) }
            }, message: {
                Text("진짜 구매하시겠습니까")
            })
        } else {
            wholeView
                .alert(isPresented: $showingAlert) {
                    Alert(title: Text("주문 확인"), message: Text("진짜 구매하시겠습니까"), primaryButton: .default(Text("확인"), action: {}), secondaryButton: .cancel(Text("취소")))
                }
        }
```

<br />
<br />

---

# @available

---

@available은 코드 안에서 분기하기 위해서가아닌 함수, 클래스, 구조체, 프로토콜등의 앞에서 그것의 사용을 제한한다.

```swift
@available
class ho {
    ~~~
}
```

<br />
<br />

---

# if & endif

---

전처리로 운영체제를 제한할 수 있다.

```swift
#if os(iOS)
  print("ios에서만 할 코드")
#elseif os(macOS)
  print("macOS에서만 할 코드")
#elseif os(watchOS)
  print("wathOS에서만 할 코드")
  #endif
```

  