---
title: 옵젝시 Foundation
categories:
  - Objective-C
excerpt: "옵젝시 Foundation 공부해보자:)"
date: 2023-11-17
tags:
- iOS
- Objective-C
---

# 개요


Foundation 프레임워크는 문자열, 배열, 딕셔너리, 숫자 오브젝트등 기본적인 객체들에 대한 클래스를 제공한다.

대표적으로 사용하는 NSString과 NSArray를 알아보겠다.



<br />
<br />

---

# Immutable, Mutable 클래스

---

Foundation클래스는 immutable과 mutable로 구분되는데 기본적인 클래스는 immutable이다.

immutable은 클래스의 인스턴스를 만든 이후에는 내용을 수정할 수 없다.

대표적으로 NSString = immutable / NSMutableString = mutable이다.

이러한 구분은 왜있는걸까? NSString도 값을 나중에 바꿀 수 있는데...??? 포인터값을 바꾸는건가..??

첫째로 구현의 용이성 때문이다.

예를들어 문자열이 변경되지 않는다고 정해두면 변경에 필요한 메소드나 자료구조를 준비하지 않아도 된다.

변수 선언할 때 var, let 느낌인듯하다.

두번째로 객체 취급에 대한 개념때문이다.

[a add:b]의 코드는 어떻게 해석해야하는가? 객체를 속성이 변하지 않는 '값을 나타내는 실체'라고 간주하는지

속성이 변하는 '담는 그릇'이라고 간주하는 지에 따라 다르다. 

예를 들어 a,b가 집합이라면 a의 값은 변하지 않고 a U b를 리턴하면 변경 불가능 객체

a가 변하여 b가 합쳐진 a가 리턴되면 변경 가능 객체이다.

변경 불가능 객체를 잘 활용해야하는데 동시성 프로그래밍에서 중요하다. 변경 가능 객체는 어느 틈에 다른 스레드에서 값을 변경할지 모른다.


<br />
<br />

---

# 클래스 클러스터

---

NSString, NSArray, NSDictionary, NSSet, NSNumber, NSData클래스는 클래스 클래스터로 구현되어있다.

클래스 클러스터는 단순한 인터페이스를 통해 복잡한 부분을 숨기는 역할을 한다.

클래스 클러스터를 볼 때 밖으로 보이는 부분은 추상 클래스로, 실제 클래스 내용은 숨겨져있다.

내부의 서브 클래스는 인터페이스를 모두 구현한다.

iOS 개발을 할 때 내부적으로 타고 타고 올라가면 헤더파일에 도착하는데 그걸 클래스 클러스터라고 하나보다.


<br />
<br />

---

# NSString

---

옵젝시는 문자열을 다루기 위해 NSString을 제공한다. NSString은 크게 두가지 타입이 있는데

하나는 NSString 상수로 컴파일러가 생성하는 NSString 문자열 상수이며, 다른 하나는 NSString 오브젝트이다.

NSString 상수를 만들기 위해서는 `NSString* ho = @"ho";`의 형태로 사용한다.

이렇게 작성하면 문자열 객체의 object constant가 되어 NSString 인스턴스로 다룰 수 있다.

유니코드도 사용할 수 있는데 다양한 나라의 언어를 지원한다면 특정 언어를 사용하는것은 안된다.

NSString 객체를 만들기 위해서는 `NSString *ho = [NSString stringWithContentsOfFile: @"~~~", ~~~]`의 형태로 만든다. 이건 하나의 예시이고 다양한 방법이 있는듯

NSString은 Cocoa 환경에서 문자열을 다루는 표준 클래스이다. 문자열은 내부 문자코드로 Unicode를 사용한다.




<br />

---

## NSLog

---

`NSLog( @"hello hola %@", @"hoho");`

NSLog 포맷 스트링은 그 자체가 NSString이다.

NSLog는 %@ 구분자에 해당하는 인수에 description 메시지를 보낸다.


<br />

---

## Unicode 문자열 조작

---

문자열은 문자를 유니코드로 표현하는데 유니코드중 UTF-8은 7비트 문자 범위가 아스키 코드와 공통이다.

* `(id) initWithUTF8String: (const char *) bytes` - 편의 생성자 (stringWithUTF8String)
* `(__strong const char *) UTF8String` : 자동 해제인듯?
* `(NSUInteger) length` : 문자의 수를 리턴한다.
* `(unichar) characterAtIndex: (NSUInteger) index` : 원하는 인덱스의 문자 리턴
* `(id) initWithCharacters: (const unicahr *) characters length: (NSUInteger) length`: 문자열을 복사하여 length 수만큼 char로 초기화
* `(void) getCharacters: (unichar *)buffer range: (NSRange) aRange`: 원하는 범위의 문자를 얻는 듯

<br />

---

## 비교

---

문자열을 비교하는 메소드인데 비교 결과로 NSCompararisonResult형을 돌려준다.

NSOrderedAscending = -1L,
NSOrderedSame,
NSOrderedDescending

위처럼 3개가 있다.

