---
title: SwiftUI 커스텀 폰트
categories:
  - SWIFTUI 
excerpt: "SwiftUI에서 커스텀 폰트를 사용해보자:)"
date: 2022-08-18
tags:
- SwiftUI
---



# 개요

커스텀 폰트를 사용하려는데 어떻게하는지 알아보겠다.


<br />
<br />

---

# 적용방법

---

* workSpace에 otf, ttf 폰트 파일 넣는다.
* pList가서 fonts provided by application에 폰트 이름만 넣는다.
* 안된다면 띄어쓰기 다 없애본다
* 그래도 안된다면 아래 코드를 프로그램에 넣어서 폰트 리스트들을 다 출력하고 해당 이름을 넣는다.

```swift
for family: String in UIFont.familyNames {
    print(family)
    for names : String in UIFont.fontNames(forFamilyName: family){
        print("=== \(names)")
    }
}
```