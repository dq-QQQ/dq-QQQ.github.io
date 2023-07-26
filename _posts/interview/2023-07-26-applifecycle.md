---
title: iOS View Life Cycle
categories:
  - iOS
excerpt: "앱 생명주기:)"
date: 2023-07-26
tags:
- iOS
---


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

