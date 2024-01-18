---
title: iOS의 Asynchronous Programming
categories: 
  - iOS
excerpt: "iOS에서 비동기 프로그래밍을 어떻게  알아보자:)"
date:   2022-09-24
tags:
- iOS-PRO
- Concurrency
---

# 개요

SwiftUI를 하다가 async/await이 궁금해서 파고파다 여기까지 왔다.

[애플 공식문서](https://github.com/apple/swift-evolution/blob/main/proposals/0296-async-await.md)

병렬프로그래밍과 async/await을 이용한 방법, GCD를 이용한 방법, NSThread를 이용한 방법, callback함수를 이용한 방법을 알아보겠다.

그렇다면 스레드를 알아야한다. 알아보자.


<br />
<br />

---

# 멀티스레드

---

스레드란 프로세스안 작업의 흐름 단위라고 할 수 있다.

프로그램을 실행하면 여러개의 스레드를 생성해서 병렬로 동작시킬 수 있다. 이를 멀티스레딩이라고 부른다.

스레드를 생성한 쪽을 부모 스레드 만들어진 스레드는 자식 스레드라고 부르는 데 자식이 끝날 때까지 기다리지 않고 다음 작업을 하는 것을 detach 되었다고 한다.

iOS 에서 멀티스레딩이라 하여 GCD, NSThread를 이용해서 멀티스레딩을 하는 것은 기본적으로 detach 상태이다.

생성된 스레드는 스택을 제외한 프로세스의 메모리 공간을 공유한다. 따라서 하나의 메모리 공간에 여러개의 스레드가 접근하게 되면 변수값이 맞다는 것을 보장할 수가 없게 된다.

이럴 때는 lock, semaphore등의 상호 배제를 통해 접근을 통제해야한다. 그렇게 된다면 결과를 보장한다는 뜻의 Thread-safe하다고 부른다.


<br />
<br />

---

# Concurrency Programming

---

네트워크로 연결된 모든 시스템은 동시성 프로그래밍이 적용되었다고 과언이 아니다. 나도 SwiftUI하다가 Firebase에서 데이터를 땡겨올 때 적용하기에 궁금했었다.

나는 비동기가 궁금하지만 비동기 프로그래밍을 알기 위해서 간단하게 동시성 프로그래밍이 뭔지 알아보겠다.

동시성, 병렬성. 비슷한 의미로 통용되는 듯 하다. 이에 대해 알아보겠다.

동시성은 2개 이상의 프로세스가 동시에 계산을 진행하는 상태를 나타내는 것이다.

병렬성은 같은 시각에서 여러 프로세스가 동시에 계산을 실행하는 상태를 의미한다. 즉 여러 프로세스가 동시에 실행 중일 때 이를 병렬로 작동하고 있다고 한다.

병렬성은 task 병렬성, data 병렬성, instruction Level 병렬성으로 나뉜다.

주로 말하는 것은 task이며 data는 데이터를 쪼개서 여러개로 처리하는 것이다.

instruction Level은 Cpu의 명령어 레벨에서 병렬화를 하는 것이다. 굉장히 로우레벨에서 처리하는 것으로 우리는 건드릴 경우는 거의 없다.

아래는 그림으로 표현한것이다. 근데 보면 혼용해서 자주 쓰는 듯하다. 

<br />

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/186420456-20827db3-9afb-4375-bfd1-7200a550791b.jpg">
		<img src="https://user-images.githubusercontent.com/79088896/186420456-20827db3-9afb-4375-bfd1-7200a550791b.jpg" class="w8" />
	</a>
</figure>

<br />

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/186420461-016dc2c4-4176-44b3-a3ff-0d637627f451.jpg">
		<img src="https://user-images.githubusercontent.com/79088896/186420461-016dc2c4-4176-44b3-a3ff-0d637627f451.jpg" class="w8" />
	</a>
</figure>

<br />

동시성이 필요한 이유는 효율적인 계산 리소스 활용, 공정성, 편리성등의 이유가 있다. 

동시처리가 가능하면 IO대기 상태중에 다른일을 할 수 있기 때문에 계산 리소스를 효율적으로 이용할 수 있다.

병렬처리는 단순히 성능 향상을 위해 필요하다.

<br />
<br />

---

# Asynchronous Programming

---

내가 글을 읽고 있을 때 카톡이 오거나 급한일이 생기면 그 상황에 대응할 것이다. 

컴퓨터에서는 카톡이 오거나 급한일을 이벤트 혹은 인터럽트라고 부른다. 
비동기 프로그래밍은 독립해서 발생하는 이벤트에 대한 처리를 기술하기 위한 동시성 프로그래밍 기법을 총칭한다.

처리순서는 코드의 순서가 아닌 이벤트 발생 순서에 의존한다.

비동기 프로그래밍 방법은 Future, async/await이 있다.

<br />

---

## 동기 <-> 비동기 / 직렬 <-> 병렬

---

특정 스레드에서 특정 작업을 다른 스레드로 보낸 후 끝날 때까지 기다리지 않고 다음 작업을 바로 실행하는 것을 비동기라고 한다.

특정 스레드에서 특정 작업을 다른 스레드로 보낸 후 끝날 때까지 기다리고 다음 작업을 실행하는 것을 동기라고 한다.

동기 <-> 비동기 개념은 작업이 끝날 때까지 기다릴지 말지에 대한 개념이고 직렬 <-> 병렬 개념은 큐로 보낸 작업들이 하나의 스레드 or 여러개의 스레드로 가냐이다.

<br />
<br />

---

# NSThread

---


Foundation 프레임워크에는 스레드를 관리하는 NSThread 클래스가 있다. 이 클래스에서 제공하는 메소드는 다음과같다.

-   \+ (NSThread \*) currentThread : 현재 스레드의 인스턴스
-   \+ (NSThread \*) mainThread : 앱의 메인스레드
-   \+ (NSMutableDictionary \*) threadDictionary : 현재 실행중인 스레드의 딕셔너리
-   \+ (void) sleepForTimeInterval: (NSTimeInterval) time : time 만큼 스레드 중단
-   \+ (void) sleepUntilDate: (NSDate \*) aDate : aDate까지 스레드 중단

---

## Lock

위의 그림처럼 동시에 실행하는 부분을 critical section이라고 부르며 이를 상호 배제 하기 위해 semaphore, mutex를 이용한다.

iOS에서는 이것을 Lock이라고 부르며 NSLock 클래스를 이용해 제어한다.

Lock은 일반 인스턴스처럼 클래스 메서드 alloc, init을 이용해 생성할 수 있으며 멀티스레딩 되기 전에 생성되어야한다.

NSLock은 POSIX 스레드 기능을 이용하기 때문에 lock과 unlock은 같은 스레드에서 진행되어야한다.

```
NSLock *ho = [[NSLock alloc] init];

(void) addNumber: (NSInteger)n
{
    [ho lock];
    num = 5;
    [ho unlock];
}
```

---

## deadlock

lock을 사용할 때는 조심해서 사용해야한다.

잘못쓰면 여러 스레드가 서로의 실행을 기다리면서 무한히 진행하지 못하는 데드락이 생길수있다.

iOS에서는 어떤 락을 여러 스레드가 실행하지 않도록 지정하지 못하게 하는 @synchronized 키워드가 있다.

```
@synchronized (sharedObject) {
    // 공유 자원에 대한 작업 수행
}
```

이렇게 하면 runtime이 코드 블록을 독점적으로 수행하는 mutex를 생성한다.

그러나 단일 락이기 때문에 성능상의 이슈가 있을 수 있으며 objective-c에서 주로 쓰던 동기화 매커니즘이고 요즘은 GCD를 이용한다.

---

## NSOperation

operation 객체는 실행해야할 코드와 관련된 데이터를 모아서 캡슐화한 것이라고  할 수 있다.


<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/e30a9571-8c74-43dc-bd18-f4b856c848da">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/e30a9571-8c74-43dc-bd18-f4b856c848da" class="w8" />
	</a>
</figure>

<br />


operation은 대기열에 들어간 순서대로 실행되며 우선도를 설정해 우선순위를 정할 수 있다.

그 대기열을 NSOperationQueue 클래스에서 제공하며 FIFO 형태의 오퍼레이션 큐를 제공한다.

그러나 이 방법은 옵젝시에서 많이 사용한 방법이고 Swift와 SwiftUI에서는 GCD를 많이 이용하므로 이런게 있다정도만 알고 넘어간다.

---

## callback 함수

#### block?

콜백함수란 비동기 작업을 할 때 실행될 코드를 함수의 인자로 전달하여 처리하는 함수를 의미한다.

옵젝시에서는 block이라는 개념을 사용하여 구현하는데 Swift의 클로저랑 같은 개념이다. 회사 제품 코드를 보면 상당히 많이 쓴다.

블록 객체는 변수에 대입하거나 함수의 매개변수로 넘겨서 사용하는데 함수포인터의 개념과 유사하다. \* 대신 ^를 쓰는것만 다른정도?

```
- (void)performTaskWithCallback:(void (^)(NSString *error))callback {
    NSString *result = @"Task is completed";
    callback(result);
}

[self performTaskWithCallback:^(NSString *result) {
    NSLog(@"Callback result: %@", result);
}];
```

위의 예시를 보면 블록 객체 부분 가독성이 떨어진다. 따라서 typedef를 사용해서 헤더에 정의하는 방법을 주로 사용한다.

```
typedef void (^MyCallbackBlock)(NSString *result);

- (void)performTaskWithCallback:(MyCallbackBlock)callback {
    NSString *result = @"Task is completed";
    callback(result);
}

[self performTaskWithCallback:^(NSString *result) {
    NSLog(@"Callback result: %@", result);
}];
```

이렇게 하는 것이 좀 더 가독성이 좋다 :)

