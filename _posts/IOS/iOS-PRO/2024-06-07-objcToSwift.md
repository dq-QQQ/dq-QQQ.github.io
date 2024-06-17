---
title: Obj-C To Swift
date: 2024-06-07
excerpt: "Obj-C 프로젝트를 SwiftUI 프로젝트로 전환하자!"
categories:
- iOS
tags:
- iOS-PRO
---




# 개요

우리 제품 중 프레임워크가 있다.

그 프레임워크는 Obj-C / UIKit으로 구현되어있다.

근데 js가 많이 관여되어있어서 js도 알아야할듯

간단하게 말해 웹(js)에서 네이티브(swift) 뷰어 통제할 수 있어야한다.

구현하는데 필요한 정보와 트러블 슈팅. 여기에 적어보겠다.

<br />

---


# 궁금증

-   현재 objc 프로젝트에서 swift로 바꿔나가야할지? OR SwiftUI 프로젝트를 만들고 objc를 가져오는 식으로 해야할지?
-   이건 앱이 아니라 프레임워크이다. MVVM이니 TCA니 의미가 있나?
-   프레임워크이다. 뷰나 API들의 트리거가 언제되냐가 중요한데 UIKit랑 SwiftUI중에 어떤게 나으려나...
-   API이다. 그럼 .h같은 것이나 인터페이스는 어떻게 제공하지...?
-   API이다. 근데 같은 Swift에서 쓰는게 아니라 js에서 호출되어야한다. 뭐지,,?? 이게 어캐되는거지
-   SwiftUI로 만든 프레임워크를 모든 프로젝트에서 쓸 수 있나? SwiftUI로 햇을때의 장점이뭐지
-   기술스택을 어떻게 하지 UIKit? SwiftUI? Combine? RX? 또 머있지
-   ObjC 프레임워크를 Swift 프레임워크 만들 때 사용해야하는데 어캐하지
-   