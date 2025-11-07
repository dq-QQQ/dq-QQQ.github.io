---
title: ios 렌더링
date: 2025-11-03
excerpt: "uikit과 swiftui 렌더링 방식"
categories:
- iOS
tags:
- iOS-PRO
---




# 개요

실무를 하다보면 uiview나 일반적인 swiftui 뷰로 안될때가 있다.

CG나 CA를 이용하거나 하는데 알아보겠다.

일단 사전지식부터


<br />

---

# 벡터 vs 비트맵

- 백터는 데이터가 아니라 명령을 가지고있음(여기서부터 저기까지 선을 그려라)
- 비트맵은 정사각형의 픽셀을 기반으로 데이터를 가지고 있음(래스터라고도 명칭함)
- 따라서 벡터를 기반으로 비트맵을 생성하는것을 래스터라이징이라고 함



<br />

---

# Immediate Mode vs Retained Mode

GPU가 이해할 수 있는 수준(계속반복해야하면 대충 맞음)의 명령으로 표현 가능한가? 없으면 CPU 잇으면 GPU

CPU는 호텔 셰프, GPU는 신입 보조 셰프 + 웨이터



- **즉시모드**는 상태가 없는 그리기 방식.
- 화면을 그려야할 때마다 시스템은 빈 캔버스를 개발자에게 줌
- 개발자는 모든 그리기 명령어(원 그려, 선 그려, 텍스트 써)를 매번 처음부터 다시 실행함(CG)
- 이 과정은 CPU가 통제함
- UI가 매번 완전히 바뀌는 동적인 동작이나 복잡한 뷰에 유리 (커스텀뷰)
- CPU가 비트맵을 만드는 비용은 비쌈 (코어수가 별로없음, CPU->GPU 전송)

<br />


- **유지모드**는 상태를 가지고 바뀐 부분만 업데이트하는 그리기 방식.
- 시스템은 실행되고 있는 전체 객체 목록을 가지고 있음
- 개발자가 뷰의 속성을 변경하면 프레임워크(CA)는 이 변경을 감지해서 시스템으로 보냄
- 시스템(렌더서버)는 합성한 데이터를 GPU로 넘기고 GPU는 이를 렌더함
- UI가 단순한 경우에도 시스템은 합성을 계속 해야됨
- 그러나 렌더링 관련에서 GPU의 비용이 압도적으로 쌈 (코어 많음, 이부분은 엔비디아에서 설명한 GPU 세션 참고바람)
- UIKit은 기본적으로 유지모드 시스템, SwiftUI는 더 진화된 유지모드 시스템


<br />

---

# 한줄요약

- CALayer (엔진): 나는 비트맵을 움직이고, 합성할 수 있는 고성능 GPU 렌더링 엔진이다.
- UIKit: 수동기어 차
    - 나는 저 CALayer 엔진을 가져다가, UIView라는 껍데기를 씌우고, 오토 레이아웃과 리스폰더 체인이라는 조작 시스템으로 동작하는것
    - 내가 몇단으로 갈 지 빠르게 갈지 어떻게 갈지를 모두 결정
- SwiftUI: 테슬라
    - 나도 저 CALayer 엔진을 가져다가, 설계도(View)만 넣으면 알아서 굴러가는 상태 주도(State-Driven) 조작 시스템으로 동작하는것
    - 뷰는 네비게이션 같은 역할


<br />

---

# UIView

UIView는 터치이벤트, 레이아웃 관리, UIKit 연동, 뷰컨과의 연동(뷰 생명주기) 위한 고수준 API


<br />

## GPU 드로잉 (backgroundColor 등):

-   CPU: GPU야, '파란색 사각형(명령어)' 하나만 그려줘.
-   GPU: OK, 재료 필요 없어. 내가 최종 화면에 직접 색칠할게(렌더링)

<br />

## CPU 드로잉 (draw(rect:)):

-   CPU: 픽셀을 하나하나 계산해서 **비트맵(재료)**을 만들게.
-   GPU: OK, 그 재료 줘. 내가 최종 화면에 붙여넣을게(합성)

<br />

