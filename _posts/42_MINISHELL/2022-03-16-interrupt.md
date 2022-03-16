---
title: Signal 함수와 인터럽트
categories: 
  - 42_MiniShell
excerpt: "signal 함수와 인터럽트에 대해 알아보자:)"
date:   2022-03-16
tags:
- 42seoul
- MiniShell
---

# 개요


쉘에서 어떤 프로그램을 실행중 일 때 ctrl-C를 이용하여 프로그램을 종료한다.

그 원리와 방법에 대해 알아보겠다.


<br />
<br />

---

# signal

---

* `함수 원형` : void (*signal(int sig, void (*func)(int)))(int);
* `함수 라이브러리` : #include <signal.h>
* `int sig` : signal flag
* `void (*func)(int))` : signal 감지시 실행할 함수

<br />

---

## signal 종류

---

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/158511529-7aa13ae2-2486-42f4-b039-77535ab18ea8.png">
		<img src="https://user-images.githubusercontent.com/79088896/158511529-7aa13ae2-2486-42f4-b039-77535ab18ea8.png"  width="800px;">
	</a>
</figure>


<br />
<br />

<br />

---

## signal 설명

---

SYSIFCOPT(*ASYNCSIGNAL)옵션으로 컴파일하면 비동기 신호를 사용하며 기본적으로 signal 함수는 동기 신호를 감지한다.

신호가 감지되면 두번째 파라메터인 함수를 실행하고 그 함수의 인자로 첫번째 인자값을 넣어준다.

<br />

---

## 신호 무시

---

signal(SIGINT, 

<br />
<br />

---

# ctrl-C

---

신호의 종류를 보다보면 두번째에 **SIGINT**가 있다. 이 신호의 설명에는 interrupt program이라고 적혀있는데, 키보드의 의한 인터럽트 신호를 감지하는 것이다. 

키보드의 의한 인터럽트 신호는 ctrl-C이다.

## 활용한 예시

```c
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
 
void sigHandler(int sig){
    exit(0);
}

int main(){
    signal(SIGINT, sigHandler);
    while(1);
}
```



<br />
<br />

---

# ctrl-C, ctrl-D and ctrl-\

---

ctrl-C는 위에서 말한 것처럼 현재의 프로세스에 SIGINT 신호를 보내는 것을 의미하고,

ctrl-D는 표준 입력에 EOF를 의미한다. 그러므로 입력창에 입력을 하면 터미널이 종료가 된다.

ctrl-\는 현재의 프로세스에 SIGQUIT 신호를 보낸다. 그러면 프로그램이 종료된다.

