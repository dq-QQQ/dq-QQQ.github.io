---
title: iOS 지식
categories:
  - iOS
excerpt: "면접 대비!!!!!!!!:)"
date: 2023-07-25
tags:
- iOS
---


<br />
<br />

---

# iOS


Delegate vs Block vs Notification
Memory Management
assign vs weak
Bounds 와 Frame 의 차이점을 설명하시오.
AppDelegate 에서 앱의 상태 변화에 따라 호출되는 함수에 대해 명확히 설명할 수 있나요 ?
스레드(thread) 와 프로세스(Process) 의 차이점 ? / Program vs Process
객체 지향 프로그래밍(OOP) 의 정의와 특징

'Call by value' vs 'Call by reference'

동기 vs 비동기

메모리 구조 와 스택

링크드리스트(Linked List) 란?

64비트와 32비트의 차이

Mutable 객체 vs Immutable 객체.

샌드박스란 무엇이고 왜 샌드박스를 사용하는지?

Delegate / Notification 의 차이와 활용도

push 서비스 등록시 절차과정

카테고리 확장과 / 서브 클래싱 이 둘의 차이와 각각의 활용

Swift 와 Objective - c 를 동일한 코드를 구현할때 서로간에 장점과 단점은?

NSArray, NSDictionary, NSSet의 쓰임

Table View 혹은 Collection View 에서 꼭 필요한 Delegate 와 Function 은 무엇이고 어떤 역할을 하나요 ?

ㄱ. 끝이 '-DataSource' 나 '-Delegate' 로 끝나는 함수들이 꼭 필요한 함수이다. DataSource 의 경우 테이블 뷰나 컬렉션 뷰에 데이터를 제공하는 역할을 하고, Delegate 의 경우에는 이벤트가 발생했을 경우 처리할 메서드를 제공한다.

Instrument 를 활용하여 앱의 Memory 사용량을 확인하고 리팩토링해본 경험이 있나요?

이미지를 Memory-Cache 와 Disk-Cache 를 이용해 보았다면, 설명해볼 수 있나요 ?

GCD(Grand Central Dispatch)의 개념을 설명할 수 있나요 ?

ㄱ. 초보자를 위한 Grand Central Dispatch

(Thread 관련) 화면이 멈추지 않게 하려면 어떤 스레드를 건드리지 말아야 하나요 ?
ㄱ. Main Thread 에서 Sync 를 사용하면 안된다.

Background Task 를 이용해 백그라운드에서 동작하는 작업을 설명할 수 있나요 ?

CustomScheme 를 이용해 딥링크 기능 구현을 설명할 수 있나요 ?

Universal Link를 사용해 웹에서 앱을 연동하는 것을 설명할 수 있나요 ?

Google Analytics, Tune, Fabric등 모바일 애널리틱스 툴을 연동한 경험이 있나요 ?

Push 서비스를 구현한 경험이 있나요 ?

UICollectionView와 UITableView의 스크롤 속도를 최적화를 위해 어떠한 방법을 사용해보셨나요?

선호하는 UI 구현 방식에 대해 설명해주세요.

iPhone의 다양한 해상도를 지원하기 위해 어떤 방식을 활용하고 있는지, 다양한 해상도를 지원하기 위해 특별히 고려한 것들이 있는지 설명해주세요.

OpenURLScheme 을 사용해 보았나요 ?

