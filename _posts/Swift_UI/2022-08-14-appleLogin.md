---
title: SwiftUI apple 로그인
categories:
  - SWIFTUI 
excerpt: "SwiftUI로 apple 로그인을 하는 기능에 대해서 공부해보자:)"
date: 2022-08-14
tags:
- SwiftUI
---



# 개요

SwiftUI로 앱에 애플 로그인 기능을 구현해보겠다.


[구현코드](https://github.com/dq-QQQ/SwiftUI_Example/tree/main/SignInWithApple)

<br />
<br />

---

# Apple Login

---

애플은 구글이나 카카오같은 써드파티 로그인 기능들도 애플로그인을 구현하는 방법을 사용하라고 강제한다.

애플로그인 기능은 시뮬레이터나 프리뷰에서는 테스트가 불가능하다. 실제 아이폰이 있어야한다.

프레임워크는 로그인 처음할 때 유저 정보를 저장한다.

예제에서는 iOS의 `@AppStorage("name")` 프로퍼티 래퍼를 사용해서 `UserDefaults`에 저장할 것이다.

그러나 UserDefaults에 저장하는 것은 위험하기 때문에 실제 앱에는 저장하면 안된다.

실제 앱은 keychain에 무조건 저장해야한다.

애플은 Logout API를 제공하지 않는다. 그래서 인증 정보를 설정에가서 지워야한다.


<br />
<br />

---

# 구현

---

<br />

---

## Sign in Apple Permission 받기

---

* 앱 설정의 Target 설정으로 가기
* 만약 Xcode에 내 계정이 로그인 되어있다면 안뜰 수 있으니 Automatically manage signing 체크해제
* Sign in with Apple Entitlements File 추가
* 소스파일 폴더안에 체크모양 파일이 만들어지면 완료

<br />

---

## Sign in Apple 버튼 생성하기

---

`import AuthenticationServices` 해야한다.

`SignInWithAppleButton`을 사용하면 흔히 보는 버튼을 사용할 수 있다.

signIn인지 signUp인지 설정할 수 있다. onRequest, onCompletion파라메터가 있다.

버튼 스타일도 지정할 수 있다.