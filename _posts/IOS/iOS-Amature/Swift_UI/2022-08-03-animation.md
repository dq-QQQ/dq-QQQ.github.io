---
title: SwiftUI 애니메이션
categories:
  - SWIFTUI 
excerpt: "SwiftUI의 애니메이션에 대해서 공부해보자:)"
date: 2022-08-03
tags:
- SwiftUI
---



# 개요

SwiftUI에서 애니메이션에 대해서 알아보고 사용법을 익혀보겠다.

[애플 공식문서](https://developer.apple.com/documentation/swiftui/animation)


<br />
<br />

---

# animation

---

`@frozen struct Animation`

화면상에서 정적인 시각적 요소들에 동적인 움직임을 부여한다.

애니메이션은 평소의 상태, 트리거가 발동한 상태, 애니메이션 동작이 끝난 상태로 나눌수 있다.

트리거는 사용자의 터치등이 있겠다.

ios15버전 이전은 이전에 반영된 뷰를 꾸미는 modifier에 대해서 `.animation(.default)`를 사용하면된다.

ios15부터는 `withAnimation()`을 사용하라고 한다.

```swift
func withAnimation<Result>(
    _ animation: Animation? = .default,
    _ body: () throws -> Result
) rethrows -> Result
```

animation 옵션을 지정할 수 있다.

```swift
@State private var blur: Bool = false
//~iOS14
Image("cat")
    .blur(radius: blur ? 5 : 0)
    .animation(.default)
    .ontapGesture {
        self.blur.toggle()
    }
//iOS15~
Image(systemName: "house")
            .blur(radius: selected ? 5 : 0)
            .onTapGesture {
                withAnimation {
                    self.selected.toggle()
                }
            }
```

<br />
<br />

---

# animation 종류

---

* `.default` : 기본값, easeInOut 유형이 사용됨 0.35동안 지속
* `.linear` : 일정한 속도로 애니메이션
* `.easeIn` : 첨에는 느리게 점점 빠르게. 밖으로 사라지는 뷰에 사용
* `.easeOut` : 첨엔 빠르게 뒤엔 느리게
* `.easeInOut` : 첨, 뒤엔 느리게, 중간은 빠르게 가장 일반적
* `timingCurve`: 커스텀 애니메이션
* `spring` : 커스텀 애니메이션



<br />
<br />

---

# animation 제어

---

* `.delay` : Double값을 매개변수로 받아 그 값만큼 지연
* `.speed` : 매개변수로 Double넣으면 애니메이션 스피드 조절
* `.repeatCount` : 매개변수로 Int값 넣으면 애니메이션을 일정횟수만큼 반복
* `.repeatForever` : 매개변수로 true 넣으면 애니메이션을 무한반복


<br />
<br />

---

# 트랜지션

---

뷰 계층 구조에 새로운 뷰가 추가되거나 기존에 있던 것이 제거될 때 적용되는 애니메이션의 한 종류

트랜지션은 뷰의 계층구조 변화만 일어나는 것이 아니라 동적인 움직임을 표현하기에 애니메이션이랑 같이 쓰임

버튼을 누르면 Transition이라는 글자가 생기고 사라진다. 

이것은 AnyTransition.opacity가 적용된 트랜지션이라고 말할 수 있다.

```swift
@State private var showText = false
    
var body: some View {
    VStack {
    if showText {
        Text("Transition")
        .font(.largeTitle)
        .padding()
    }
        
    Button("Display Text On / Off") {
        withAnimation {
        self.showText.toggle()
        }
    }.font(.title)
    }
}
```

<br />

---

# 트랜지션 종류

---

* `opacity` : 투명도 조절. 생겼다가 사라졌다가 하는 기본값
* `scale` : 뷰의 배율조절
* `slide` : 밀어서 잠금해제
* `move` : 특정방향에서 뷰가 나타났다가 그 방향으로 다시 사라짐
* `offset` : 특정 위치로 움직이고 사라짐


<br />

---

# Animatable 프로토콜

---

```swift
protocol Animatable {
    associatedtype AnimatableData: VectorArithmetic
    var animatableData: Self.AnimatableData { get set }
}
```

이 프로토콜은 애니메이션 다음동작인 animatableData를 필수로 구현해야한다.

그럼 이 값들이 연속적으로 이어지면서 애니메이션이 된다.

Shape 프로토콜은 이 프로토콜을 채택하고 있고 보통 도형들로 애니메이션을 할 때는 자동으로 채택되어있다.