블록 객체는 블록이 작성된 위치에서 변수를 캡쳐해놓는다. 따라서 복사된 값을 읽는 것만 가능하고 바꾸는 것은 불가능하다.

블록 객체안에서 외부 값을 변경하는 작업을 수행할 수 있는 것은 전역변수, static 변수이다. 이 값은 블록 안에서 바로 반영할 수 있다.

그러나 캡쳐 개념이기 때문에 외부에서 지역변수가 변경되어도 블록 객체 안에서는 캡쳐한 시점의 값을 가지고 있다. 또한 변경을 시도하면 컴파일 에러가 난다.

그러나 이 지역변수에 \_\_block 키워드를 붙이면 블록객체에서 읽고 쓸 수 있는 변수로 사용할 수 있다.

#### ARC와 블록객체

스택에 있는 블록 객체를 메소드가 끝난 후에도 계속 사용하려면 블록 객체를 복사해둬야한다.

강한 참조 변수에 대입될 때와 return으로 반환될 때 ARC에서는 컴파일러가 자동으로 copy 작업 코드를 넣는다.

따라서 명시적으로 객체를 복사하지 않아도 사용할 수 있게 되지만 메소드의 인수로 전달된 블록객체는 자동으로 복사되지 않는다.

따라서 copy 옵션을 부여한 프로퍼티를 선언해야한다.

