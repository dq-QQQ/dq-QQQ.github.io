---
title: SwiftUI TextField
categories:
  - SWIFTUI 
excerpt: "SwiftUI에서 TextField를 공부해보자:)"
date: 2022-08-04
tags:
- SwiftUI
---

# 개요

텍스트를 입력하는 창을 만드는 텍스트필드를 공부해보자

<br />
<br />

---

# TextField

---

텍스트필드는 사용자가 직접 텍스트를 수정할 수 있는 인터페이스를 제공하는 컨트롤.

`struct TextField<Label> where Label : View`

`TextField(텍스트 입력전 투명문자열, text: 입력되는 문자열)`를 사용한다.

텍스트 스타일은 2가지가 있다.

* PlainTextFieldStyle()
* RoundedBorderTextFieldStyle()

첫번째거는 그냥 기본값이고, 두번째거는 테두리에 둥근 사각형이 있다.

<br />
<br />

---

# 이미지 조합

---

```swift
HStack {
            Image(systemName: "envelope").frame(width: 30)
            TextField("이메일", text: $email)
                .textFieldStyle(RoundedBorderTextFieldStyle())
        }
        
        HStack {
            Image(systemName: "envelope").frame(width: 30)
            TextField("이메일", text: $email)
        }
        .padding()
        .background(RoundedRectangle(cornerRadius: 5)
            .stroke(Color.gray.opacity(0.6), lineWidth: 1))
```


<br />

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/182867244-c6d024ba-8544-4a0a-9b3a-3be858ce8404.png">
		<img src="https://user-images.githubusercontent.com/79088896/182867244-c6d024ba-8544-4a0a-9b3a-3be858ce8404.png" class="w8" />
	</a>
</figure>

<br />

<br />
<br />

---

# formatter

---

매개변수로 formatter: 다음거

* nameFormatter
* dateFormatter
* numberFormatter

<br />
<br />

---

# SecureField

---

비밀번호칠 때처럼 검정색으로 땡땡땡

`SecureField(Label, text: Value)`

