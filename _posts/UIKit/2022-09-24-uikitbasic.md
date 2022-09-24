---
title: UIKit 기초
date: 2022-09-24
excerpt: "UIKtit의 기초를 공부해보자:)"
categories:
- UIKit
tags:
- UIKit
- iOS
---


<br />
<br />

---

# 개요

---

앱의 기본 구조, 코코아 터치, 화면의 객체 제어 방법, 오토 레이아웃에 대해 알아보겠다.

<br />

---

# 뷰 컨트롤러

---

뷰 컨트롤러는  하위에 있는 컨텐츠를 관리하고, 보여주거나 숨기는 등의 구성을 조정하는 역할을 한다. 

그래서 뷰 컨트롤러는 내부적으로 뷰를 포함하고 있으며, 뷰에 대한 관리를 주로 한다.

또 뷰 컨트롤러는 화면 전환이 발생할 때 다른 뷰 컨트롤러와 서로 통신하고 조정하는 일을 수행한다.

뷰 컨트롤러가 맡은 일이 많기 때문에 객체 간의 연결 관계를 한번에 이해하는 것은 힘들다. 그래서 스토리보드라는 것을 활용한다.

* UIScreen : 기기에 연결되는 물리적인 화면을 정의하는 객체
* UIWindow : 화면 그리기 지원 도구를 제공하는 객체
* UIView : 그리기를 수행할 객체 세트

<br />

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/192083177-4eafff40-3f18-4dd2-9ebc-577d5426d0df.jpg">
		<img src="https://user-images.githubusercontent.com/79088896/192083177-4eafff40-3f18-4dd2-9ebc-577d5426d0df.jpg" class="w8" />
	</a>
</figure>

<br />

뷰 컨트롤러는 앱 아키텍처에서 MVC 패턴을 도입하면서 생겨난 단순 컨트롤러 객체이다.

그러나 뷰 컨트롤러는 뷰와 리소스를 관리하는 역할을 맡는다. 모든 뷰 컨트롤러는 이역할을 해야하고 UIViewController 클래스 안에 있다.


<br />

---

# 엔트리 포인트

---

C언어에 뿌리를 둔 모든 앱은 main함수에서 시작한다. 이를 Entry Point라고 한다. 

objective-c는 C언어 기반 언어이므로 AppDelegate 클래스를 이용하여 UIApplicationMain() 함수를 호출하고, 그 결과로 UIApplication 객체를 반환한다.

생성된 UIApplication 객체는 UIKit 프레임워크에 속해있으므로 이후의 앱 제어권은 UIKit 프레임워크로 이관된다.

이 UIApplicationMain()함수는 iOS 앱의 엔트리 포인트라고 할 수 있다.

이 함수는 앱의 핵심객체를 생성하는 프로세스를 핸들링하고, 스토리보드 파일로부터 앱의 유저 인터페이스를 읽어들이고 커스텀 코드를 호출한다.

UIApplicationMain() 함수가 생성하는 UIApplication은 앱의 본체라고 할 수 있는 객체이다.

그러나 스위프트는 C기반의 언어가 아니다. 따라서 엔트리 포인트 역시 존재하지 않고 `@UIApplicationMain`이라는 속성을 부여한다.

앱 델리게이트 역할을 할 클래스에 이 어노테이션을 붙여서 시스템에 델리게이트 클래스 정보를 전달한다.

다음은 iOS 앱의 생명 주기이다.

<br />

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/192083990-78674bc9-c1e9-49d6-b37a-dfde2031cb49.jpg">
		<img src="https://user-images.githubusercontent.com/79088896/192083990-78674bc9-c1e9-49d6-b37a-dfde2031cb49.jpg" class="w8" />
	</a>
</figure>

<br />


<br />

---

# MVC 패턴

---

