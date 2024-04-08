---
title: Publisher & Subscribers
categories:
  - iOS
excerpt: "Publisher와 Subscribers란??:)"
date: 2024-04-08
tags:
- Combine
- iOS-PRO
---



# 개요

Combine의 모든 것!

Publisher와 Subscribers!

알아보자.

[애플 공식문서](https://developer.apple.com/documentation/combine)


<br />
<br />

---

# 이해를 돕는 쉬운 예제

---

```swift
let ho = Notification.Name("ho")

let observer = NotificationCenter.default.addObserver(forName: ho, object: nil, queue: nil) { ho in
    print(ho)
}

let publisher = NotificationCenter.default.publisher(for: ho)

let subscriber = publisher.sink { ho in
    print(ho)
}
```

-   위의 코드 post하면 같은 동작


<br />
<br />

---

# Publisher와 Subscriber의 흐름

---

1.  Subscriber의 Publisher 구독
2.  Publisher가 활성화되고 subscription을 만들고 전달함
3.  Subscriber가 값 요청
4.  Publisher가 값 전달
5.  Publisher가 completion 전달
6.  Subscriber에게 더이상 값이 필요없다 -> cancel

<br />
<br />

---

# Publisher 프로토콜

---

```swift
public protocol Publisher {
  associatedtype Output

  associatedtype Failure : Error

  func receive<S>(subscriber: S)
    where S: Subscriber,
    Self.Failure == S.Failure,
    Self.Output == S.Input
}

extension Publisher {
  public func subscribe<S>(_ subscriber: S)
    where S : Subscriber,
    Self.Failure == S.Failure,
    Self.Output == S.Input
}
```

-   Output, Failure 두개의 값을 가지고 있음
-   Subscriber는 subscribe 메서드를 호출하여 publisher에 등록
-   subscriber 메서드는 receive 메서드 호출하여 subcription 생성


<br />
<br />

---

# Subscriber 프로토콜

---

```swift
public protocol Subscriber: CustomCombineIdentifierConvertible {
  associatedtype Input

  associatedtype Failure: Error

  func receive(subscription: Subscription)

  func receive(_ input: Self.Input) -> Subscribers.Demand

  func receive(completion: Subscribers.Completion<Self.Failure>)
}
```

-   publisher가 보내준 값(output)
-   publisher가 보내준 에러
-   publisher가 만들어준 값들



<br />
<br />

---

# Subscription 프로토콜

---

```swift
public protocol Subscription: Cancellable, CustomCombineIdentifierConvertible {
  func request(_ demand: Subscribers.Demand)
}
```

-   publisher와 subcriber의 소통 창구
-   Demand는 Malloc 얼만큼 할지 같은 느낌?

<br />

---

# Just

---

-   단일 값에 대한 publisher
-   Just(5).sink~~~ 형태로 사용

<br />

---

# Future

---

-   비동기 작업의 결과를 생성하는 publisher
-   값을 생성하는 클로저를 실행완료할 때까지 대기
-   Future객체는 바로 생성되지만 값이나 오류는 완료되어야 알수있음




<br />

---

# sink

---

-   publisher를 구독하는 방법 중 하나
-   호출하면 Subscriber가 생성되고 Publisher가 전달하는 값을 처리
-   클로저를 이용해 값을 처리하며 반환하지 않음
-   간단한 Subscriber로 콘솔 출력, UI 업데이트등 간단한 로직에 사용

<br />

---

# assign

---

-   publisher가 전달한 값을 Subscriber에 할당하는 역할
-   KeyPath를 사용하여 사용
-   ViewModel 바인딩에서 주로 사용


<br />

---

# subscribe

---

-   커스텀 subscriber를 publisher에 연결하는 방법


<br />

---

# PassthroughSubject

---

-   값을 전달하는 Publisher
-   들어온 값 그대로 Subscriber들에게 내보냄
-   현재 값을 저장하지 않음

<br />

---

# CurrentValueSubject

---

-   값을 저장하고 그 값을 전달하는 Publisher
-   초기 값을 가지고 있으며 현재 값을 저장함

<br />

---

# 요약

---

-   Publisher는 시간의 흐름에 따라 구독자들에게 동기/비동기적으로 값을 전달하는 객체
-   Subscriber는 값을 받기 위해 Publisher와 연결함
-   따라서 Subscriber.input.type == Publisher.output.type이어야함
-   Publisher를 구독할 수 있는 sink, assign 두개의 메서드가 있음
-   Subscriber는 demand를 증가시킬 수 있다. 감소는 못함
-   값 전달이 끝났다. 그럼 cancel 시켜야 안전함
-   subscription을 AnyCancellable에 저장시키면 자동으로 cancel해주고 메모리 관리해줌
-   future은 단일 값을 비동기적으로 받을 수 있음
-   Subject는 Subscriber에게 비동기적으로 여러개의 값(값 스트림으로)을 전달할 수 있는 Publisher