상단 상태바의 색을 변경하는 방법은 ?
실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오.
앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가?
앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?
App thinning에 대해서 설명하시오.
앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가?
@Main에 대해서 설명하시오.
앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요?
상태 변화에 따라 다른 동작을 처리하기 위한 앱델리게이트 메서드들을 설명하시오.
앱이 In-Active 상태가 되는 시나리오를 설명하시오.
scene delegate에 대해 설명하시오.
UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가?
App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오.
NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오.
GCD API 동작 방식과 필요성에 대해 설명하시오.
Global DispatchQueue 의 Qos 에는 어떤 종류가 있는지, 각각 어떤 의미인지 설명하시오.
iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인가?
Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.
Delegate란 무엇인지 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오.
NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.
UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가?
App Bundle의 구조와 역할에 대해 설명하시오.
모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?
자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오.
View 객체에 대해 설명하시오.
UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.
iOS에서 뷰(View)와 레이어(Layer)의 개념과 차이점에 대해 설명해보세요.
UIWindow 객체의 역할은 무엇인가?
UINavigationController 의 역할이 무엇인지 설명하시오.
TableView를 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오.
하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오.
setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.
stackView의 장점과 단점에 대해서 설명하시오.
NSCache와 딕셔너리로 캐시를 구성했을때의 차이를 설명하시오.
URLSession에 대해서 설명하시오.
prepareForReuse에 대해서 설명하시오.
다크모드를 지원하는 방법에 대해 설명하시오.
ViewController의 생명주기를 설명하시오.
TableView와 CollectionView의 차이점을 설명하시오.
Dynamic Library와 Static Library의 차이점에 대해 설명해보세요.
Diffable Datasource
Frame vs Bounds
Compositional Layout
Multiple Gesture Recognizer
ViewController 라이프사이클 이해 및 활용
오토레이아웃을 코드로 작성하는 방법
Left, Right Constraint vs Leading, Trailing Constraint
Safe Area
스토리보드의 장단점
Responder Chain
First Responder
UI를 메인스레드에서 다루는 이유
View Drawing Cycle
setNeedsDisplay, setNeedsLayout
UITableView 기초부터 다시 살펴보기
dequeueReusableCell (withIdentifier:for:) vs (withIdentifier:)


<br />
<br />

---

# Autolayout

오토레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)
hugging, resistance에 대해서 설명하시오.
Intrinsic Size에 대해서 설명하시오.
스토리보드를 이용했을때의 장단점을 설명하시오.
Safearea에 대해서 설명하시오.
Left Constraint 와 Leading Constraint 의 차이점을 설명하시오.
Auto Layout과 Frame-based Layout의 차이점은 무엇인가요?
성능 향상을 위해 어떤 디버깅 도구를 사용할 수 있나요? 각각의 디버깅 도구는 어떤 상황에서 사용하는 것이 좋나요?

<br />
<br />

---

# Swift

