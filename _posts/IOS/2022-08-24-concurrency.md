---
title: async/await
categories: 
  - OS
excerpt: "비동기 프로그래밍을 알아보자:)"
date:   2022-08-24
tags:
- iOS
- Concurrency
---

# 개요

SwiftUI를 하다가 async/await이 궁금해서 파고파다 여기까지 왔다.




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

## Future 

---

Future은 미래의 언젠가의 시점에서 값이 결정되는 것을 나타내는 데이터 타입이다.

Fu
