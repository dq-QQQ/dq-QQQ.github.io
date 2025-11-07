---
title: Obj-C To Swift
date: 2025-11-03
excerpt: "Obj-C 프로젝트를 SwiftUI 프로젝트로 전환"
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


# 이건 앱이 아니라 프레임워크이다. MVVM이니 TCA니 의미가 있나?

-   mvvm,tca는 앱의 ui와 상태관리를 편하게 하기 위해서 쓰는것임
-   프레임워크의 목적은 기능들을 캡슐화해서 재사용가능한 도구임 따라서 ui와 상태관리가 덜 중요함
-   그래서 아키텍쳐 패턴보다 SOLID, 디자인패턴등이 중요함
-   Single Responsibility "하나의 클래스,파일은 하나의 책임만 가져야 한다.
    -   파일의 개수로 확인가능
-   Open Closed : 확장에는 열려있어야 하고, 변경에는 닫혀 있어야 함
    - 기능을 추가하기 위해 기존 코드를 수정하는 게 아니라, 새 코드를 '추가'하도록 설계해야 합니다.
    - 델리게이트??
-   인터페이스 분리 원칙
    - 기능별로 인터페이스 분리
-   D: 의존성 역전 원칙
    - 의존성이 강한 두 클래스의 프로토콜을 추출해서 커넥터를 만들고 그걸로 통신함

<br />

---

# 프레임워크이다. 뷰나 API들의 트리거가 언제되냐가 중요한데 UIKit랑 SwiftUI중에 어떤게 나으려나...

-   uikit

<br />

---

# API이다. 그럼 .h같은 것이나 인터페이스는 어떻게 제공하지...?

- public 속성

<br />

---

# API이다. 근데 같은 Swift에서 쓰는게 아니라 js에서 호출되어야한다. 뭐지,,?? 이게 어캐되는거지

- 웹뷰로 됨, js 인터페이스 하나 뚫어놓으면 됨

<br />

---

# SwiftUI로 만든 프레임워크를 모든 프로젝트에서 쓸 수 있나? SwiftUI로 햇을때의 장점이뭐지

- 로직이 많으면 맞지않음

<br />

---

# SwiftUI 뷰가 구조체인 이유는 뷰는 UI가 보여줘야하는 현재 상태를 서술적 묘사임, 시간이 지남에 명령형 커맨드를 받는 객체 인스턴스로 살아서 돌아다닐 필요가 없음
    - 객체 인스턴스로 돌아다니는건 뷰 자체가 상태를 가지는것(uikit 방식)
    - 그러면 진짜 데이터와 뷰의 데이터를 동기화해주는 작업이 필요함. 둘다수정해야됨
    - 구조체는 상태가 없고 source of truth를 받아서 묘사만 하는것임
    - 뷰 자체가 자신만의 상태를 갖게 되어, 진짜 데이터(상태)와 뷰의 상태가 일치하지 않는 버그의 근원이 됨
    - SwiftUI는 뷰를 상태가 없는 구조체로 만듦으로써 이 문제를 원천적으로 방지함


-   뷰는 단지 선언적인 설명(description)이므로 하나의 뷰를 여러개로 나누어도(코드 구조와) 앱 성능과는 무관함



<br />

---

# 다중 윈도우, Scene 
static var currWindow: UIWindow? {
        UIApplication.shared.connectedScenes
            .compactMap { $0 as? UIWindowScene}
            .flatMap { $0.windows }
            .first(where: { $0.isKeyWindow})
    }

- ios 13 이전은 단일 윈도우, 그 이후는 다중, 사용자가 실제로 상호작용하고 있는 윈도우 찾아내는 코드



<br />

---







애플리케이션 생명 주기와 뷰
앱 시작과 종료 시점에서의 뷰 처리
백그라운드와 포그라운드 전환 시 뷰 처리
비동기 작업과 UI 업데이트
왜 메인스레드에서 업데이트해야하는가
iOS의 메인 런 루프 및 업데이트 사이클
화면 갱신 주기와 이벤트 처리 방식에 대한 설명
layoutifneeded / layoutsubview


뷰 최적화 및 메모리 관리
메모리 경고 처리: didReceiveMemoryWarning
뷰 최적화: shouldRasterize, drawsAsynchronously
뷰의 재사용: reuseIdentifier와 dequeueReusableCell















<br />

---

# 타입