#### 콜백 실행 순서

```
//명시적으로 메인큐에서 실행하라고 안해도 기본적으로는 메인스레드에서 실행됨
dispatch_async(dispatch_get_main_queue(), ^(){ 
    run 메서드 {
        로그(run 시작);
        ...
        open(... handler: ^ {
            로그(open handler 시작);
        }
    }
}

open 메서드 {
    로그(open 시작);
    ...
    fetch(... handler: ^ {
        로그(fetch handler 시작);
    }
}

fetch 메서드 {
    로그(fetch 시작);
}
```


<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/3606c985-0d0c-4ac3-b40a-93dd9a38c108">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/3606c985-0d0c-4ac3-b40a-93dd9a38c108" class="w8" />
	</a>
</figure>

<br />


위의 코드에서 백그라운드 스레드에서 실행되도록 코드를 수정하면 코드 실행순서와 메인스레드 여부는 다음과 같다.


<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/d0a215c2-dd32-49ba-9bc5-3642ab5be7fa">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/d0a215c2-dd32-49ba-9bc5-3642ab5be7fa" class="w8" />
	</a>
</figure>

<br />


이 결과에서 알 수 있는 점은 다음과 같다. 하루종일 테스트 해봤으니 99.999% 맞을듯

-   콜백함수는 따로 설정하지 않는 이상 메인스레드에서 실행된다.
-   콜백함수가 아닌 일반적인 함수는 부른 스레드를 따라간다. 
-   그리고 기본적으로 콜백함수는 추가적인 스레드를 생성하여 멀티스레딩을 하지않는다.
-   비동기 프로그래밍은 동시에 뭔가를 파바바박 하는게 아니라 스레드가 달라도 코드를 순차적으로 시작하는 것을 보장한다.
-   멀티스레딩으로 처리를 한다면 해당 구문을 보내놓고 다음 코드를 실행한다.

어렵네...근데 뭔가 감은 오는 것 같다.




<br />

---

## Future과 async/await

---

Future은 미래의 언젠가의 시점에서 값이 결정되는 것을 나타내는 데이터 타입이다.

Future은 코루틴을 이용해 구현되며 이로 인해 중단 재개가 가능한 함수에서 미래에 결정되는 값을 표현한 것으로 의미가 바뀐다.

코루틴이란 함수를 임의의 시점에 중단하고 중단한 위치에서 함수를 다시 재개하는 것을 말한다.

Future 타입을 이용한 기술 방법에는 명시적 기술과 암묵적 기술이 있다. 여기서 명시적 기술이 async/await인 것이다.

await은 Future 타입의 값이 결정될 때까지 처리를 정지하고 다른 함수에 Cpu 리소스를 양보하기 위해서 이용하며,

async는 Future 타입을 포함한 처리를 기술하기 위해 이용한다.

비동기 프로그래밍은 콜백을 이용해서도 기술된다 그러나 이는 가독성이 매우 낮다. 그렇기에 Swift에서는 async/await을 지원한다.

개념적인 부분은 이정도이고 실제로 iOS에서는 어떻게 작동하는지 알아보자


<br />
<br />

---

# GCD

---

`Grand Central DispatchQueue` 이건 나중에.
