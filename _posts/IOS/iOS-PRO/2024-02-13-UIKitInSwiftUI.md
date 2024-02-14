---
title: SwiftUI에서 UIKit 사용하기
date: 2024-02-13
excerpt: "SwiftUI에서 UIKit을 사용해보자:)"
categories:
- iOS
tags:
- iOS-PRO
---



# 개요

스유는 불완전하다. 아직도 업데이트중이다.

UIKit의 뷰, 뷰컨을 스유에서 사용해야하는 경우가 있다.

그 방법에 대해 알아보겠다.


<br />

---


# 언제 사용하나??

당장 독사 프로젝트에서도 qr 스캐너 만들 때, pdfkit을 사용할 때, 네비게이션바의 색을 바꿀 때에 사용한다.

-   SwiftUI가 지원하지 않는 컴포넌트일 때
    -   UIImagePickerController같은 경우
-   import한 라이브러리가 UIKit 기반일 때
    -   AVKit, PDFKit같은 경우
-   커스터마이징
    -   네비게이션 바의 색을 바꿀 경우
-   UIKit과 SwiftUI를 혼용할 때

등등등...


<br />

---

# 어떻게 사용하나??

-   UIView -> UIViewRepresentable 채택
    -   UIButton, UILabel, UIImageView와 같은 단일 뷰
-   UIViewController -> UIViewControllerRepresentable 채택
    -   UINAvigationController, UIImagePickerController와 같은 뷰컨트롤러

<br />

## UIViewRepresentable

```swift
@available(iOS 13.0, tvOS 13.0, *)
@available(macOS, unavailable)
@available(watchOS, unavailable)
public protocol UIViewRepresentable : View where Self.Body == Never {
  associatedtype UIViewType : UIView
  
  @MainActor 
  func makeUIView(context: Self.Context) -> Self.UIViewType
  
  @MainActor 
  func updateUIView(_ uiView: Self.UIViewType, context: Self.Context)
  
  @MainActor 
  static func dismantleUIView(_ uiView: Self.UIViewType, coordinator: Self.Coordinator)
  
  associatedtype Coordinator = Void
  
  @MainActor 
  func makeCoordinator() -> Self.Coordinator
  
  @available(iOS 16.0, tvOS 16.0, *)
  @MainActor
  func sizeThatFits(_ proposal: ProposedViewSize, uiView: Self.UIViewType, context: Self.Context) -> CGSize?


  typealias Context = UIViewRepresentableContext<Self>

  @available(iOS 17.0, tvOS 17.0, *)
  typealias LayoutOptions
}
```

-   이 프로토콜을 채택한 구조체는 View의 속성을 가지며 SwiftUI의 뷰처럼 다룰 수 있음
-   해당 구조체 안에서 뷰의 생성과 업데이트, tear down(스유 뷰 계층에서 나온다는 말인듯)할 수 있음
-   SwiftUI -> UIKit으로의 데이터 흐름은 @Binding으로 가능
    -   이 구조체 안에서 스유에서 바뀌는 데이터를 감지하고 ReadOnly임
-   UIKit -> SwiftUI의 데이터 흐름은 Coordinator로 가능
-   makeUIView, updateUIView 이 두개의 메서드를 필수 구현해야함


<br />

### makeUIView

-   뷰의 객체를 생성하고 초기화하는 메서드로 만들어질 때 한번만 호출됨
-   `context` 파라메터는 뷰가 생성될 때 시스템이 호출함
-   UIKit 뷰를 리턴함

<br />

### updateUIView

-   앱의 상태가 바뀌면 SwiftUI는 그 변화에 영향을 받는 UI를 업데이트 시킴
-   SwiftUI가 관리하는 뷰에 대응하는 UIView로 makeUIView의 리턴값


<br />

### dismantleUIView

-   deinit과 같은 역할로 자동으로 생성됨

<br />

### makeCoordinator

-   UIView의 이벤트 처리
-   SwiftUI로의 데이터 전달
-   Corrdinator 클래스를 구현해야함


<br />

### UIViewRepresentableContext

-   UIKit뷰를 생성하고 업데이트하는 시스템의 상태를 담고 있는 정보
-   coordinator, transaction, environment의 데이터를 담고 잇음




<br />

### 예시

```swift
import SwiftUI
import UIKit

struct MyButton: UIViewRepresentable {
    typealias UIViewType = UIButton
    
    @Binding var buttonText: String
    
    func makeUIView(context: Context) -> UIButton {
        let button = UIButton(type: .system)
        button.setTitle(buttonText, for: .normal)
        button.addTarget(context.coordinator, action: #selector(Coordinator.buttonTapped), for: .touchUpInside)
        return button
    }
    
    func updateUIView(_ uiView: UIButton, context: Context) {
        uiView.setTitle(buttonText, for: .normal)
    }
    
    func makeCoordinator() -> Coordinator {
        Coordinator(buttonText: $buttonText)
    }
    
    class Coordinator: NSObject {
        @Binding var buttonText: String
        
        init(buttonText: Binding<String>) {
            _buttonText = buttonText
        }
        
        @objc func buttonTapped() {
            print("Button tapped!")
            buttonText = "Button Tapped!"
        }
    }
}

struct ContentView: View {
    @State private var buttonText = "Tap me"
    
    var body: some View {
        VStack {
            Text("Button text: \(buttonText)")
            MyButton(buttonText: $buttonText)
        }
    }
}
```




<br />

## UIViewControllerRepresentable

-   프로토콜 개념과 사용법, 필수 구현 목록은 UIViewRepresentable과 같음
-   [UIKit의 생명주기를 사용하고 싶을 때 사용](https://doing-programming.tistory.com/entry/SwiftUI-SwiftUI-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C-ViewController-Life-Cycle-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)