클로저(Closure)
AutoLayout
IBDesignable & IBInspectable
Swift vs Objective-C
Cocoapods
ARC vs non-ARC / (ARC 관련) Strong, Weak, Unowned 의 개념
ARC와 Block, GCD 와 연관해서 설명해보세요
Static 키워드
Overloading vs Overriding
Access Control 의 종류와 특징
Delegate 와 Protocol 의 차이는 무엇일까요 ?
Rxswift 란 무엇일까요 ?
HIG(Human Interface Guideline) 을 알고 있나요 ?
옵셔널(Optional) 의 개념에 대해 설명할 수 있나요 ?
struct와 class와 enum의 차이를 설명하시오.
class의 성능을 향상 시킬수 있는 방법들을 나열해보시오.
Copy On Write는 어떤 방식으로 동작하는지 설명하시오.
Convenience init에 대해 설명하시오.
AnyObject에 대해 설명하시오.
Optional 이란 무엇인지 설명하시오.
Struct 가 무엇이고 어떻게 사용하는지 설명하시오.
Subscripts에 대해 설명하시오.
String은 왜 subscript로 접근이 안되는지 설명하시오.
instance 메서드와 class 메서드의 차이점을 설명하시오.
class 메서드와 static 메서드의 차이점을 설명하시오.
Delegate 패턴을 활용하는 경우를 예를 들어 설명하시오.
Singleton 패턴을 활용하는 경우를 예를 들어 설명하시오.
KVO 동작 방식에 대해 설명하시오.
Delegates와 Notification 방식의 차이점에 대해 설명하시오.
멀티 쓰레드로 동작하는 앱을 작성하고 싶을 때 고려할 수 있는 방식들을 설명하시오.
MVC 구조에 대해 블록 그림을 그리고, 각 역할과 흐름을 설명하시오.
프로토콜이란 무엇인지 설명하시오.
Protocol Oriented Programming과 Object Oriented Programming의 차이점을 설명하시오.
Hashable이 무엇이고, Equatable을 왜 상속해야 하는지 설명하시오.
mutating 키워드에 대해 설명하시오.
탈출 클로저에 대하여 설명하시오.
Extension에 대해 설명하시오.
Extension 내부에서 함수를 override할 수 있는지 설명하시오.
접근 제어자의 종류엔 어떤게 있는지 설명하시오.
defer란 무엇인지 설명하시오.
defer가 호출되는 순서는 어떻게 되고, defer가 호출되지 않는 경우를 설명하시오.
property wrapper에 대해서 설명하시오.
Generic에 대해 설명하시오.
some 키워드에 대해 설명하시오.
Result타입에 대해 설명하시오.
Codable에 대하여 설명하시오.
Closure에 대하여 설명하시오.
Closure와 함수와의 관계에 대해 설명하시오.
Optional Chaining과 nil-coalescing operator(??)의 차이점과 사용 시 주의사항은 무엇인가요?
Swift에서 Async/Await 기능이 도입되기 전에, 비동기(Asynchronous) 작업을 처리하는 방법에는 어떤 것들이 있나요?
타입 변환(Type Casting)과 다형성(Polymorphism)에 대해 설명해보세요.
Swift에서 타입 안전성(type safety)은 어떤 방식으로 보장되나요?
Struct와 Class, Enum의 차이점
ARC 메모리 관리 방식
strong, weak, unowned
Foundation
Generic
Codable Protocol
Dynamic Dispatch
UserDefaults
Codable vs NSCoding
문자열 처리
NSCache vs NSDictionary
KVC(Key-Value Coding)
KVO(Key-Value Observing)
async await
Task
Actor
defer
Convinience init
Escaping Closure
NotificationCenter
sort의 내부구현
Localizing
Method Swizzling
autoreleasepool


<br />
<br />

---

# ARC

ARC란 무엇인지 설명하시오.
Retain Count 방식에 대해 설명하시오.
Strong 과 Weak 참조 방식에 대해 설명하시오.
순환 참조에 대하여 설명하시오.
강한 순환 참조 (Strong Reference Cycle) 는 어떤 경우에 발생하는지 설명하시오.
Functional Programming

순수함수란 무엇인지 설명하시오.
함수형 프로그래밍이 무엇인지 설명하시오.
고차 함수가 무엇인지 설명하시오.
Swift Standard Library의 map, filter, reduce, compactMap, flatMap에 대하여 설명하시오.
Either type이란?
Architecture

MVVM, MVI, Ribs, VIP 등 자신이 알고있는 아키텍쳐를 설명하시오.
의존성 주입에 대하여 설명하시오.
<br />
<br />

---

# SwiftUI

@State에 대해서 설명하시오.
<br />
<br />

---

# Combine

PassthroughSubject에 대해서 설명하시오
@Published에 대해서 설명하시오
AnyCancellable에 대해서 설명하시오
sink에 대해서 설명하시오
throttle과 debounce의 차이점을 설명하시오.
Data를 Binding 하는 방법에 대해서 설명하시오.
Optional




<br />
<br />

---

# Rx

Reactive Programming이 무엇인지 설명하시오.
RxSwift를 왜 사용하는지 설명하시오.
RxSwift의 단점을 설명하시오.
RxSwift에서 Hot Observable과 Cold Observable의 차이를 설명하시오.
Subject의 종류와 차이점에 대해 설명하시오.
Subject와 Driver의 차이를 설명하시오.
Single, Completable, Maybe의 차이점에 대해 설명하고, 언제 적용하면 좋을지 설명하시오.

<br />
<br />

---

# Advanced



