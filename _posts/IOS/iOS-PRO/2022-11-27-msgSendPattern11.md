---
title: UIKit에서의 데이터 전달
categories:
  - iOS
excerpt: "앱의 runLoop와 델리겟, 알림 리스폰더등의 패턴을 알아보자:)"
date: 2023-11-27
tags:
- UIKit
- iOS-PRO
---

# 개요

앱을 실행하면 어떤 동작을 하는 지와 데이터를 어떻게 

<br />
<br />

---

# Application RunLoop

---

GUI를 사용하는 iOS는 사용자와 상호작용하며 동작한다. 사용자나 내부적인 이벤트등을 iOS는 감지하고 그에 따른 처리를 하는 동작을 반복한다. 이것을 run loop라고 부른다.


<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/bf0dc181-76fe-44cc-a2b9-49d2be65fb59">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/bf0dc181-76fe-44cc-a2b9-49d2be65fb59" class="w8" />
	</a>
</figure>

<br />

런루프는 OS에서 넘어온 이벤트의 종류와 상태에 따른 처리를 한다.

이벤트들은 이벤트 큐에 저장되며 순차적으로 처리된다. 이벤트 큐가 비어있다면 앱도 쉬는 상태가 된다.

이벤트들은 특정 객체에 메시지를 전달될 것이다. 이 작업을 런루프가 해주며 개발자는 어떤 동작을 하는 지만 잘 짜면된다.

앱이 실행되면 한 개의 런루프는 무조건 생성되고 앱의 생명주기와 리소스 관리를 하는 객체인 UIApplication이라는 클래스 인스턴스가 실행된다.

이 인스턴스는 OS에서 전달된 이벤트에 대응하는 객체를 선택하고 적절한 메시지를 전송한다.

인스턴스에 접근하기 위해서는 sharedApplication이라는 클래스 메서드를 사용하는데 이 메서드는 싱글톤 패턴으로 되어있다.

UIApplication()은 UIKit 프레임워크에서 제공하는 함수로 앱의 초기설정은 main함수에서 하는 것이 아닌 UIApplication 델리게이트 객체 안에 작성해야한다.

런루프가 있으면 어떤 이벤트가 발생했을 때 이벤트 큐에 대기시키고 나중에 순서대로 실행할 수 있다.

이러한 특징은 멀티스레딩에서 비동기적인 동작에 활용되는데 앱이 멀티스레드로 동작할 때는 앱의 메인 런루프 이외에

각 스레드마다 런루프를 실행해서 스레드간의 통신을 구현할 때 사용하는 개념이다.

일정 시간 후 또는 일정 시간 간격으로 메시지 송신을하려면 병렬 처리에 대한 개념을 알아야한다.

Foundation에는 지정한 메시지를 일정 시간 후에 실행시키기 위한 NSTimer클래스가 있다. 이를 타이머라고 부른다.

이 타이머를 이용할 수도 있고 performSelector를 이용할 수도 있다.


<br />
<br />

---

# delegate

---



객체가 용도에 따라 기본 동작을 변경하거나 추가 작업을 수행하기 위해 참조하는 객체를 델리게이트라고 부른다.

델리게이트는 실행 중에 동적으로 할당할 수 있는데 객체가 서로 기능을 분담하고 연계하며 작동하도록 하는 디자인 패턴이다.

객체지향에서는 어떤 객체가 처리할 수 없는 메시지를 받았을 때 다른 객체에 처리를 대신하게 하는 구조라고 정의한다.

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/184c60b0-9e8f-4e00-b36a-47a48554933a">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/184c60b0-9e8f-4e00-b36a-47a48554933a" class="w8" />
	</a>
</figure>

<br />

그러나 iOS 개발에서는 불가능한 처리를 하는 개념보다는 내가 할 수 있는 처리를 추가하고 위임하는 개념이다.

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/bc7a3853-397a-4686-9c5a-e2478e6597b8">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/bc7a3853-397a-4686-9c5a-e2478e6597b8" class="w8" />
	</a>
</figure>

<br />

델리게이트를 사용하면 독립성과 범용성 높아지고 특히 클래스에서 유용하다. 

예를 들어 UIAccelerometer라는 가속도 센서를 이용해 기기의 정보를 알고 싶은 경우가 있다. 

객체를 하나 만들어서 이것을 UIAccelerometer 인스턴스에 대한 델리게이트로 등록한다.

앱의 설계에 따라 기기의 정보가 항상 필요할 때가 있고 특정 변화가 있을 때만 필요할 때가 있다.

이때 기기의 정보를 얻기 위한 동작에서 UIAccelerometer에 직접 접근하는 것이 아니라 델리게이트 쪽의 프로그램에서 구현한다.

