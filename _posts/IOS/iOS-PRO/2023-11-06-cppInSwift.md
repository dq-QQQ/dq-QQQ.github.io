---
title: 스위프트에서 C++ 사용하기
categories:
  - iOS-PRO
excerpt: "스위프트에서 C++을 사용해보자:)"
date: 2023-11-06
tags:
- iOS
- swift
---

# 개요

Objective-c로 된 코드에 C++을 사용할 수 있던데 스위프트에서도 가능한지 알아보자

<br />
<br />

---

# 옵젝시에서 C++ 사용하기

---

1. cpp파일에 클래스를 만든다.
2. objective-c파일의 확장자를 mm으로 바꾼다.
3. cpp 파일의 헤더 hpp를 import 시키고 사용한다.

---

## ho.hpp

---

```cpp
#ifndef ho_hpp
#define ho_hpp

#include <stdio.h>
#include <iostream>

class Ho {
private:
    int ho;
    std::string str;
public:
    Ho();
    Ho(int a, std::string b);
    ~Ho();
    
    void printHo();
    
    void setHo(int tmp);
    int getHo();
    
    void setStr(std::string s);
    std::string getStr();
};

#endif /* ho_hpp */
```

<br />
<br />

---

## ho.cpp

---

```cpp
#include "ho.hpp"

Ho::Ho() { ho = 0; str = ""; }
Ho::Ho(int a, std::string b) { ho = a; str = b;}
Ho::~Ho() {}

void Ho::printHo() {
    std::cout << "int : " << ho << std::endl << "str : " << str << std::endl;
}

void Ho::setHo(int tmp){
    ho = tmp;
}

int Ho::getHo() {
    return ho;
}

void Ho::setStr(std::string s) {
    str = s;
}

std::string Ho::getStr() {
    return str;
}

```

<br />
<br />

---

## main.mm

---

```objective-c
#import <Foundation/Foundation.h>
#import "ho.hpp"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // insert code here...
        Ho ho;
        
        ho.printHo();
        std::cout << std::endl;
        
        ho.setHo(1);
        ho.setStr("hoho");
        ho.printHo();
        std::cout << std::endl;
        
        Ho ho2(10, "helloooo");
        ho2.printHo();
        std::cout << std::endl;
    }
    return 0;
}

// Result
//
// int : 0
// str : 
//
// int : 1
// str : hoho
//
// int : 10
// str : helloooo
//
// Program ended with exit code: 0
```


<br />
<br />

---

# 스위프트에서 C++ 사용하기

---

스위프트에서는 C++을 직접 지원하지 않는다. 따라서


1. 위에서 만든 cpp 클래스를 똑같이 만든다.
2. 그럼 아래와 같은 안내문이 뜨는데 Create를 누른다.

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/6d04bc7e-6b31-4784-9936-5e3fd9d3cf23">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/6d04bc7e-6b31-4784-9936-5e3fd9d3cf23" class="w8" />
	</a>
</figure>

<br />
<br />

3.