method swizzling이 무엇이고, 어떨 때 사용하는지 설명하시오.
NSCoder 클래스는 어떤 상황에서 어떻게 써야 하는지 설명하시오.
Responder Chain 구조에 대해 설명하고, First Responder 역할에 대해 설명하시오.
NSObject부터 UIButton 까지 상속 과정의 계층과 역할을 설명하시오.
shallow copy와 deep copy의 차이점을 설명하시오.
Push Notification 방식에 대해 설명하시오.
Foundation 과 Core Foundation 프레임워크의 차이점을 설명하시오.
NSURLConnection 에서 사용하는 Delegate 메서드들에 대해 설명하시오.
Synchronous 방식과 Asynchronous 방식으로 URL Connection을 처리할 경우의 장단점을 비교하시오.
Plist 파일 구조와 Plist 파일에 저장된 데이터를 다루기 적합한 클래스를 설명하시오.
Core Data와 Sqlite 같은 데이터 베이스의 차이점을 설명하시오.
JSON 데이터를 처리하는 방식과 파서, 객체 변환 방식에 대해 설명하시오.
웹 서버와 HTTP 연결을 사용해서 데이터를 주거나 받으려면 사용해야 하는 클래스와 동작을 설명하시오.
Protocol에서는 왜 var만 되는지 설명하시요.
DispatchQueue.main.sync를 사용하는 상황을 설명하시오.
Run Loops에 대해 설명하시오.
객체지향

객체지향이 무엇인가요? 절차지향과의 차이점은 뭐죠?
객체지향 SOLID 원칙에 대해서 설명해 주세요.
객체지향 4가지 특징에 대해서 설명해 주세요.
대표적인 객체지향 언어에는 어떤 것들이 있나요?
함수형 프로그래밍에 대해서 설명해 주세요.
클래스, 객체, 인스턴스 차이에 대해서 설명해 주세요.
순수 추상 클래스와 인터페이스의 차이는 무엇인가요?
인터페이스는 주로 언제 사용하나요?
오버로딩과 오버라이딩의 차이는 무엇인가요?
업캐스팅과 다운캐스팅이란?
디자인 패턴

디자인 패턴이란 무엇인가요?
추상 팩토리 패턴이란?
싱글톤 패턴이란?
빌더 패턴이란?
팩토리 메소드 패턴이란?
옵저버 패턴이란?
어댑터 패턴이란?
뷰홀더 패턴이란?

<br />
<br />

---

# 자료구조

배열과 링크드 리스트의 차이점에 대해서 설명해 주세요.
스택과 큐에 대해서 설명해 주세요.
우선순위 큐에 대해서 설명해 주세요.
해시테이블에 대해서 설명해 주세요.
그래프와 트리의 차이점에 대해서 설명해 주세요.
최소 신장 트리에 대해서 설명해 주세요.
힙 자료구조에 대해 설명해 주세요.
힙의 삽입과 삭제는 어떻게 이루어지나요?
이진 탐색 트리에 대해 설명해 주세요.
포화(Perfect) 이진트리, 완전(Complete) 이진트리, 정(Full) 이진트리의 차이점에 대해 각각 설명해주세요.
레드 블랙 트리에 대해 설명해주세요.
레드 블랙 트리의 삽입과 삭제 과정에 대해서 말해보세요.
AVL에 대해 설명해주세요.
B-Tree와 B+Tree에 대해서 설명해 주세요.
String / Long Data

String Comparison Complexity에서 시간 복잡도가 최악인 경우는? 발생할 확률은?
String Comparison Complexity를 개선할 수 있는 방법은? (길이비교, 해시)
substr(), length(), indexOf() 를 직접 구현해보자
비교기반 자료구조/탐색알고리즘에 적용하면 생기는 문제점과 해결책 (hash / graph)
String Literal과 언어에서 String의 구현방법
Substring Problem의 종류와 원리를 설명하시오

<br />
<br />

---

# al

시간복잡도