## 렌더링이란

-   데이터를 시각적 이미지로 변환하는 모든 과정
-   CPU가 만드는것은 래스터화(rasterization), GPU에 넘길 재료
-   GPU가 만드는것은 합성(compositing), 최종 화면 비트맵

<br />

## GPU 렌더링 흐름

- UIView 속성 변경함
- UIView는 상태변화를 CA로 통보
- CA는 해당 레이어를 더티상태로 변경 (CATransaction에 큐해놓음)
- 런루프 한 사이클이 끝나면 CA는 CATransaction을 commit
- 변경사항이 렌더트리에 반영됨
- CA는 이 렌더 트리를 렌더서버(시스템 프로세스)에 넘김
- 렌더서버는 GPU 명령어 생성해서 넘김
- GPU는 비트맵,벡터등으로 프레임 버퍼를 만들고 그림

<br />

## CPU 렌더링 흐름

- draw, setNeedsDisplay호출, bounds가 변경되어 기존 비트맵을 사용할 수 없을때, 이미지뷰
- CA가 비트맵 버퍼 준비하고 CPU에서 CGContext생성
- CG로 직접 픽셀 계산
- 비트맵을 CALayer.contents에 설정하고 그 이후로는 같음


<br />

## UIView / CALayer

- UIView는 '무엇을' 할지(이벤트 처리, 레이아웃)를 결정하고, CALayer는 '어떻게' 보일지(시각적 표현, 애니메이션)
- CALayer의 contents가 있으면 GPU는 캐싱되어있는 비트맵(순수 이미지, CGImage)을 받고 그걸 그대로 뿌려준다 
- contents가 없으면 GPU는 명령어를 받고 그걸 이용해 화면 비트맵을 만든다.

<br />


## CG는 그리기를 함 그러나 CA는 그리기 안함

-   CAShapeLayer처럼 path(벡터)를 받아 GPU가 직접 그려주는 '특별한' 레이어가 있긴함

<br />


## draw(rect:) 호출 시점

-   뷰가 처음 화면에 나타날 때
    - CA가 layer를 그리려고하는데 contents가 없음 -> 나의 델리게이트(UIView)한테 받아와야지
-   뷰의 bounds가 변경될 때

<br />

## 이벤트 처리 흐름

-   UIWindow라는 루트를 가진 트리로 뷰 계층구조를 관리
-   UIView는 UIResponder를 상속받아 이벤트를 처리하는 객체임
-   사용자가 화면을 터치하면 UIKit은 firstResponder를 찾아 이벤트 처리를 부탁
-   하지않으면 루트까지 타고타고 감. 이 경로를 리스폰더 체인이라고 함

<br />

## UIKit의 렌더링 과정

-   VSYNC
    -   흔히 말하는 프레임 단위.
    -   60Hz는 16.67ms 마다 업데이트를 진행함 1초당 60번 업데이트 한다는 소리.
    -   60Hz 기준으로는 16.67ms가 1 VSYNC
    -   16.67ms안에 이벤트 발생부터 렌더링까지 완료해야함 실패시 다음 프레임으로 넘어감
    -   프레임이 하나 밀리게 되는것을 hitch라고 말하며 쉽게 말하면 '버벅임'
    -   Event, Commit / Render prepare, Render execute / Display 단계로 렌더링 과정이 진행됨

-   App(Event)
    -   주체: UIView, RunLoop / CPU
    -   앱에서 터치, 네트워크 응답등 화면 업데이트 이벤트가 발생하고 RunLoop가 감지 후 처리
    -   이벤트에 따라 layoutSubviews(), display(), draw(_:), CALayer의 변경 등의 호출이 예약됨

-   App(Commit)
    -   주체: UIView, CALayer / CPU
    -   Event의 내용을 CALayer에 반영하고 Core Animation에게 알림

-   Render Prepare
    -   주체: Core Animation, CALayer / CPU -> GPU
    -   CALayer의 정보를 기반으로 비트맵 변환 후 GPU에 전달

-   Render Execute
    -   주체: Metal, OpenGL / GPU
    -   Core Animation → Metal → OpenGL/Metal → GPU 연산 단계로 진행

