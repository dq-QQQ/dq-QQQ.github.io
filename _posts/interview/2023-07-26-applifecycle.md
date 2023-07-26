---
title: APP & View Life Cycle
categories:
  - iOS
excerpt: "생명주기:)"
date: 2023-07-26
tags:
- iOS
---



<br />
<br />

---

# App Life Cycle

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/fa961b2a-4b21-4e9b-82ee-a86a0538b23d">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/fa961b2a-4b21-4e9b-82ee-a86a0538b23d" class="w8" />
	</a>
</figure>

* `Unattached` : 앱을 처음 실행할 때의 상태이며 시스템이 connection notification을 주기 전 까지는 유지한다.
* `Foreground Inactive` : Scene이 Foreground에 있지만 이벤트를 받지 않을 때이다. 알림창 같은 것
* `Foreground Active` : Scene이 Foreground에 있으며 이벤트를 받고 있을 때이다.
* `Background` : 실행중이지만 화면 위에서가 아니라 Background에 있을 때이다.
* `Suspended` : Background에 있으며 아무것도 실행되지 않을 때이다. 이 상태는 UIScene클래스의 상태 열거형에 없다.

여기서 점선은 특별한 Event 없이도 시스템이 자동으로 수행해주는 것, 실선은 사용자나 시스템에 의한 Event로 인해 수행되는 것이다.


<br />
<br />

---

# UIKit App Life Cycle

앱의 현재 상태는 앱이 할 수 있는 것과 없는 것을 결정한다.

예를 들면, Foreground 앱이 유저의 관심을 받고 있다면, 앱은 CPU와 같은 시스템 자원의 우선순위에 있는 것이다.

반대로 Background 앱은 화면을 점유하고 있지 않기 때문에 자원을 최소한으로만 가져야한다.

생명주기 이벤트에 반응하기 위해 iOS 13이후는 UISceneDelegate 객체를, iOS 12이전은 UIApplicationDelegate를 이용한다.

앱은 하나의 프로세스이지만 여러개의 UI 객체나 scene session을 가지게 된다. 그래서 나온 것이 UISceneDelegate이다.

AppDelegate에서 모든 생명주기를 처리했지만 이제 UI 생명주기는 UISceneDelegate이 담당한다.

이렇게 되면서 멀티태스킹으로 하나의 Window에 여러개의 Scene을 띄울 수 있게 되었다.

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/db2e823b-186e-4728-ad3c-373e5ebf76c5">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/db2e823b-186e-4728-ad3c-373e5ebf76c5" class="w8" />
	</a>
</figure>

프로그램을 하나 만들면 기본으로 생성되는 파일에 AppDelegate와 SceneDelegate가 있다.

AppDelegate에는 `didFinishLaunching`, `configurationForConnecting`, `didDiscardSceneSessions` 메서드가 있고

앱을 처음 실행하면 AppDelegate에 있는 `didFinishLaunching` 메서드가 실행되고 `configurationForConnecting`로 어떤 Scene으로 구성할 지 선택한다.

앱이 실행화면으로 들어가면 권한은 SceneDelegate이 가져가게 되는데 `willConnectTo session`으로 Window를 선택적으로 구성하고 제공된 Scene에 연결한다.

이후 앱의 상태에 따라 `sceneDidDisconnect`, `sceneDidBecomeActive`, `sceneWillResignActive`, `sceneWillEnterForeground`, `sceneDidEnterBackground`의 메서드를 호출한다.

앱을 종료시키고 메모리에서도 제거하면 AppDelegate의 `didDiscardSceneSessions`가 실행되고 앱의 한 생명주기가 끝나게 된다.

Scene은 디바이스에서 실행중인 앱 UI의 인스턴스이다. 사용자는 각각의 앱마다 여러개의 Scene을 만들고 보여지고 숨길 수 있다.

각각의 Scene들은 고유의 생명주기와 다른 실행 상태를 가질 수 있기 때문이다.

사용자나 시스템이 앱의 새로운 Scene을 요청하면 UIkit은 앱을 생성하고 Unattached 상태에 놓는다.

유저가 요청한 Scene은 Foreground로 빠르게 이동하여 화면에 띄워진다. 시스템이 요청한 Scene은 Background로 이동해서 event를 처리한다.

사용자가 화면을 앱에서 다른 것으로 전환하면, UIKit은 관련된 Scene을 background 상태로 바꾸고 얼마 안있어 Suspended state로 바꾼다.

UIKit은 언제든지 자원의 요청하여 background나 suspended Scene의 연결을 끊고 Unattached 상태로 되돌릴 수 있다.


<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/fa961b2a-4b21-4e9b-82ee-a86a0538b23d">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/fa961b2a-4b21-4e9b-82ee-a86a0538b23d" class="w8" />
	</a>
</figure>




<br />
<br />

---

# SwiftUI App Life Cycle

SwiftUI는 Scene delegate