시간 복잡도 VS 공간 복잡도
시간 복잡도는 실제 수행 시간과 어떤 관계가 있는가?
시간복잡도가 작은 알고리즘은 무조건 빠른가?
최악의 복잡도는 나쁘지만 실제로는 자주 사용되는 알고리즘을 나열하시오
빅오 표기법에 대해서 설명해주세요

알고리즘

최장 증가 수열(LIS)
최소 공통 조상(LCA)
비트마스크(BitMask)
Call by value, call by reference의 차이점을 설명하시오.
DFS & BFS
크루스칼 알고리즘과 프림 알고리즘에 대해서 설명해 주세요.
다익스트라 알고리즘에 대해서 설명해 주세요.
LinkedList vs ArrayList의 차이점에 대해 설명하시오
인접행렬과 인접리스트에 대해 설명하시오

정렬

54321 배열이 있을 때, 어떤 정렬을 사용하면 좋을까요?
랜덤으로 배치된 배열이 있을때, 어떤 정렬을 사용하면 좋을까요?
자릿수가 모두 같은 수가 담긴 배열이 있을 때, 어떤 정렬을 사용하면 좋을까요?
정렬을 하는 이유는 무엇인가요?
선택 정렬(Selection Sort)
삽입 정렬(Insertion Sort)
거품 정렬(Bubble Sort)
퀵 정렬(Quick Sort)
병합 정렬(Merge Sort)
힙 정렬(Heap Sort)
기수 정렬(Radix Sort)
계수 정렬(Count Sort)
이분 탐색(Binary Search)
언제 불안정정렬 쓰면 안될까?
언어 기본제공 정렬은 어떻게 구현되어 있을까?

Recursive Function / DnC / DP

Tail Recursion
분할정복에 대해 설명하고 그 예시를 드시오
Dynamic Programming가 무엇이고 왜 어떻게 사용하는가?
Memoization 에 대해 설명하시오


<br />
<br />

---

# NET

전산 기본

OSI 7계층에 대해서 설명해주세요.
TCP/IP 4계층에 대해서 설명해주세요.
DNS가 무엇인가요?
www.naver.com에 접속할때 일어나는 일에 대해 설명해주세요.
도메인 이름으로 실제 IP를 어떻게 찾을 수 있는지 흐름을 설명해 주세요.
유니캐스트, 멀티캐스트, 브로드캐스트란?
TCP/UDP

TCP와 UDP의 차이에 대해서 설명해 주세요.
TCP 헤더에 대해서 설명해 주세요.
MTU가 무엇인가요?
3-way hand shake, 4-way hand shake 흐름에 대해서 설명해주세요.
HTTP

HTTP 프로토콜에 대해서 아는대로 말해주세요.
HTTP와 HTTPS 의 차이는 무엇인가요?
HTTPS가 동작하는 방식에 대해서 설명해 주세요.
HTTP Method 종류 및 역할
HTTP 1.0과 1.1의 차이는 무엇인가요?
HTTP2와 그 특징에 대해서 설명해 주세요.
HTTP 헤더의 구조에 대해서 설명해 주세요.
keep-alive 헤더에 대해서 설명해 주세요.
HTTP GET과 POST의 차이는 무엇인가요?
쿠키와 세션에 대해서 설명해 주세요.
웹

www.google.com에 접속할때 일어나는 일
웹브라우저에서 서버로 요청했을 때, 흐름을 설명해주세요.
CORS란 무엇인가요?
웹 서버와 웹 어플리케이션 서버(WAS)의 차이는 무엇인가요?
REST API에 대해서 설명해 주세요.
REST ful
API Gateway란 무엇인가요?
API Gateway가 다운되면 모든 API를 사용 못할지도 모르는데, 어떤 방안을 마련해야 할까요?
기타

nagle 알고리즘에 대해 설명하세요.
TLS에 패킷 프토토콜의 대해 설명하세요
TLS
네트워크 Layer 라우팅 알고리즘
SNI 필드 차단
흐름제어 / 혼잡제어 / 오류제어
로드 밸런서 / 로드 밸런싱은 무엇인지 설명하세요.
WebRTC
REST API