-   Display
    -   주체: Core Animation / GPU -> 하드웨어 화면
    -   Core Animation이 VSYNC 신호에 맞춰 GPU 버퍼를 교체

<br />

## 주의할 점

-   SetNeedsLayout()은 frame 변경이나 addSubview등 레이아웃을 변경할 때 사용됨
    -   GPU 기반 드로잉
    -   내부적으로 layoutSubviews()이 호출됨
    -   layoutSubViews()를 직접 호출하지말고 setNeedsLayout()으로 시스템이 최적화된 알고리즘으로 실행하도록해야함
    -   layoutIfNeeded()는 layoutSubViews()를 강제로 호출하는 메서드 (사용 지양)
    -   layoutIfNeeded()는 런루프를 기다리지 않고 즉시, 동기적으로 업데이트 시킴
-   SetNeedsDisplay()은 draw(rect:) 메서드를 강제로 호출하고 싶을 때만 사용
    -   CPU 기반 드로잉
    -   내부적으로 draw(_:)가 호출됨 
-   오프 스크린 렌더링 : GPU가 그리지 못하고 Off-screen buffer를 만든 뒤 그 결과물을 다시 복사해오는 과정
    -   부모에 cornerRadius + masksToBounds에서 주로 발생
    -   부모에 꽉채워 UIImageView를 넣으면 GPU는 자식과 부모를 그리는 동시에 자식을 부모의 cornerradius처럼 자식도 깎아야함
    -   이건 못함 따라서 버퍼에 부모와 자식을 원래대로 그리고 깎음 그 결과물을 다시 가져와서 그림
    -   원래 한 프레임에 끝날 렌더링을 버퍼로 갓다가 오는 과정으로 여러 프레임을 사용하고 이는 버벅임으로 이어짐
    -   메모리 사용, GPU VRAM으로 작업공간 전환등 공간, 시간적 오버헤드 발생
    -   해결책
        -   자식에 직접 cornerRadius를 주기
        -   layer.shouldRasterize = true 주기 (첨에 만든 이미지 GPU에 캐싱해놔라~), 뷰가 잘 안바뀔때 씀

<br />

## frame vs bounds

- 부모기준 origin과 size (바깥에서 본 나)
- 내 기준 origin과 내 진짜 size (나 자체)
- 회전시켰을 때 frame은 (150, 150), bounds는 (100, 100)

<br />

## AutoLayout LayoutPass

-   런루프의 Commit단계에서 updateConstraints가 호출된다 (제약조건이 업데이트된다)
-   UIKit은 수집된 모든 제약조건을 Cassowary 알고리즘을 사용하여 Frame을 계산한다. (레이아웃 계산)
-   layoutSubviews가 호출되고 각 계산된 frame으로 세팅이 된다. (레이아웃 적용)
-   updateContraints는 비싼 작업으로 setNeedsLayout을 우선 사용하라
-   뷰를 다룰때 constraint를 껐다 키는것보다 constant값을 변경하거나 isHidden을 활용하는것이 유리

<br />

## 뷰 레이아웃부터 화면 렌더링 과정

-   UIWindow 생성
-   window.rootViewController가 설정됨
-   viewDidLoad 호출 (자신의 UIView가 메모리에 로드, 이때 CALayer 생성)
-   뷰 계층에 추가됨
-   viewWillAppear / viewDidAppear 호출
-   LayoutPass 실행
-   RenderPass 실행



<br />

---

# SwiftUIView

-   상태를 가지고 있지않은 화면이 어떻게 보여야 하는지를 설명하는 blueprint
-   @State가 바뀔 때 의존성 그래프를 사용해서 최소한의 변경만 렌더 트리에 적용

<br />

## 레이아웃 방식

-   부모가 자식에게 크기를 제안 (자식은 GeometryReader로 알수있음)
-   자식은 그 크기 안에서 제안
-   부모는 자식이 정한 크기를 존중하여 배치


<br />

## 렌더링 방식

