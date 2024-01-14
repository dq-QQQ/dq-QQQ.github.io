---
title: 옵젝시 메시징
categories:
  - Objective-C
excerpt: "옵젝시의 메시징을 공부해보자:)"
date: 2023-11-08
tags:
- iOS
- Objective-C
---

# 개요

함수호출이 아니라 메시징...이게 뭘까


<br />
<br />

---

# 메시징이란?

---

옵젝시에서는 객체가 어떤 작업을 하도록 하려면 메시지를 보낸다.

함수 호출은 컴파일 시간에 어떤 코드가 사용될 지 결정되어 고정적으로 연결되어있다.

그래서 컴파일러가 함수 호출을 만나면 호출되는 함수의 본문으로 점프하도록 jump 어셈블리어를 추가한다.

옵젝시에서는 런타임에 정하는 동적인 시스템을 사용한다. 이를 메시징이라고 하는데 오브젝트에 메시지를 전달하는 개념이다.

메시지 전송이라는 개념에는 sender, receiver, message가 필요하다.

`[receiver message]`의 형태로 사용하며 receiver는 오브젝트로 메소드를 실행시키는 주체가 되며 메시지를 수신한다.

메시지는 메소드의 이름으로, 이때 receiver는 메소드를 실행시킨다.

옵젝시의 runtime은 receiver를 확인하여 receiver의 클래스를 결정한다.

runtime은 클래스가 정의한 자신의 메소드 리스트와 각 메소드의 이름 및 실제 코드의 위치 포인터등을 가지고있다.

여기서 runtime은 C함수와 자료구조로 구성된 공유 라이브러리이다. 스위프트의 opaque이다.

sender는 메시지를 보내는 곳 즉 메시지 표현식을 포함하고 있는 코드 블록이다.

예를들어 버튼을 설정할 때 target으로 오브젝트를 등록하게 되는데 버튼을 클릭하면 버튼 오브젝트가 target에 메시지를 보낸다.

target에 보내는 메시지는 - (void) somethingChanged:(id) sender의 형태를 띈다.

이 메시지는 sender라는 인자를 가지고 있다. UIViewController는 이 메시지를 통해 자기 자신을 sender에 담아 건네준다.

그럼 제어받는 객체는 receiver이 되어 메시지를 실행하는 것이다.



<br />
<br />

---

# 메시징 예시

---

<br />

## 네스팅

---

그냥 쉽게 말해 이중으로 메시징을 할 수 있다는 뜻이다.

```objective-c
Shape *shape1 = ...
Shape *shape2 = ...
NSColor *tmpFillColor;

tmpFillColor = [shape1 fillColor] ;
[shape2 setFillcolor: tmpFillColor];

//아래의 코드는 위의 코드와 동일하게 동작한다.

Shape *shape1 = ...
Shape *shape2 = ...

[shape2 setFillcolor: [shape1 fillColor]];
```

<br />

---

## nil 메시징

---

옵젝시에서 receiver이 nil이면 아무런 일도 발생하지 않는다.

```objective-c
Shape *a = ...

if (a != nil)
{
    [a draw];
}

// 위의 코드처럼 예외처리를 하지 않아도 상관없다.

[a draw];
```

결과값의 타입이 포인터이거나 숫자인 메시지가 nil로 전달될 경우 결과값은 0이된다.

이 경우는 실행되어야할 메소드가 실행되지 않을 때 확인해볼 필요가 있을 경우이다.

<br />

---


## self로 메시지 보내기

---

만약 객체의 메소드에서 다른 메소드를 실행시키고 싶다면 receiver로 self를 사용하면된다.

self는 숨겨진 변수로 컴파일러가 self 변수를 메소드가 구현된 곳으로 넘겨준다.

이 패턴은 accessor 메소드를 사용할 때 주로 사용한다.

accessor은 인스턴스 변수의 getter, setter를 의미한다.

<br />

---

## super 오버라이딩에서 메시징

---

클래스는 동일한 메소드를 자식클래스에서 구현하는 오버라이딩이 가능하다.

