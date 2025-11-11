---
title: ios 디버깅
date: 2025-11-03
excerpt: "나만의 디버깅 기법"
categories:
- iOS
tags:
- iOS-PRO
---


# 개요

버그가 많다.

겁나 많다.

xcode에서 안잡아주는것도 있다.

그럼 굉장히 골치아프다

디버깅 기법 공부해보고 써먹자

<br />

---

# 런타임 디버깅

<br />

## Breakpoints

-   일반적인 디버깅 방법 edit을 활용해서 condition, action등을 설정할 수 있음
-   이외에도 디버깅 창으로 가면 더 있음
    -   Swift Error Breakpoint : Swift에서 예외 발생 시 행, Type을 활용해서 특정 타입 에러 확인
    -   Exception Breakpoint : objc, cpp 예외 발생 시 행, 항상 키는거 추천
    -   Symbolic Breakpoint : 행 걸고 싶은 함수 이름 쓰면 됨, objc는 풀네임으로 swift는 맹글링 규칙에 따라
    -   Runtime Issue Breakpoint : Diagnostics에 Runtimer으로 시작하는 부분에서 경고를 감지하면 행
    -   Constraint Error Breakpoint : AutoLayout 제약조건 충돌하면 행
-   Xcode의 스텝 버튼을 Control + Shift 키를 누른 채로 클릭하면, 현재 스레드만 한 단계 실행하고 나머지 스레드는 행


<br />


## Name Mangling 

-   Objective-C Property
    -   @property (nonatomic, strong) NSString *name; 이런 프로퍼티는 컴파일러가 자동으로 getter/setter를 생성
-   Swift Property
    -   모듈명.클래스명.프로퍼티명.(getter|setter)로 자동생성

<br />


## LLDB

<br />

### 자주 쓰는 명령어
    -   po(print object) : 변수를 확인할 때 pretty print, debugDescription 출력
        -   debugDescription과 description은 오버라이드 가능 (CALayer와 같이)
    -   p : raw 구조로 print, `expression --`랑 같으며 코드를 실행함
    -   v : 코드를 실행하지 않고 메모리에서 값을 읽어옴
    -   e(expression) : 앱을 재시작하지 않고 런타임에 코드를 주입할 수 있음
    -   bt : 크래시가 났을 때 현재 스레드의 함수 콜스택을 프린트 (디버그 네비게이터랑 같음)

<br />

### 디버깅 컨텍스트

-   행이 걸릴 때, Swift or Non-Swift로 나뉘어 디버깅 컨텍스트를 사용함
-   Swift 컨텍스트에서 `po [UIApplication SharedApplication]과 같이 ObjC 문법을 입력하면 에러 발생 
-   일시정지로 멈추면 기본값인 Non-Swift 컨텍스트 사용 이 때 po UIApplication.shared와같이 swift 문법 입력시 에러발생
-   `-l`(language) 플래그로 컨텍스트를 강제로 지정 가능함
    -   Objective-C 문법 강제: `expression -l objc -O -- [UIApplication sharedApplication]`
    -   Swift 문법 강제: `expression -l swift -O -- UIApplication.shared`




<br />

---

# Diagnostics

edit scheme 가면 있는 Diagnostics 옵션에 대해

<br />

## Address Sanitizer

-   런타임시에 발생하는 C/C++/Obj-C 기반 메모리 손상 버그를 찾아내는 기능
-   섀도우메모리: 앱이 사용하는 메모리 공간의 8분의1에 해당하는 별도의 메모리 공간
    -   8바이트마다 해당 메모리의 상태를 기록하는 1바이트의 섀도우바이트있음
    -   0: 8바이트가 모두 유효함
    -   1~7 : 8바이트가 꽉차지 않은 할당
    -   음수(F*) : 스택, 힙, 데이터 등등 접근금지 코드
-   ASan은 컴파일시에 메모리 접근 가능 여부를 확인하는 코드를 삽입함
```C
*addr = value;
------>>>
shadow_byte_addr=(addr>>3) + offset;
shadow_byte_value=*shadow_byte_addr;

if (shadow_byte_value!=0)
    check_memory_access(addr, shadow_byte_value);

*addr=value;
```    
-   >>>3은 섀도우바이트 가져오는것
-   access함수에서 음수면 프로그램 강제종료
-   레드존 : 메모리가 할당될 때 해당 메모리 앞뒤로 여분의 공간을 만들고 그 공간에 접근하면 섀도우바이트에 기록
-   탐지되는 메모리 오류
    -   해제된 메모리에 다시 접근하려고 할 때
    -   해제된 메모리의 이중 해제
    -   할당되지 않은 메모리 해제
    -   함수 반환 후 스택 메모리 사용
    -   버퍼 오버플로우, 언더플로우


<br />

### Detect use of stack after return

```C
int *func() {
    int value = 42;
    return &value;
}