---

self, Self, type, Type

스위프트, objc 자료형 (특히 문자열) isempty

unsafeBitCast















<br />

---

#  (비동기, 동기)

---

DispatchSemaphore
DispatchQueue.main.async { [weak self] in
async await
Mainactor / actor
DispatchGroup
@Sendable
@preconcurrency
스레드와 코어 개념
메인 스레드와 백그라운드 스레드
continuation









<br />

---

# swift, Objc 호환

---

@convention(block)

@objc

nsobject

dynamic

obj_msgsend

VTable

정적디스패치, 동적디스패치

Mirror








<br />

---

# 메모리

---

https://ios-development.tistory.com/1604

ARC(자동 메모리 관리) weak vs unowned

protocol OZTotoNavigatorDelegate: AnyObject / weak로 쓰려면

leak 관리

메모리 사용량






static let shared = Resolver()
이런 싱글톤에서 
Static property 'shared' is not concurrency-safe because non-'Sendable' type 'Resolver' may have shared mutable state
이런 오류가 난다.

-----------------------------------

함수나 타입에 @MainActor 를 붙이는 이유

    func startSplash() {
        Task { 
            try? await Task.sleep(nanoseconds: 2_000_000_000)
            self.isLaunching = true
        }
    }

여기에 MainActor붙이면
Task-isolated value of type '() async -> ()' passed as a strongly transferred parameter; later accesses could race
이 오류가 없어지는데 왜지

-----------------------------------

func resolve<T>(_ type: T.Type) -> T {
        container.resolve(T.self)!
type? Type 차이 Self self

-----------------------------------


        if viewModel.isFinished {
            SplashView()
        } else {
            TotoView()
        }

이건 되고 
        viewModel.isFinished ? SplashView() : TotoView()

이건 왜안돼

-----------------------------------

@State랑 @ObservedObject랑 @Statedobject랑 뭔차이야

-----------------------------------

상수를 관리할 때 enums vs structs 뭐가 좋은가

-----------------------------------

Service/Manager 간 패턴 구분

-----------------------------------

extension AppDelegate: MessagingDelegate{
    
    // fcm 등록 토큰을 받았을 때
    func messaging(_ messaging: Messaging, didReceiveRegistrationToken fcmToken: String?) {



-----------------------------------


[swiftUI] Actor, isolated, nonisolated 에 대해

-----------------------------------

<@Sendable은 무엇인가?> 5. nonisolated keyword

-----------------------------------

@UIApplicationDelegateAdaptor의 사용시 암묵적으로 AppDelegate가 MainActor에서 동작

-----------------------------------

UIImageView 초기화면 리사이징

------------------------------



 @StateObject private var viewModel = Resolver.shared.resolve(DefaultSplashViewModel.self)
//    
//    init() {
//            // DI에서 any SplashViewModel로 받아온 뒤, 다운캐스팅
//            let anyViewModel = Resolver.shared.resolve((any SplashViewModel).self)
//            self._viewModel = StateObject(wrappedValue: anyViewModel as! DefaultSplashViewModel)
//        }

self._viewModel??


---------------------------------


이렇게 하면

✅ BundleFileDataSource는 FileManagerDataSource.ReturnType을 그대로 쓰는데,
FileManagerDataSource는 associatedtype ReturnType이 있어서 Self requirement가 생깁니다.

즉,

any BundleFileDataSource 타입을 쓰려고 하면 컴파일이 막힙니다.

왜냐면 Swift에서는 associatedtype이 있는 프로토콜을 existential로 못 쓰거든요.

이게 바로 Swift에서 흔히 부딪히는 Protocol with associatedtype은 any로 못쓴다 문제.

---------------------------------


Task-isolated value of type '() async -> ()' passed as a strongly transferred parameter; later accesses could race

---------------------------------


@objc class func fetch(
    product: sending StoreListProduct,
    completion: @escaping @Sendable (AppStoreProduct?) -> Void
)

Capture of 'runtime' with non-sendable type 'OZTotoRuntime' in a `@Sendable` closure


func onPageLoad(_ runtime: OZTotoRuntime) {
if isFirstLoading {
saveDeviceInfoUC.execute(runtime: runtime)
isFirstLoading = false
}
이런 코드가 잇는데 저 saveDevice는 filemanager로 파일 저장하는거라 오래걸려서 비동기로 빼고싶은데 어떻게 하지



-----------------------------

weak 핸들러 함수 만들기


--------------------

Use of protocol 'View' as a type must be written 'any View'

SwiftUI에서 "뷰를 속성(parent로)으로 받아서 그대로 반환"하는 패턴

--------------------

Publishing changes from within view updates is not allowed, this will cause undefined behavior.

--------------------

Cannot convert value of type '[[String : any Sendable]]' to expected argument type 'Range<Int>'

--------------------

            Spacer()에 vstack spacing이 먹는구나

--------------------

.highPriorityGesture(
    TapGesture().onEnded { _ in
        // your code here to handle tap gesture......
    }
)

--------------------


_ cmd: (any OZReportCustomUICommand)

_ cmd: OZReportCustomUICommand

차이

--------------------


@escaping attribute may only be used in function parameter position


confirmAction: @escaping () -> Void,
cancelAction: @escaping () -> Void,
resetAction: (() -> Void)? = nil

위에는 @escaping이 있는데 reset은 왜없어

--------------------


PreferenceKey

--------------------


fixedSize


--------------------


@StateObject private var stampContentViewModel: StampContentViewModel
    
    init(viewModel: StampViewModel) {
        self.viewModel = viewModel
        _stampContentViewModel = StateObject(wrappedValue: StampContentViewModel(someParameter: "value"))
    }


--------------------


            LazyVGrid(columns: gridColumns, spacing: 20) {


--------------------


_selectedMode


--------------------


 @unchecked Sendable 


--------------------
                             .minimumScaleFactor(0.5)
--------------------


부모가 정해진 뷰에 맞춰서 하고싶을때 지오메트리랑


--------------------

MaxWidthPreferenceKey

--------------------


웹뷰 로그인 방식

url이 달라졌는데 계정이 같으면 로그인이 자동으로 된다

--------------------

딥링크

--------------------



아니 지금 구조가 DefaultNotificationManager 에서 didReceive로 받아서 DefaultNotificationRepository로 보낸다음에 DefaultNotificationUC -> OZTotoViewModel이렇게 감지해서 OZTotoViewModel에서 뷰를 업데이트 시킨단 말이야 근데 지금 OZTotoViewModel은 OZTotoView가 렌더링 될때 생성되고 그 생성자 안에 observe변수가 있어 흐으으음,,, 어떡하지



-----------------

scaletofill
scaletofit



<br />

---

# 정적 팩토리 메서드 vs 생성자

---

<br />

---

# lazy - 다중스레드에서 접근할 때?, 사용방법

---



<br />

---

# 클로져

---


<br />

---

# map, reduce, filter, flatmap, compactmap, foreach 

---


<br />

---

# defer

---


<br />

---

# where

---

<br />

---

# weak, unowned

---

<br />

---

# inlinable, propertyWrapper

---

<br />

---

# protocol anyobject

---

<br />

---

# 비동기, 동기

---

- Continuation?
- 위치앱(CoreLocation)의 델리게이트 방식을 async/await으로 전환 프로젝트 예시


- 비동기 코드 : 나중에 알 수 없는 시간에 호출되는 코드
- await이 되면 suspension point 전후에서 사용할 수 있는 프레임을 heap에 저장
- 스택프레임에 잇는 스택은 await 함수로 바뀜
- 디스패치큐는 스레드를 불러옴
 - 근데 한 스레드가 block되었을때 처리를 위해 스레드를 더 불러옴
 - 근데 이 block된 스레드가 많아지면? thread explosion이 됨
 - block된 스레드는 메모리와 리소스를 차지함
 - 스케쥴링 오버헤드도 일어남
 - 그래서 async/await이 나타남
- Swift Concurrency에서는 최대 스레드 개수 = 코어개수
- 스레드간의 context switch가 없음
- Task는 A unit of asynchronous work
- Task문 안에서는 순차적으로 실행됨
- Task 안에서 값이 공유될때는 sendable을 채택해야함, 그럼 값을 복사해줌
- 근데 가변 데이터를 공유하고 싶다면? actor를 사용함
- actor의 상수는 그냥 접근 가능, actor의 변수와 메서드는 await으로 접근해야함, 외부에서 변수 수정 불가) 왜? 다른곳에서 쓰고 있을 수 있으니깐
- actor에 대한 접근은 직렬임, 여러 스레드 X



arc/mrc