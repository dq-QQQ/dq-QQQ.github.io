---
title: iOS의 프레임워크란
date: 2024-01-18
excerpt: "iOS의 프레임워크를 공부해보자:)"
categories:
- iOS
tags:
- Framework
- Library
- iOS-PRO
---



## 개요

xCode Target으로 앱을 만들 수도 있지만 프레임워크와 정적 라이브러리를 만들 수 있다.

기존에는 static library로 빌드해서 .a 파일을 만들고 이 .a 파일을 다른 프로젝트에 심어서 사용하였다.

이 파일을 이용해서 프레임워크를 만들수도 있는데 이 방법에 대해 알아보고 다른점에 대해서 알아보겠다.

---

## Library

-   라이브러리는 다른 프로젝트에서 사용할 수 있는 함수, 클래스, 상수, 변수등을 모은 것
-   재사용성을 높이고, 모듈화를 하여 관리의 용이성을 높이기 좋음
-   코드를 바이너리 파일로 제공하므로 라이브러리를 만들 때 public으로 설정한 헤더를 제외하고는 코드를 볼 수 없음
-   라이브러리가 링크되는 시점으로 Static, Dynamic이 나눈다 컴파일 시점, 런타임 시점으로 흔히 사용하는 개념과 동일한 개념

---

## Framework

-   프레임워크는 라이브러리, nib, 이미지, 헤더파일, 레퍼런스등을 단일 패키지로 캡슐화한 디렉토리
-   라이브러리와 사용 방법, 사용 이유, 종류 등이 유사함

---

## Static Library / Framework

-   생성방법
    -   Static Library를 Target에 추가
    -   Build Phase -> Compile Sources에 라이브러리로 만들 소스파일을 추가
    -   해당 파일의 인터페이스나 헤더가 있다면 Build Phase -> Headers -> Project에 추가
    -   여기서 Public으로 넣는다면 라이브러리가 만들어진 경로에 복사가 됨
    -   Build Setting에서 **Mach-O Type**을 **Static Library**로 설정
    -   빌드 후 product로 .a파일 확인

-   특징
    -   .a 파일은 설정한 소스파일을 컴파일하고 오브젝트 파일을 링크한 결과
    -   소스파일의 크기가 커지거나 컴파일하는 소스파일의 수가 늘어나면 크기가 늘어남
    -   정적 라이브러리로 만들면 모든 기능이 .a파일에 포함됨
    -   외부 의존성이 없어 이식성이 좋지만 업데이트 하려면 다시 빌드해야하는 단점이 있음
    -   컴파일 시간 오래걸림. 런타임 빠름. 메모리 사용량 많음
    -   .a 파일을 만드는 프로젝트의 경로보다 .a 파일을 사용하는 프로젝트의 경로가 중요함  
        -   #include "ho/hoho.h" 이 헤더 경로는 .a 파일을 만드는 소스에 있어도 컴파일하는 소스가 기준이 아님

---

## Dynamic Library / Framework

-   생성방법
    -   Static Library를 만들 때 했던 작업에서 **Mach-O Type**을 **Dynamic Library**로 설정
-   특징
    -   .dylib 파일은 소스파일들의 심볼 및 위치를 저장한 결과
    -   소스파일의 크기가 커지거나 수가 많아져도 .dylib 파일의 크기는 크게 다르지 않음
    -   파일들을 모두 이식하고 런타임에 해당 라이브러리를 찾아야하므로 이식성이 좋지 않음
    -   컴파일 시간 빠름. 런타임 오래걸림. 메모리 사용량 적음
    -   사용하는 경로도 중요하지만 .dylib 파일을 만드는 경로가 맞지 않으면 파일이 만들어지지 않음
        -   #include "ho/hoho.h" 이 헤더 경로가 .dylib 파일을 만드는 소스 기준으로 없으면 안됨

---

## Mach-O Type

-   Target을 빌드한 후 나오는 바이너리 파일의 형식
-   NextStep 운영체제에서 사용하던 Mach-O 커널에서 유래 (현재 Apple은 XNU 커널)
-   Type의 종류
    -   Executable : 메인 타겟 (앱)
    -   Dynamic Library : .dylib
    -   Bundle : 코드없는 리소스
    -   Static Library : .a
    -   Relocatable Object File : 링크 전의 Dynamic Library

---

## XCFramework

[https://developer.apple.com/videos/play/wwdc2019/416/](https://developer.apple.com/videos/play/wwdc2019/416/)

 [Binary Frameworks in Swift - WWDC19 - Videos - Apple Developer

Xcode 11 now fully supports using and creating binary frameworks in Swift. Find out how to simultaneously support devices and Simulator...

developer.apple.com](https://developer.apple.com/videos/play/wwdc2019/416/)

---

## 적용 방법

애플 공식문서에서 설명하는 Static Library 과정

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/95582d20-6b60-4d21-9dc9-d1ac94c953c2">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/95582d20-6b60-4d21-9dc9-d1ac94c953c2" class="w8" />
	</a>
</figure>

<br />


애플 공식문서에서 설명하는 Dynamic Library 과정

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/69f06383-bfad-4272-b0c5-b7f1a45e5843">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/69f06383-bfad-4272-b0c5-b7f1a45e5843" class="w8" />
	</a>
</figure>

<br />




---

## 라이브러리와 프레임워크 차이점