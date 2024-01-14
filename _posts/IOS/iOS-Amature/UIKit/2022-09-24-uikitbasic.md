---
title: UIKit 기초
date: 2022-09-24
excerpt: "UIKtit의 기초를 공부해보자:)"
categories:
- UIKit
tags:
- UIKit
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

뷰 컨트롤러도 상태변화와 생명주기를 가진다.

<br />

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/192087570-7db2bdbb-a688-4f52-8cf5-7da5959db7bb.jpg">
		<img src="https://user-images.githubusercontent.com/79088896/192087570-7db2bdbb-a688-4f52-8cf5-7da5959db7bb.jpg" class="w8" />
	</a>
</figure>

<br />


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

iOS 앱의 객체 관계는 MVC 패턴에 기반한다. 모델 - 뷰 - 컨트롤러로 이어지는 세개의 핵심 구조를 이용하여 앱을 설계한다.

모델은 데이터를 담당하고, 뷰는 데이터에 대한 화면 표현을 담당하며, 컨트롤러는 모델과 뷰 사이에 위치하여 데이터를 가공하여 뷰로 전달하고,

뷰에서 발생하는 이벤트를 입력받아 처리하는 역할을 담당한다. 아래는 MVC패턴과 객체들의 상호작용의 관계를 나타낸 그림이다.

<br />

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/192084330-2d74bc5d-56c1-4090-b576-efbf4e2fcf01.jpg">
		<img src="https://user-images.githubusercontent.com/79088896/192084330-2d74bc5d-56c1-4090-b576-efbf4e2fcf01.jpg" class="w8" />
	</a>
</figure>

<br />

<br />

---

# 앱의 상태 변화

---

앱은 실행되는 동안 다양한 상태로 변화한다.

앱의 상태 변화는 iOS 운영체제가 처리하는 영역이다.

* Not Running : 앱이 시작되지 않았거나 실행되었지만 시스템에 의해 종료된 상태를 나타낸다.
* Inactive : 앱이 Foreground에서 실행 중이지만, 아무런 이벤트를 받고 있지 않는 상태를 의미한다.
* Active : 앱이 전면에서 실행중이며, 이벤트를 받고 있는 상태를 의미한다.
* Background : 앱이 백그라운드에 있지만 여전히 코드가 실행되고 있는 상태를 나타낸다. 대부분의 앱은 Suspended 상태로 이행하는 도중에 일시적으로 이상태에 진입하지만, 파일 다운로드와 같이 실행시간이 필요한 앱일 경우 남아있을 때도 있다.
* Suspended :  앱이 메모리에 있지만 실행되는 코드가 없는 상태이다. 메모리가 부족해지면 삭제한다.

<br />

---

# cocoa touch

---

UIApplication, UIViewController, UILabel과 같은 클래스는 UIKit 프레임워크에 속해있다.

앱을 만들 때 수많은 프레임워크들이 필요하다.

UIKit이나 WebKit등 프레임워크 계층을 거슬러 올라가면 코코아 터치라는 하나의 거대한 프레임워크가 나타난다.

즉 코코아 터치는 애플 환경에서 터치 기반의 앱을 제작하기 위한 도구들의 모음이라고 할 수 있다.

그럼 코코아 프레임워크는 뭘까? 사파리, Xcode와 같이 터치가 필요없는 OS X에서 개발하기 위해 사용되던 프레임워크이다.



<br />

---

# iOS 프레임워크 계층

---

iOS의 프레임워크 계층은 하드웨어와 어플리케이션 사이를 연결해주는 역할을 한다.

<br />

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/192087099-3a458c40-509f-4e4d-ba07-40ff4bc870d7.jpg">
		<img src="https://user-images.githubusercontent.com/79088896/192087099-3a458c40-509f-4e4d-ba07-40ff4bc870d7.jpg" class="w8" />
	</a>
</figure>

<br />

<br />



---

## Cocoa Touch

---

코코아 터치 계층은 어플리케이션 프레임워크 계층이라고도 부르며 앱을 직접 지원하는 역항르 담당한다.

iOS에 설치되고 실행되는 모든 앱은 코코아 터치 계층에서 제공하는 여러가지 기술이나 서비스를 이용하여 기능을 구현하고 동작한다.

<br />

---

## Media

---

여기에 속한 프레임워크들은 그보다 하위인 코어 서비스 계층에 의존적이며, 상위 계층인 코코아 터치 계층에 그래픽 관련 서비스나 멀티미디어 관련 서비스를 제공한다.

대표적인 프레임워크로 CoreGraphics, CoreText, CoreAudio, CoreAnimation, AVFoundation등이 있다.

<br />

---

## Core Service

---

이 계층에 속한 프레임워크들은 문자열 처리, 데이터 집합 관리, 네트워크, 환경설정등 핵심적인 서비스를 제공한다.

또한 GPS, 나침반, 가속도 센서와 같은 하드웨어 특성에 기반한 서비스도 제공한다.

대표적인 프레임워크는 Foundation이며 하드웨어를 다루는 CoreLocation, CoreMotion, CoreAnimation, CoreData등이 있다.

<br />

---

## Core OS

---

커널, 파일시스템, 보안등 우리가 다룰일이 별로 없다.



<br />

---

# 화면 객체 제어

---

@를 붙이는 것은 어노테이션이라고 하며 컴파일러에게 변수나 메서드의 성격을 알려준다.

@IBOutlet은 프로퍼티에 @IBAction은 메소드에 추가한다. IB는 Interface Builder를 의미한다.


<br />

---

## @IBOulet

---

 화면상의 객체를 소스코드에서 참조하기 위해 사용하는 어노테이션이다. 이를 아울렛 변수라고 부른다.

 Strong과 Weak이 있는데 메모리 회수 정책 차이가 존재한다.


<br />

---

## @IBAction

---

객체의 이벤트를 제어할 때 사용하는 어노테이션이다. 액션 메서드라고 부른다.

프로그래머가 의도하는 일련의 프로세스를 실행하기 위해 추가한다.


<br />

---

# 델리게이트 패턴

---

iOS 앱의 객체는 델리게이트 패턴이라고 불리는 일종의 위임 패턴을 많이 사용한다.

델리게이트 패턴은 디자인 패턴중 하나로 객체지향 프로그래밍에서 하나의 객체가 모든일을 처리하는 것이 아니라 다른객체에게 위임하는 것을 말한다.

대부분의 GUI 기반 프로그래밍에서 사용된다.