오버라이드된 메소드를 실행할 때 자식클래스의 객체를 receiver로 하면 자식클래스의 코드가 실행된다.

만약 [super message]의 형태로 사용하면 수퍼클래스의 코드가 실행된다.

self는 합법적인 포인터 변수이지만 super는 아니다.

self가 가리키는 메모리 주소에는 오브젝트의 인스턴스가 있지만 super는 self를 receiver로 하고

메소드는 self가 속한 클래스의 수퍼클래스의 코드를 실행하라고 runtime에게 알려주는 표시라고 할 수 있다.

<br />

---

## Selector

---

메시지에서 메소드 이름은 가끔 selector에 의해 참조될 때가 있다.

이는 runtime이 실행시킬 receiver의 메소드를 선택하기 위하여 사용하는데 어떠한 타입도 아니라 이름일 뿐이다.

SEL이라는 타입은 selector를 가지고 있다는 것을 의미한다.

SEL은 그냥 문자열을 가지고 있으므로 동일한 이름을 가지는 selector는 동일한 SEL을 가진다.

그래서 성능상의 이슈로 많이 사용한다. 해당 메소드를 사용하겠다는 의미로

<br />

---

## 같은 이름 메소드

---

메소드 오버로딩은 옵젝시에서 지원하지 않는다.

```objective-c
#import "ClassWithFloat.h"
#import "ClassWithInt.h"

id numberObj = [[ClassWithInt alloc] init];
[numberObj setValue: 21];
```

이 경우 import된 순서대로 인식한다.

따라서 컴파일러는 ClassWithFloat에 있는 setValue를 가져와 실행하게 된다.

<br />

---

# 내부 동작

---

메시지 표현식이 실행되면 runtime은 receiver를 통해 클래스를 결정한다.

그 다음 클래스의 정보를 확인하여 메시지 안에 있는 메소드 이름과 동일한 메소드를 찾는다.

모든 옵젝시 오브젝트는 자신의 클래스를 안다. 이를 위해 컴파일러는 모든 인스턴스에 isa라는 변수를 추가한다.

실행시간에 runtime이 이 변수를 초기화하고 클래스의 정보를 알 수 있게한다.

컴파일러는 메소드를 C함수로 전환시킨다. 이러한 과정에서 두개의 외부 인자 self와 _cmd를 함수의 인자 리스트 맨앞에 추가한다.

self는 객체를 가리키는 포인터로 메시지의 receiver이 된다. _cmd는 selector로 메시지의 메소드 이름을 가져온다.

예를들어 `-(void) exHo:(int)arg1` -> `(id self, SEL _cmd, int arg1)`형태로 바뀐다.

각각의 옵젝시 클래스는 메소드의 selector와 실제 메소드가 구현된 함수 포인터가 매핑된 테이블을 가진다.

캐시도 가지고 있는데 cpu 캐시와 같은 방식이다.

```objective-c
Shape *a = ...;
NSColor *newColor = ...;

[a setColor:newColor];
```

위와 같은 코드를 컴파일러는 objc_msgSend(receiver, message, arguments)로 바꾼다.

즉 `objc_msgSend(a, @selector(setColor), newColor);`로 말이다.

objc_msgSend는 a의 isa 변수에 저장된 포인터를 찾고 Shape 클래스임을 확인 후 클래스 구조를 참조한다.

그리고 Shape의 메소드 캐시을 확인하여 setColor의 위치를 찾는다.

setColor의 캐시 참조를 실패하면 클래스의 테이블에서 찾는다.

runtime은 탐색한 함수 포인터를 이용하여 인자값들과 함께 함수를 호출한다.

objc_msgSend는 메소드를 찾기 위해 super 클래스까지 탐색한다.

이때 super 클래스에서도 찾지 못하면 NSObject 클래스의 forwardInvocation: 메소드를 최초의 표현식에서 얻은 NSInvocation 인자와 함께 호출한다.

그러면 NSObject 클래스의 doesNotRecognizeSelector: 메소드를 호출한다.

이 메소드는 예외를 발생시키고 프로그램을 종료시킨다.