void doSomething() {
    int *pt = func();
    *pt = 43;
}
```

-   함수 반환 후에 스택 메모리를 사용하는 지 탐지하는 기능
-   성능상의 문제로 기본적으로는 비활성화

<br />

## Thread Sanitizer

-   멀티스레딩 환경에서 Data Race 버그 감지용 런타임 Sanitizer
-   ASan처럼 섀도우메모리를 사용해 어떤 스레드가 언제 접근했는지 모든 메모리 접근을 감시함
-   모든 메모리 접근을 감시하므로 성능 저하가 매우매우 큼
-   탐지되는 오류
    -   Data Race
    -   inout이나 캡처리스트에서 발생하는 swift access races    
    -   pthread_mutex_init으로 생성하지 않은 뮤텍스를 lock
    -   Thread.detach() 등으로 생성한 스레드가 작업이 끝난 뒤에도 종료되지 않고 계속 남아있는 경우

<br />

## Undefined Behavior Sanitizer

-   Swift에서는 사용불가
-   개발자가 할리가 없는 실수를 잡아내는것(INT_MAX에 1을 더하거나, 0으로 나누기등등)

<br />

## Main Thread Checker

-   UI 변경을 메인스레드에서 하지 않는 상황 감지

<br />

## Thread Performance Checker

-   진단 도구가 아니라 프로파일링 도우미 역할
-   Time Profiler에서 앱이 어디서 시간을 낭비하는지 찾아낼수있음
-   Thread State Trace에서 스레드의 상태(Runnint, Blocked, Idle)를 보고 왜 일안하는지 감시

<br />

## Hardware Memory Tagging

-   ASan과 같으나 CPU가 모든 메모리 접근을 실시간으로 검사하는 하드웨어 메모리 보안기능
-   성능 저하가 없어 release빌드에서도 항상 켜둘 수 있음
-   메모리 포인터가 생성될 때 CPU는 해당 포인터의 사용되지 않는 상위 비트에 태그를 붙임
-   malloc으로 실제 할당이 되고 그곳을 가리키는 포인터와 동일한 태그를 붙임
-   CPU는 해당 메모리에 접근이 될 때마다 두 태그를 비교함
-   좋은 기능이지만 너무 엄격하게 검사해서 디버깅할 때나 활성화, 태그가 다르면 앱 크래쉬 발생

<br />

## Fall back to Guard Malloc

-   매우매우매우 엄격한 것 malloc 대신 libgmalloc이라는 특수 할당자를 사용함
-   이 할당자는 10바이트 할당에도 최소 1개의 가상메모리페이지(4kb or 16kb)를 통째로 할당
-   잘안씀

<br />

## Malloc Scribble

-   할당은 되었으나 초기화 되지않은 메모리 사용과 해제된 메모리 사용 버그 감지

<br />

## Malloc Guard Edges

-   오버플로우, 언더플로우 감지

<br />

## Zombie Objects

-   Use-after-free 감지
-   rc가 0이 되어도 메모리에서 해제시키지않음
-   이 객체를 초기화하고 isa 포인터를 _NSZombie로 바꿔치기함
    -   isa 포인터 : 객체가 어떤 클래스인지 가리키는 포인터
-   이 객체에 다시 접근하면 NSZombie가 가로채서 앱 크래쉬


<br />

## Malloc Stack Logging

-   릭을 잡을 때 유용
-   Instruments에서 릭을 잡을 때 해당 누수가 어떤 코드에서 할당했는지 추적 가능

<br />

## API Validation

-   개발자가 Metal API를 부적절하게 호출하는 것을 감지

<br />

## Shader Validation

-   개발자가 Metal API를 부적절하게 호출하는 것을 더 엄격하게 감지

<br />

## Show Graphics Overview

-   앱의 그래픽 성능을 HUD로 보여줌

<br />

## Log Graphics Overview

-   앱의 그래픽 성능을 로깅함


<br />

# Logging

-   print (swift)
    -   stdout으로 콘솔에 출력
    -   출력할 문자열만 표시
    -   동기식으로 빠르게 출력만함
-   NSLog (objc)
    -   stderr로 출력하여 시스템 로거랑 동기로 통신
    -   출력할 문자열 + 앱 + pid + threadID, 타임스탬프등등 메타데이터 포함
-   Logger (swift) / os_log (objc)
    -   비동기로 시스템 로깅하여 제일 빠름
    -   debug, info, error, fault 등 로그의 중요도를 설정가능
    -   변수값 비공개 처리(콘솔에서는 확인 가능)





<br />

---

# Instruments

많이 쓰는 도구 3가지

앱이 느릴때 사용하는 Time Profiler, 메모리 잡을 때 사용하는 Leaks, 네트워크 체크하는 Networks

<br />

## Time Profiler

-   앱에 행이 걸리거나 뭔가 느리다, 버벅인다 하는 작업을 찾을 때 사용
-   일반적으로 메인스레드에서 무거운 작업을 하거나, 메인스레드가 우선순위가 낮은 다른 스레드의 작업을 기다리는 경우 행
-   행은 100ms미만이 이상적, 250ms이상이면 딜레이가 눈에 보임
-   메인 스레드가 Busy, Blocked된 것인지를 구분하는 것이 중요
-   busy는 짧지만 자주호출될때, block은 너무 오래걸릴때
-   동기식 행 : 메인스레드가 무거운 작업을 동기적으로 처리할 때
-   비동기식 행 : 완료된 비동기 작업들의 콜백이 메인스레드로 몰려들 때 발생
-   대부분의 해결책은 동기적인 작업을 비동기적으로 변경하여 메인 스레드의 부담을 덜어주는 것

<br />


### 비동기

-   데이터 로직은 백그라운드 스레드에서, UI 업데이트 로직은 메인 스레드에서
-   비동기 전환에도 비용 발생, 컨텍스트 스위칭 발생, Data Race 발생, 디버깅 까다로움
-   메인스레드를 1ms ~ 2ms 이상 잡고있으면 비동기로 전환 했을 때 유리
    -   네트워크, 디스크, DB I/O
    -   무거운 JSON 파싱
    -   이미지 처리(리사이징, 필터 적용 등)
    -   복잡한 연산(암호화, 대규모 배열 정렬 및 필터링)
-   메인 스레드는 절대 대기하거나 일하지 않고, 항상 반응할 수 있도록 유지
-   async 키워드가 붙으면 이 함수는 일시 중지 될 수 있습니다 라는 뜻

<br />

## Leaks, Allocations, memory graph

-   Leaks로 릭이 있는지를 파악하고 Alloctiontions, memory graph로 어디서 나는지 확인한다.
-   앱을 쓸 수록 사용량이 올라갈때, 특정 화면에 들어갔다 나와도 메모리가 줄어들지 않을 때

<br />

## 네트워크

-   API 응답이 늦거나 데이터 사용량이 비정상적일 때 사용
-   요청이 느릴때 (Latency) - 앱보다 외부적인(서버, 네트워크 상태) 요인일 가능성이 높음
-   데이터 사용량이 많을 때 - 원본 이미지 수신, 불필요한 데이터 수신, 캐싱 동작 오류
-   데이터 오류 - 404, 500등 에러가 발생할 때 


<br />

---

# Crash


<br />

---

## dSYM(debugSymbol)

-   크래시 리포트에 함수 이름, 줄 번호등 개발자가 읽을 수 있는 콜스택을 적어주는것
-   빌드설정에서 Debug Information Format을 DWARF with dSYM File로 세팅
-   앱 분석 공유에 동의한 App Store 사용자는 xcode에서 분석가능 (but firebase crashlytics를 주로 사용)


## 메모리 접근 오류

-   크래시 유형은 EXC_BAD_ACCESS (SIGSEGV)
-   nil 포인터, 해제된 메모리, 접근권한 없는 주소에 접근하려고 할 때 발생
-   진단도구 : ASan, Zombie Object

## 런타임 및 언어 오류

-   Swift 런타임 오류, 대부분 !를 사용할 때
-   처리되지 않는 ObjC 오류


## 크래시 종류

-   Exception Type
    -   EXC_BAD_ACCESS (SIGSEGV): 가장 흔한 크래시. nil 포인터 접근, 해제된 메모리 접근 등 잘못된 메모리 주소에 접근했다는 뜻
    -   EXC_CRASH (SIGABRT): "의도된" 크래시. Swift의 fatalError()나 처리되지 않은 Objective-C 예외(NSException)
    -   EXC_BREAKPOINT (SIGTRAP): Swift 런타임이 감지한 오류, 잘못된 ! 사용시
    -   EXC_RESOURCE: 메모리(OOM)나 CPU 등 리소스 한계를 초과하여 OS가 앱을 종료
-   Termination Reason
    - Namespace SPRINGBOARD, Code 0x8badf00d(Ate Bad Food) : 앱 실행(Launch) 시간이 너무 오래 걸림
    - Namespace SPRINGBOARD, Code 0xdead10cc(Dead Lock) : 앱이 백그라운드 작업을 제시간에 완료하지 않는 등 교착 상태에 빠짐
    - Namespace DYLD, Code 0x1(Missing Framework) : dyld가 라이브러리를 로드하지 못함