* `(NSComparisonResult) compare: (NSString *) aString`: 비교한다.
* `(NSComparisonResult) caseInsensitiveCompare: (NSString *) aString`: 대소문자 구별 없이 비교
* `(BOOL) isEqualToString: (NSString *) aString` : 같은지 확인
* `(BOOL) hasPrefix: (NSString *)aString` 인수의 문자열이 리시버 앞부분과 일치하는지 확인
* `(BOOL) hasSuffix: (NSString *)aString` 인수의 문자열이 리시버 뒷부분과 일치하는지 확인

<br />

---

## 결합

---

* `(NSString *) stringByAppendingString: (NSString *)aString` : 더하기
* `(NSString *)componentsJoinedByString:(NSString *)separator;`: 구분자 더해서 더하기

<br />

---

## 부분 문자열

---

* `(NSString *) substringToIndex: (NSUInteger) anIndex` : 처음부터 인덱스까지
* `(NSString *) substringFromIndex: (NSUInteger) anIndex` : 인덱스부터 끝까지
* `(NSString *) substringWithRange: (NSRange) aRange` : 원하는 범위
* `(NSArray *) componentsSeparatedByCharactersInSet: (NSCharacterSet *) sep`: 구분자로 나누기


`NSMakeRange(0, [objcCaptionText length])`의 형태로 범위를 만들 수 있다.

<br />

---

## 검색과 치환

---

* `(NSRange) rangeOfString: (NSString *) aString` : 검색된 문자열 범위 리턴
* `(NSRange) lineRangeForRange: (NSRange) aRange` : 행 리턴
* `(NSString *) stringByReplacingCharactersInRange: (NSRange) range withString:(NSString *) replacement` : 입력한 범위를 입력한 문자열로 치환



<br />

---

### 행 끝을 나타내는 문자

---

* `\r`: 0x0d로 CR로도 복귀문자로도 불린다. 맥OS에서의 구분 문자이다. 
* '\n': 0x0a로 LF로도 줄바꿈문자로도 불린다. Unix에서의 구분 문자이다.
* `\r\n`: CRLF로 불리며 복귀줄바꿈문자로도 불린다. Windows에서의 구분 문자이다.


<br />

---

## 문자열 다루기

---

* `(NSString *) stringWithString:(NSString *)string` : 복사
* `(NSString *) uppercaseString` : 대문자로
* `(NSString *) lowercaseString` : 소문자로
* `const char *UTF8String` : C 문자열로

<br />
<br />

---

# NSMutableString

---

NSString의 서브클래스로 NSString의 메소드를 모두 사용가능하다.

* `(id) initWithCapacity: (NSUInteger) capacity` : 인스턴스 생성
* `stringWithCapacity` :  편의 생성자
* `appendString: (NSString *)str` : append
* `insertString: (NSString *)aString atIndex: (NSUInteger) loc` : 문자열 넣기
* `deleteCharactersInRange: (NSRange) range` : 범위 삭제
* `(void) setString: (NSString *)aString` : 말그대로 setString
* `(void) replaceCharactersInRange: (NSRange) aRange withString: (NSString *)aString`: 교체


<br />
<br />

---

# NSArray

---

Cocoa 환경에서 객체를 배열로 다루는 표준 클래스는 NSArray클래스이다.

nil을 요소로 가지고 있을 수 없다.

<br />

---

## 배열 다루기

---

* `(id) array` : 빈 배열 생성
* `(NSUInteger) count` : element 개수
* `(NSUInteger) indexOfObject: (id) anObject` :  객체의 위치
* `(id) objectAtIndex: (NSUInteger) index` : 인덱스의 객체
* `(id) lastObject` : 마지막
* `(NSArray *) subarrayWithRange: (NSRange) range` : 범위의 배열
* `(BOOL) isEqualToArray: (id) anObject`: 비교
* `(NSArray *) arrayByAddingObject: (id) anObject` : 끝에 추가

<br />
<br />

---

# NSMutableArray

---

NSArray의 서브클래스로 배열 요소가 되는 객체를 추가 및 삭제할 수 있다.

<br />

---

## mutable 객체 다루기

---

* `(id) initWithCapacity: (NSUInteger) numItems` : numItems수만큼 빈 배열을 만듬
* `(void) addObject: (id) anObject`:  끝에 추가 nil은 안됨
* `(void) insertObject: (id) anObject atIndex: (NSUInteger)index` : 삽입
* `(void) replaceObjectAtIndex: (NSUInteger) index withObject: (id) anObject`: 대체
* `(void) exchangeObjectAtIndex: (NSUInteger) idx1 withObjectAtIndex: (NSUInteger) idx2` : 교체
* `(void) removeAllObjects` : 전체 삭제
* `(void) removeLastObject` : 마지막 삭제
* `(void) removeObjectAtIndex` : 인덱스에 있는 객체 삭제
* `(void) removeObjectsInRange` : 범위에 있는 객체 삭제
* `(void) removeObject: (id) anObject` : 같은 객체 삭제