근데 이 델리게이트는 SwiftUI에서 잘 활용하지 않는다고 한다. @State와 같은 프로퍼티 래퍼를 이용해서 데이터 흐름을 다룬다.

UIKit상에서 델리게이트 패턴의 목적 중 하나는 객체 간의 결합도를 낮추고 특정 객체의 동작을 다른 객체에 위임하며 나의 데이터를 다른 곳에서 업데이트하고 싶을 때 사용하는데 SwiftUI는 상태를 중심으로 한 선언적인 방식이기 때문에 뷰를 구성하고 관리하는 데 더 많은 초점을 두고 있다.

<br />
<br />

---

# Notification Center

---

개발을 하다 보면 사이렌과 같이 나의 상황을 널리 알리고 싶은 경우가 있다.

iOS에서는 Foundation 프레임워크에서 Notification을 제공하여 메시지 전송을 할 수 있다.

앱에는 notification center라는 객체가 있다. 알림을 받고 싶은 객체는 미리 어떤 알림을 받고 싶은 지 center에 등록한다.

어떤 객체가 메시지 전송 요청을 notification center로 보낸다. 이것을 post 한다고 부르며 post 하면 등록된 객체 모두에게 메시지가 전송된다.

여기서 notification center에 등록된 객체는 observer라고 부른다. 객체가 notification center에 등록할 때 어느 이름의 알림을 어떤 실렉터의 메시지로 받고 싶은 지, 그리고 알림 수신방법 또한 정한다.

어떤 객체라도 알림 post를 자유롭게 할 수 있다. observer가 없어도 되고 어떻게 구현되어 있는지 모른다.

송신과 수신 객체가 알아야 하는 것은 알림의 이름뿐이다.

notification center에 post 할 경우 NSNotification 클래스 인스턴스에 담아 알림 센터에 넘긴다. 이때 알림은 다음과 같은 정보를 가지고 있다.

-   name : 알림을 식별하기 위한 이름
-   object : 알림과 함께 보내는 객체이며 보통 자기 자신을 보내지만 nil을 보낼 수도 있다.
-   userInfo : 알림과 관련된 정보를 보낼 수 있지만 보통 nil이다

알림을 포스트하려고 메서드를 호출하면 관련된 observer 모두에게 알림 메시지가 순차적으로 전달되고 처리가끝나면 post 메서드도 종료된다.

그러나 비동기로 포스트 하고 싶거나 같은 알림이 있다면 notification queue를 이용해 알림 객체를 저장되어 FIFO 형태로 notification center에 등록된다.

알림을 큐에 추가한 다음 runLoop가 하고 있는 작업이 끝나면 알림을 post한다. 그렇게 되면 알림을 큐에 추가하는 메서드는 독립적으로 실행되며, 결과를 기다리지 않고 다음 코드를 실행한다.


<br />
<br />

---

# 공통점

앱에서 발생한 이벤트가 현재 화면이 아닌 다른화면까지 영향을 줄 때 사용한다. 그러기에 결과는 같다.

모두 앱 내부에서 이벤트를 처리하거나 데이터를 전달하는 데 사용되는 패턴이다.

두 방식 모두 값의 변화를 포착하여 이벤트를 발생시킨다.

<br />
<br />

---

# 차이점

1대1, 1대다의 객체간 관계가 있다.따라서 Delegate은 객체간 상호작용이 필요한 경우, Notification은 한 이벤트에 여러개의 객체가 반응할 때 사용한다.

Delegate은 프로토콜을 사용하여 델리게이트 객체가 해당 프로토콜을 구현하는 방식으로 등록하지만 Notification은 NotificationCenter라는 외부객체를 이용한다.

Notification 방식은 수신자가 발신자의 정보를 모르지만 Delegate은 알고있다.

Notification은 어떤 값의 변화를 포착하여 상응하는 이벤트를 발생하기만 하면 된다.

Delegate은 객체의 틀을 프로토콜로 잡고 값의 변화를 저장한 변수를 추적하며 이벤트처리 메서드를 요구한다.


<br />
<br />

---

# SwiftUI에서 데이터 송신 패턴

---


delegate와 Notification Center는 UIKit에서 데이터 흐름과 상호작용을 처리하는 주요 패턴 중 일부다.

UIKit에서는 이러한 패턴들을 사용하여 객체 간 통신, 데이터 송수신, 이벤트 처리 등을 관리한다.

SwiftUI에서는 UIKit과는 다르게 뷰와 데이터의 상태에 중심을 두고 데이터 흐름을 관리하는데 프로퍼티 래퍼를 활용한다.

delegate와 Notification Center를 대체하는 것으로 @State, @Binding, @ObservableObject, @EnvironmentObject등을 활용하여 데이터를 관리하고 전달한다.