---
title: JSP 내장객체
categories: 
  - CS
excerpt: "JSP 내장객체에 대해서 공부해보자:)"
date: 2022-04-20
tags:
- webserver
---

# 개요

JSP의 내장 객체를 알아보겠다.


<br />
<br />

---

# 내장객체

---

JSP 내에서 선언하지 않고 사용하는 객체이다.

서블릿 형태로 변환된 코드 내에 포함되어 있는 멤버변수, 메서드등의 객체로 생각하면 된다.


<br />
<br />

---

# request

---

사용자 요청과 관련된 기능을 제공하는 내장객체이다.

주로 클라이언트에서 서버로 전달되는 정보를 처리하려고 사용한다.

가장 대표적인 유형이 HTML을 통해 입력된 값을 JSP에서 가져올 때 사용하는 것이다.

<br />

---

## request 주요 메서드

---

| 메서드 | 설명 |
| --- | --- |
| getParameterNames() | 현재 요청에 포함된 매개 변수의 이름을 열거 형태로 넘김 |
| getParameter(name) | 문자열 name과 이름이 같은 매개변수의 값을 가져옴 |
| getParameterValues(name) | 문자열 name과 이름이 같은 매개변수의 값을 배열 형태로 가져옴 |
| getCookies() | 모든 쿠키 값을 javax.servlet.http.Cookie의 배열 형태로 가져옴 |
| getMethod() | 현재 요청이 GET이나 POST 형태로 가져옴 |
| getSession() | 현재 세션 객체를 가져옴 |
| getRemoteAddr() | 클라이언트의 IP 주소를 알려줌 |
| getProtocol() | 현재 서버의 프로토콜을 문자열 형태로 알려줌 |
| setCharacterEncoding() | JSP로 전달되는 내용을 지정한 캐릭터셋으로 변환 |

<br />
<br />

---

# response

---

request와 반대되는 개념으로 사용자 응답과 관련된 기능을 제공하는 내장객체이다.

<br />

---

## response 주요 메서드

---


| 메서드 | 설명 |
| --- | --- |
| setContentType(type) | type으로 설정 |
| setHeader(name, value) | 문자열 name의 이름으로 문자열 value의 값을 헤더로 설정 |
| setDateHeader(name, date) | name으로 시간을 헤더에 설정 |
| sendError(status, msg) | 오류 코드를 세팅하고 메시지를 보냄 |
| sendRedirect(url) | 클라이언트 요청을 다른 페이지로 보냄 |

<br />
<br />

---

# out

---

출력 스트림으로 사용자 웹 브라우저로 출력하기 위한 채널이다.

브라우저에 텍스트를 출력하는 데 사용한다.

<br />

---

## out 주요 메서드

---

| 메서드 | 설명 |
| --- | --- |
| getBufferSize() | output buffer의 크기를 바이트로 알려줌 | 
| getRemaining() | 남아 있는 버퍼의 크기 중 사용 가능한 비율을 알려줌 |
| clearBuffer() | 버퍼에 있는 콘텐츠를 모두 지움 |
| flush() | 버퍼를 비우고 output stream도 비움 |
| close() | output stream을 닫고 버퍼를 비움 |
| println(content) | content의 내용을 newline과 함께 출력 |
| print(content) | content의 내용을 출력 |

<br />
<br />

---

# session

---

HTTP 프로토콜은 비연결형 프로토콜이기 때문에 한 페이지가 출력된 다음에는 연결이 끊어진다. 

따라서 로그인 같은 기능의 처리가 힘들다. 이러한 문제점을 해결하기 위한 것이 쿠키와 세션이다.

쿠키는 사용자와 관련된 정보를 PC에 보관하는 방식이고, 세션은 서버에 보관하는 방식이다.

세션이 보안 문제에 유리하고 제약사항이 적은 편이기 때문에 최근에는 대부분 세션을 이용한다.

세션이 최초로 설정되는 것은 웹에 최초로 접속이 이루어졌을 때다.

<br />

---

## session 주요 메서드

---


| 메서드 | 설명 |
| --- | --- |
| getID() | 각 접속에 대한 세션 고유의 ID를 문자열 형태로 반환 |
| getCreatingTime() | 세션 생성 시간을 1970/1/1로부터 밀리세컨드 값으로 반환 |
| getLastAccessedTime() | 현재 세션으로 마지막 작업한 시간을 밀리세컨드 값으로 반환 | 
| getMaxInactiveInterval() | 세션 유지 시간을 초로 반환 |
| invalidate() | 세션 종료 |

<br />
<br />

---

# MVC와 JSP 내장객체

---

MVC 패턴에 따르면 JSP는 뷰의 역할만 수행해야 한다.

컨트롤러에서 처리한 데이터를 JSP로 가져와야하는데 이때 필요한 것이 내장객체이다.
