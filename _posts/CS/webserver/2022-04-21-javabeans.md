---
title: JSP와 자바 빈즈
categories: 
  - CS
excerpt: "JSP 빈즈에 대해서 공부해보자:)"
date: 2022-04-21
tags:
- webserver
---

# 개요

JSP 빈즈의 구조를 이해하고 useBean 액션 활용 방법을 알아보겠다.

<br />
<br />

---

# 빈즈

---

빈즈는 특정한 일을 독립적으로 수행하는 컴포넌트를 의미한다.

원래 자바에서는 GUI를 제작하기 위해서 빈즈를 만들었다. 그러다가 JSP 빈즈와 자바 빈즈로 나뉘어 개념이 확장되었다.


<br />

---

## 자바 빈즈

---

자바 빈즈는 서로 다른 회사에서 GUI용 컴포넌트를 만들고, 이들을 조합해서 프로그램을 개발할 수 있도록 하는 것이 초기 목적이었다.

최근에는 GUI 프로그램에서 빈즈라는 표현보다 JSP 빈즈를 더 많이 사용한다.

<br />

---

## JSP 빈즈

---

JSP 빈즈는 JSP와 연동하려고 만들어진 컴포넌트 클래스를 말한다.

JSP 빈즈는 컨테이너에 위치하며, JSP에 데이터베이스 연동 등 프로그램적 요소를 모듈화할 수 있도록 도와준다.

가능하면 Scriptlet을 사용하는 것보다 빈즈를 만들어 사용하는 것이 좋다.

빈즈를 가장 많이 이용하는 경우는 HTML 폼을 처리하고 데이터베이스와 연동할 때다.

빈즈 클래스를 개별 JSP에서 사용하기보다는 컨트롤러에서 사용하고 뷰에 필요한 객체들을 만들어 공급하는 형태로 구현한다.

<br />
<br />

---

# 빈즈와 JSP 연동

---

JSP 빈즈는 JSP에서 사용할 수 잇는 자바 컴포넌트로, useBean액션과 결합해서 웹프로그램을 더욱 간편하고 단순한 구조로 처리할 수 있다.

<br />
<br />

---

# 빈즈 클래스 구조

---

```java
class xxxBean {
  // 멤버변수 : DB 테이블의 칼럼 이름과 매칭된다.
  private String xxx;
  
  // get, set 메서드 : 멤버변수와 매칭된다.
  public String getXxx() {
    return xxx;
  }
  public setXxx(String xxx) {
    this.xxx = xxx;
  }
}
```

<br />
<br />

---

# JSP에서 빈즈 선언

---

`<jsp:useBean id="mybean" scope="request" class="MyBean" />`와 같은 형태로 사용한다.

| 속성 | 설명 |
| --- | --- |
| id | 빈즈 클래스의 인스턴스 이름으로 사용할 변수 |
| class | 빈즈 클래스의 클래스 이름 | 
| scope | 빈트 클래스의 범위로 내장객체를 넣는다 |

<br />
<br />

---

# JSP에서 빈즈 속성 설정

---

`<jsp:setProperty name="mybean" property="userid" />`
`<jsp:setProperty name="mybean" property="userpasswd" />`

| 속성 | 설명 |
| --- | --- |
| name | 빈즈 클래스의 인스턴스 이름 |
| property | 속성 값으로 빈즈 클래스의 setXxx메서드와 매칭될 속성값 |

대부분의 경우 property 값으로는 *를 사용한다.

```java
mybean.setUserid(request.getParameter("username"));
mybean.setPasswd(request.getParameter("userpasswd"));
```
위의 두 코드는 같은 기능을 수행하는 코드이다.

