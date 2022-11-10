---
title: 스위프트의 프로토콜
categories:
  - SWIFT
excerpt: "스위프트에서의 프로토콜을 공부해보자:)"
date: 2022-07-26
tags:
- iOS
- swift
---



# 개요

---


스위프트는 흔히 프로토콜 지향 언어라고 한다.

프로토콜을 들어본곳은 네트워크에서 통신 프로토콜밖에 없는데 프로토콜이 무엇인지 알아보고 무엇이 프로토콜 지향 프로그래밍인지 알아보겠다.

<br />
<br />

---

# 프로토콜

---

프로토콜이란 특정 작업이나 기능들의 프로토타입이다. 애플 공식문서에는 blueprint라고 설명한다. 다른언어의 인터페이스 느낌이다.

프로토콜은 클래스 구조체 열거형에 의해 adopted(채택)되어 요구사항들을 구현하도록 한다. 이들은 해당 프로토콜을 conform(준수)했다고 표현한다.

프로토타입이라고 말했는데 프로토콜은 정의만하고 구현은 하지 않는다. 네트워크에서 프로토콜의 의미는 통신을 하기위한 약속이라고 한다. 여기에서도 같다.

이 클래스는 이러이러한 변수를 가지고 있고 기능들을 가질거야라고 약속을 하는 것이라고 보면된다.

다른 언어에서의 Interface라고 생각하면 된다.

<br />
<br />

---

# 명령전달

---

스위프트의 프로토콜은 옵젝시 프로토콜의 superset이다. 옵젝시에서 모든 메서드는 런타임시 메시지를 이용해서 dynamic dispatch를 사용하지만 스위프트는 다양하다.

스위프트는 기본적으로 특정 클래스에서 사용가능한 메서드 목록을 담은 vtable기법을 사용하는데, 컴파일 시 생성된 vtable은 인덱스값으로 접근할 수 있는 함수 포인터를 지원한다.

컴파일러는 vtable을 메서드 호출 시 적절한 함수포인터를 찾기 위한 참조용 테이블과 같이 사용하고 옵젝시 클래스의 상속을 받은 클래스는 이를 이용해서 런타임에 명령을 전달한다.

메서드에 `@objc` 속성을 부여하면 강제로 dynamic dispatch가 적용된다.

<br />
<br />

---

# 프로토콜 사용방법

---

상속과 같은 방법으로 사용하면 되는데 클래스에서는 상속할 클래스를 먼저 쓰고 프로토콜을 쓴다.

프로토콜은 프로퍼티가 읽기 전용일지 읽기 쓰기가 모두 가능한 것인지를 알려줘야한다.

만약 get set특성을 모두 부여한다면 상수 저장 프로퍼티와 읽기 전용 연산 프로퍼티는 사용할 수 없다.

프로퍼티는 항상 var로 선언한다.

타입 프로퍼티를 요구하려면 static 키워드를 똑같이 사용하면 된다. class 타입 프로퍼티도 static으로 선언한다.

메서드도 요구할 수 있다. 만약 해당 메서드가 내부의 값을 변경한다면 `mutating`키워드를 적는다. 열거형이나 구조체는 그대로 적고 클래스는 생략해도된다.

프로토콜도 상속할 수 있다.

```swift
protocol Naming {
  var name: String { get set }
  static var surname: String { get }
  func toUpper() -> String
}

struct Info: Naming {
  var name: String
  static let surname = "Lee"
  func toUpper() -> String {
    return (Info.surname + name).uppercased()
  }
}

var ho = Info(name: "kyujin")

print(ho.toUpper()) // LEEKYUJIN
```


<br />
<br />

---

# associatedtype

---

프로토콜에서 제네릭을 사용하고 싶으면 associatedtype을 사용하면된다.

```swift
protocol View {
    associatedtype Body: View
    var body: Self.Body { get }
}
```



<br />
<br />

---

# 프로토콜 확장

---

이미 정의되어있는 프로토콜에 기능을 추가할 수 있다.

프로토콜 뿐만 아니라 구조체, 클래스, 열거체에도 추가할 수 있다.

확장은 말그대로 타입에 새로운 기능을 추가하는 것일 뿐 재정의할 수는 없다.

추가할 수 있는 요소는 다음과 같다.

* 연산프로퍼티
* 메서드
* 이니셜라이저
* 서브스크립트
* 중첩 타입
* 프로토콜 기능추가

```swift
extension Int {
  var isEven: Bool {
    return self % 2 == 0
  }
}
print(1.isEven)// false
```




<br />
<br />

---

# Identifiable Protocol

---

값 타입은 현재 상태를 통해 비교를 한다. 하지만 상태는 항상 변할 수 있으며 고유의 식별자가 없으면 다른 것을 같다고 인식할 수 있다.

참조타입은 상태의 변화와 관계없이 비교한다. 그러나 여러 프로세스에 분산되어 처리되는 경우와 같이 메모리 주소만으로만으로 완벽하게 식별할 수 없다.

따라서 Entity(개체)에 상태와는 무관한 식별자를 제공하기 위해 Identifiable Protocol을 사용한다.

공부하면서 느낀점은 데이터베이스의 Primary Key와 같은 개념 같았다.

이 프로토콜은 Hashable 프로토콜을 준수하는 id 프로퍼티 하나만 가진다.

```swift
protocol Identifiable {
  associatedtype ID: Hashable
  var id: Self.Id { get }
}
```

이 프로토콜을 채택한 타입은 고유한 개체를 구분하기 위해 비교 알고리즘에 이 id를 사용한다.

id는 다음 특징을 가질 수 있다.

* UUID와 같이 유일성을 보장한다.
* DB의 record key와 같이 환경 별로 유일하다.
* global incrementing integer처럼 프로세스의 lifetime에는 유일하다.
* object identifiers처럼 객체의 lifetime에는 유일하다.
* collection indices처럼 현재 collection에서는 유일하다.

id는 보통 Int, String, UUID, URL등의 타입을 사용한다.

```swift
//그냥 id 사용
struct Example: Identifiable {
  let id: UUID = UUID()
}

// 다른 변수를 id로 채택
struct Example: Identifiable {
  var id: UUID { uuid }
  var uuid = UUID()
}

struct Example {
  var id: UUID
}
extension Example: Identifiable {}
```