-   @State가 변경됨
-   AttributeGraph는 @State에 의존하는 View의 body를 다시실행하여 blueprint를 받음
-   뷰마다 ID를 가지고 있으며 이전 설계도와 현재 설계도를 비교하여 Diff함
-   바뀐 부분만 식별하여 실제 렌더 트리의 CALayer의 속성을 변경함


<br />

## CPU 드로잉

-   Canvas 뷰를 사용
    -   UIKit의 draw(rect)와 동일하게 즉시모드로 동작
    -   GraphicsContext(CGContext의 Swift래퍼)를 사용하여 CPU가 재료 비트맵을 그림

<br />

## GPU 드로잉

-   Text, Rectangle등 SwiftUI의 뷰와 수정자
    -   SwiftUI가 CALayer의 속성으로 변경함


<br />

## 최적화 팁

-   hitTest == .contentShape
-   shouldRasterize == drawingGroup
-   .id
    -   SwiftUI는 매번 새로 생성되는 Struct로 UIView처럼 메모리주소로 뷰를 구별하지 못함
    -   SwiftUI는 body의 구조를 보고 ID를 판단함, 따라서 if문으로 구조가 바뀌면 새로그림
    -   그러나 다른부분은 같은데 처음부터 그리는것은 불필요함 따라서 id를 이용하여 해당 부분은 같은 것임을 명시해줘서 그부분만 다시 렌더링가능


<br />

## 상태 관리 - 뷰가 직접 소유하는 상태

-   @State : 단순한 값을 저장할 때 사용
-   @StateObject : @State의 클래스 버전, 뷰가 뷰모델과같은 복잡한 상태를 직접 생성하고 소유할 때 사용
-   객체를 @State로 소유하면 안됨
    -   @State는 값을 저장하도록 설계되었고 @StateObject는 참조를 저장하도록 설계됨
    -   @State는 참조값을 저장했을 때 그 안에서 내부의 변화를 감지할 수 없음, 그러나 @StateObject는 감지 가능
    -   @StateObject는 단 한 번만 초기화를 보장

## 상태 관리 - 남의 상태를 연결하는 상태

-   @Binding : 부모의 @State를 연결받는 two way 통로
-   @ObservedObject : 부모의 @StateObject를 연결받는 two way 통로
-   @Published : 상태 관리를 하고싶은 ObservableObject의 프로퍼티에 사용 

## 상태 관리 - 환경에서 받는 상태

-   @EnvironmentObject : 커스텀 전역 상태
-   @Environment : 시스템 전역 상태

## Bindable, Observable (iOS 17 +)

-   ObservableObject, @Published, @StateObject, @ObservedObject를 대체하는 매크로
-   Observable : ObservableObject 프로토콜을 따르고, @Published를 일일이 붙일 필요가 없게 해줌
-   Bindable : Observable 매크로로 만든 객체를 자식에게 바인딩 가능한 상태로 넘겨줄 수 있음


## 기타 래퍼

-   @AppStorage: UserDefaults에 값을 저장하고 동기화
-   @SceneStorage: 앱이 백그라운드로 갈 때 화면의 상태를 임시 저장
-   @FocusState: 키보드 포커스(예: 어떤 TextField가 활성화되었는지)를 관리
-   @GestureState: 제스처가 '진행 중'일 때만 상태를 임시로 저장



<br />

---

# 왜 UI는 메인스레드에서 업데이트 되어야하는가

-   UIKit, SwiftUI는 Not Thread-Safe함
-   Not Thread-Safe로 설계 되었다는 것은 여러곳에서 수정하는 것에 대한 잠금장치가 없다는것
-   이는 Race Condition을 만들 수 있고 예측 불가능하게됨
-   따라서 모든 UI 수정은 메인스레드에서 순서대로 처리한다라는 서로간의 약속을 정함
-   왜 Thread-Safe하게 하지 않았나
    -   Lock을 하면 다음 변경사항은 끝날때까지 계속 기다려야됨
    -   데드락 발생 다수. 스레드 A가 버튼을 잡고있는데 다음 작업이 라벨이고 스레드 B가 라벨을 잡고있는데 다음 작업이 버튼일때 무한 기다림