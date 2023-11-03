---
title: 웹 프로그래밍과 JSP
categories: 
  - CS
excerpt: "웹 프로그래밍과 JSP의 기초에 대해서 공부해보자:)"
date: 2022-04-18
tags:
- webserver
---

# 개요

웹 프로그래밍의 기반이 되는 인터넷의 기술적 배경을 이해하고 관련 기술에 대해서 알아보겠다.

<br />
<br />

---

# 인터넷

---

인터넷 자체는 네트워크 인프라라고 할 수 있다.

www나 Email은 인터넷 기반의 서비스이다. 

이러한 서비스들은 TCP/IP의 4계층 중에서 응용계층에 속한다.

네트워크에서 서비스를 제공하는 컴퓨터를 서버라고 하고, 서비스를 이용하는 컴퓨터를 클라이언트라고 한다.

웹 서비스를 제공하는 소프트웨어가 있어야 웹서버의 역할을 할 수 있는데 아파치가 대표적이다.

그리고 클라이언트에서 사용할 수 있는 소프트웨어는 흔히 말하는 웹 브라우저, 크롬 사파리 같은 것을 말한다.

<br />

---

## 웹 서비스의 동작 과정

---

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/164393288-343523a8-756c-4111-ad30-6ae66895df9e.jpeg">
		<img src="https://user-images.githubusercontent.com/79088896/164393288-343523a8-756c-4111-ad30-6ae66895df9e.jpeg" class="w8" />
	</a>
</figure>

<br />
<br />

---

# JSP

---

JSP는 Java Server Page의 약자로 서블릿이라고 하는 자바로 구현된 웹 프로그래밍 기술에 기반한다.

JSP는 자바의 모든 기능을 이용할 수 있으며 함 께 스크립트를 사용할 수도 있다.

JSP는 기본적으로 서블릿으로 변경되어 실행되며, 메모리상에 적재된 서블릿을 스레드로 실행함으로써 시스템 자원을 효율적으로 실행할 수 있다.

스프링 프레임워크와 결합하여 가장 많이 사용하는 웹 서버 기술이다.

<br />
<br />

---

# 서블릿

---

서블릿은 자바를 이용한 서버 프로그래밍 기술로 자바를 웹 환경에서 사용할 수 있는 기술이다.

JSP와 서블릿은 대체 기술이라기보다 상호보완적인 기술이다.

서블릿은 컨테이너라고 불리는 서버 소프트웨어에 의해 동작한다.


<br />

---

## 서블릿 실행 과정

---

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/164401089-115fa903-7f54-4a95-8ceb-4955dd4f65fb.jpeg">
		<img src="https://user-images.githubusercontent.com/79088896/164401089-115fa903-7f54-4a95-8ceb-4955dd4f65fb.jpeg" class="w8" />
	</a>
</figure>

<br />

---

## 서블릿 동작 과정

---

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/164401248-3e97a762-8ebd-4492-a739-9cf0d9e12266.jpeg">
		<img src="https://user-images.githubusercontent.com/79088896/164401248-3e97a762-8ebd-4492-a739-9cf0d9e12266.jpeg" class="w8" />
	</a>
</figure>

<br />
<br />

---

# JSP와 서블릿의 관계

---

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/164409985-1a72554f-fbbf-44b9-924d-b0db8d5ff106.jpeg">
		<img src="https://user-images.githubusercontent.com/79088896/164409985-1a72554f-fbbf-44b9-924d-b0db8d5ff106.jpeg" class="w8" />
	</a>
</figure>