서버와 통신해서 데이터를 어떻게 가져왔나요 ?

Alamofire 혹은 AFNetworking 등의 라이브러리 사용 경험이 있나요 ? 네트워크 연동 라이브러리를 왜 사용했으며, 장점과 단점을 설명할 수 있나요 ?

인터넷이 느리고 불안정한 지역에서 서버로 API를 호출하여 10만 개의 데이터를 리스트로 보여줘야 한다. 이 문제를 해결하는 과정 및 그 과정 중에 구현할 요소들과 단계별 고려사항은?

JSON 구조는 어떻게 생겼나요 ?

XML 과 JSON 의 차이점에 대해 설명해주세요.

OSI 7계층에 대해 설명해주세요.


<br />
<br />

---

# OS

프로세스

프로세스와 스레드의 차이는 무엇인가요?
멀티 스레드 vs 멀티 프로세스
스택을 스레드마다 독립적으로 할당하는 이유는 무엇인가요?
PC 레지스터를 스레드마다 독립적으로 할당하는 이유는 뭘까?
멀티 프로세스 대신 멀티 스레드를 사용하는 이유는?
컨텍스트 스위칭(Context Switching)이란 무엇인가요?
컨텍스트 스위칭의 과정
교착상태(Dead Lock)란 무엇인가?
교착상태가 발생하기 위한 조건은?
교착상태의 해결법은 무엇인가요?
회피 기법인 은행원 알고리즘이 뭔지 설명해보세요.
은행원 알고리즘의 단점
기아상태를 설명하는 식사하는 철학자 문제에 대해 설명해보세요.
철학자 문제 교착상태 조건 성립 조건
식사하는 철학자 문제 해결책
Mutex vs Semaphore
임계구역이란?
경쟁 상태(Race Condition)란 무엇인가요?
경쟁상태가 발생하는 경우
경쟁상태를 방지하기 위한 해결법의 충족 조건
경쟁상태 해결방법은 무엇이 있나요?
프로세스 혹은 스레드의 동기화란 무엇인가요?
사용자 수준의 스레드와 커널 수준의 스레드의 차이는 무엇인가요?
CPU 스케줄링이란 무엇인가요?
프로세스 스케줄러에는 어떤 것들이 있나요?
CPU 스케줄링의 성능 척도에는 어떤 것들이 있나요?
CPU 스케줄링 방법에는 대표적으로 어떤 것들이 있나요?
동기와 비동기, 블로킹과 넌블로킹의 차이는 무엇인가요?
IPC란 무엇인가요?
fork()란 무엇인가요?
child process와 zombi process에 대해 설명해 보시오. (고아/좀비)
인터럽트란 무엇인가요?
시스템 콜이란 무엇인가요?
전통적인 동기화 문제에는 어떤 것들이 있나요?
메모리

프로세스에 할당되는 메모리의 각 영역에 대해서 설명해 주세요.
메모리 구조의 순서가 어떻게 되는가? CPU에서 가까운 순으로 말해보시오.
페이지와 세그멘테이션에 대해서 설명해 보시오.
외부 단편화란? 내부 단편화란?
메모리의 First Fit, Best Fit, Worst Fit에 대해서 설명해 보시오.
페이지 교체 알고리즘 종류에는 어떤 것들이 있나요?
가상 메모리(Virtual Memory)란?
Demand Paging이란?
가상 메모리를 사용할 시 장단점은?
Cache Memory의 역할은 무엇인가
Caching Locality와 Cache Hit Ratio에 대해 설명하시오
Call Stack에 대해 설명하시오
Heap 메모리는 무엇이고 사용하는 이유는 무엇인가
Heap과 Stack의 장단점 비교 (속도, 크기 등)
Memory Corruption이란?
Heap Corruption에 대해 설명하시오
거짓 공유에 대해 설명하시오
DMA란?
