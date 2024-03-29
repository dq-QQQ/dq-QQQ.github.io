---
title: 오즈 독사 iOS 사내 프로젝트
date: 2024-01-19
excerpt: "오즈 독사 개발기:)"
categories:
- iOS
tags:
- iOS-PRO
---



# 개요

이번에 전자문서 위변조를 검증하는 사내 프로젝트의 iOS 개발을 맡게되었다. 만쉐이~

이 프로젝트는 웹, 안드로이드, iOS, 서버, Windows 개발자가 협업하는 프로젝트다.

iOS 개발을 하시는 실장님이 계시긴 하지만 PM느낌으로 다 관여하셔서 iOS의 세부설계는 내가 하게되었다. 만쉐이~

우리회사 주 제품군인 OZ와는 별개의 프로젝트이므로 신기술 써보고 싶은거 좋은거 다 써봐도 좋다고 하셨다. 만쉐이~

그래서 TCA, TDD, Tuist(다 t로 시작하네,,,iOS 개발자는 T야?)등 유명한 iOS 개발 지식을 알아보고 괜찮으면 도입하려고한다.


<br />

---


# 무슨 앱이야?

-   앱 이름은 OZVeriScanner(oz독사가 좋은데,,,)
-   우리회사 주 제품군은 전자문서를 다룸
-   전자문서에 큐알코드를 삽입하고 해당 큐알을 앱으로 스캔하면 원본 문서인지를 검증해주고 띄워주는 앱
-   타겟 사용자는 우리 고객사의 직원(그래서 그런가 UI는 중요도가 떨어져보임ㅠㅠ)



<br />

---


# 무슨 기능이 필요할까?

-   큐알코드 스캔 기능
-   큐알에 있는 링크는 우리 내부 서버라고 했음 그러니 네트워크 통신 기능
-   자세한 이유는 말 못하지만 .APP의 보안 수준, 디컴파일도 고려
-   링크를 통한 위변조 검증 기능
-   서버로 보낼 데이터를 암호화하는 기능
-   전자문서를 암호화해서 넘겨준다고 했으니 복호화 기능
-   복호화한 전자문서를 띄워주는 기능

이건 입사한 지 3달 째인 내가 정할 수 없으니,,, 

<br />

---


# 어떤 기술 스택을 사용할까?

이것들을 입사한 지 3달 째인 내가 정할 수 있다니,,,만쉐이~

많이 알아보고 왜 그 스택을 사용했는 지 적어놔야지

일단 사용할 기술스택이라고 할만한 것을 정리해봤다.

-   프로그래밍 언어
-   UI 개발 프레임워크
-   최소 지원 iOS 버전
-   앱의 아키텍쳐
-   QR Scanner
-   네트워크 통신 방법
-   비동기 처리 기술
-   문서를 띄워줄 뷰어
-   암호화, 복호화
-   의존성 관리도구
-   생산성을 높여주는 기타 라이브러리

<br />

## 프로그래밍 언어 / UI 개발 프레임워크

서로 관련이 있는 것이라 Swift랑 SwiftUI로 정했다.

현재 주 제품군의 코드는 Objective-C / UIKit으로 되어있음. 이것을 추후에 Swift / SwiftUI로 전환할 예정

어짜피 iOS 개발의 트렌드는 SwiftUI가 차지할 것이기 때문에 굳이 옛날의 것을 사용할 필요가 없음

이번 프로젝트는 비교적 간단한 앱이지만 주 제품군의 코드는 몇십만줄이기 때문에 이것을 전환하기 위한 전초전 같은 느낌

그리고 나는 SwiftUI가 더 자신있고 재밌음 objc랑 uikit은 어려워

<br />

## 최소 지원 iOS 버전

흠 iOS 14를 할까 15를 할까 고민중

일단 14?

15에서 List가 많이 수정된것같은데 List가 안들어갈듯함? 그것도 그러고 15에서 추가된 내용이 크리티컬하게 앱에 영향 주는게 없음

근데? 우리회사에 iOS 14 장비가 없음

옛날 장비들 강제 다운그레이드나 탈옥 해봐도 되냐고 물어봤지만,,,바로 컷ㅠㅠ 한번 해보고 싶었는디 까비

그리고 우리 주 제품은 라이브러리로 배포해주는 형식이니깐 보수적으로 최소로 잡아 iOS 12인거지 우리가 앱으로 배포하는건 높게 잡아도 된다고 하셨다.

그래서 15로 하라고 했으므로 15로 편하게 결정!

버전별 호환성은

<br />

## 앱의 아키텍쳐

나는 SwiftUI에서 mvvm을 기반으로 구현하는 것이 이해가 되지 않았다.

이것은 iOS 개발에서 꽤 논란이 되는 주제로 조금만 구글링해봐도 많은 사람들이 의문을 가지는 것을 볼 수 있다.

나 또한 뷰모델의 존재에 대한 의문이 있었고 mvvm으로 구현했던 dq의 다음 프로젝트는 다른 아키텍쳐를 사용해야겠다고 생각했다.

종류가 굉장히 많더라 mvvm, mvi, clean architecture, tca, viper, ribs등등

그중 SwiftUI에서 가장 핫한 아키텍쳐 TCA! 현대차, 라인등 수많은 개발사에서 채택한 TCA! 그리고 무엇보다 dq 개발할 때도 관심이 있던 TCA가 강력한 후보였다.

아마 취업이 바로 안됐다면 dq를 TCA로 재구현 해볼 예정이었을 정도로 TCA에 대해서 관심이 많았다.

이번에 한번 맛보기로 알아봤는데 이 아키텍쳐를 한번 적용해봐야겠다라는 생각이 들었다.

간단한 샘플이긴 했지만 앱 데이터의 구조가 단방향으로 각 파트들이 왜 존재하는지 단번에 이해가 되었다.

근데 TCA를 알아볼수록 학습곡선이 많이 필요해보였다. 근데 이해하면 강력한 무기가 될 것같았다. 맘에들었어 TCA

실제 프로덕트에 적용하기엔 나의 이해도도 그렇고 사이드 프로젝트면 공부를 계속해서 완벽히 이해한 후 개발하겠지만 회사 업무이니 마냥 그럴수는 없었다.

따라서,,, 둘 다 해보기로 했다! MVVM은 알고 있으니 바로 개발을 들어가면 되고 금방 개발할 수도 있다.

신입이라 그런가 다른분들보다 할당된 업무가 적어서 나름 일정에 여유가 있었다. 그러니 빠르게 `MVVM`으로 개발하고 `TCA`로 다시 짜보기로 했다.

그러면 두 방식을 비교해보고 어떤게 더 좋은 지 체감되지 않을까 싶다. 둘 다 개발하고 실장님께 컨펌받은 코드로 회사 Git에 푸시하기로 정했다.

<br />

## QR Scanner

우리 주 제품 iOS 코드도 그렇고 처음 회의할 때 나왔던 얘기는 zixing을 사용하는 것이었다.

근데 나는 개발할 때 아무리 좋은 외부 라이브러리를 쓰는 것보다 기본으로 제공해주는 것을 선호한다.

알아보니 AVFoundation 프레임워크를 사용하면 QR Scanner를 만들 수 있는 것 같았다.

따라서 `AVFoundation`을 사용하기로 정했다.


<br />

## 네트워크 통신 방법

이건 뭐 당연히 `URLSession`을 이용할 것

기본으로 제공해주는데 편의를 위한 외부라이브러리는 안씀. 스냅킷 같은것도 별로 안좋아함

뭐 alamofire 이용하면 편리한건 알지만 안할거임 이게 내 스타일임

<br />


## 비동기 처리 기술

뭐 GCD도 있고 Async/Await도 있고 rx도 있고 combine도 있다

Async/Await이랑 combine을 사용할듯하다.



<br />

## 문서를 띄워줄 뷰어

전자문서는 무조건 PDF형태로 가져온다고 그랬다.

그럼 이것도 당연히 내부 `PDFKit`을 사용할 것

예전에는 없었나보다 그래서 잘 알아봐야할 것 같다고 실장님이 그러셨는데 PDFKit을 이용하면 간단하게 구현가능

<br />

## 암호화, 복호화

문서등의 데이터 암호화 방식을 여러번 꼬았다. 그 과정에서 발생하는 문제점이 공개키로 복호화를 해야하는 부분이 존재하는 것이었다.

보통의 경우는 공개키로 암호화를 하고 개인키로 복호화를 한다.

처음에 이 말을 듣고 뭐 잘되겠지~ 생각하며 이것도 당연히 기본으로 제공해주는 Security 프레임워크를 사용하려고 했다.

그러나!!!!!!!!!!!!!!!!!!!!!!!

이걸 막아 놓네;;; Security 프레임워크에서 제공하는 'decryptwithData' api를 사용하면 공개키로 복호화가 안된다,,,

iOS 15에서 deprecated된 예전 api를 사용하면 되지만 이건 사용하지말고 다른 방법을 찾아보라고 하셨다,,,

따라서 RSA 암호화 방식을 사용할 수 있는 다른 방법을 생각해봤다. OpenSSL이라는 것을 이용하면 공개키로 복호화가 되는것 같았다.

따라서 `OpenSSL`을 이용하기로 했다.


<br />

## 의존성 관리도구

First-Party인 SPM을 사용할 것

그러나 Openssl은 SPM으로 사용할 수 없음

따라서 CocoaPod 사용했음



<br />

## 생산성을 높여주는 기타 라이브러리

우선 TDD와 Tuist가 생각났다.

TDD도 학습곡선이 있었다. 따라서 TCA를 적용해서 개발할 때 사용해보기로 했다. TCA의 장점이 테스트가 쉬워진다는것도 있으니,,,

Tuist는 적용하지 않기로 했다. MVVM에 TDD를 하지 않는 이유와 비슷한데 이번 프로젝트의 규모와 학습곡선 때문이다.

일단 TDD도 좀 투머치라고 생각할 정도로 이번 프로젝트의 규모가 크지 않다.

그렇게에 프로젝트 관리도구인 Tuist까지 하는것은 오버엔지니어링이라고 생각했다.

TDD는 나중에 주 제품을 전환할 때 거의 확실시 하게 사용해야한다. 몇십만줄이나 되는 코드를 중간중간 테스트 없이 개발한다,,,? 이건 너무 위험하다.

그래서 TDD는 언젠가 학습할 예정이긴했다. 그리고 TCA랑 TDD만 제대로 이해하는 것도 쉽지 않을 텐데 tuist까지? 절레절레

이번엔 일단 TCA와 TDD만 제대로 이해하고 적용해보고 tuist는 나중에 학습하기로 결정했다.



<br />

---

# 개발

개발을 하며 많이 고민했던 문제들에 대해서 정리해봤다.

앱 테마가 위변조 검증인 만큼 RSA 암복호화를 많이 고민했고 코드도 제일 길다.

근데 이건 제품 주요 로직이라 내 머릿속에만 저장...

RSA 구현 방식도 공부해보려했으나,,,투머치같아서 대략적인 내용까지만

[SwiftUI에서 UIKit 사용하기](https://dq-qqq.github.io/ios/2024/02/13/UIKitInSwiftUI/)

[의존성 관리 방법](https://dq-qqq.github.io/ios/2024/01/18/Package/)

<br />

---

## 큐알 스캐너 만들기

<br />

---

### AVKit과 AVFoundation

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/c4133333-db8f-49d9-b546-a174ca1af545">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/c4133333-db8f-49d9-b546-a174ca1af545" class="w8" />
	</a>
</figure>

<br />


-   AVFoundation - 오디오 및 미디어를 처리하기 위한 프레임워크
    -   좀 더 로우레벨 처리가 가능함
    -   다양한 멀티미디어 처리가 가능함
-   AVKit - AVFoundation 기반의 재생 특화 프레임워크
    -   근데 import AVFoundation하던데 이게 더 광범위한거 아닌가 싶음
-   비디오 재생만 시킬거 아니면 왠만하면 AVFoundation 쓰면될듯
-   공식문서에도 AVKit은 iOS Playback and Capture 챕터밖에 안다룸
-   이 프레임워크는 UIKit 기반이므로 UIRepresentable을 사용해서 뷰를 만들어야함
-   나는 스캐너를 만들거니깐 AVFoundation/Capture의 지식만 필요함
    -   카메라, 마이크로부터 오디오 및 비디오 데이터를 캡처하는 기능
    -   크게 device, session, input, output으로 나눌 수 있음

<br />

---

### Capture Session

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/8cfadc0c-a369-41f4-8166-f2da7dc49f59">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/8cfadc0c-a369-41f4-8166-f2da7dc49f59" class="w8" />
	</a>
</figure>

<br />

위의 그림을 보면 AVCaptureDevice -> AVCaptureInput -> AVCaptureSession -> AVCaptureOutput의 흐름으로 처리가 된다.

차근차근 하나씩 알아보자

#### Capture Device

-   어떤 카메라를 사용할지 선택하는 클래스
    -   전면, 후면, 듀얼, 트루톤, 광각등등 (AVCaptureDevice.DeviceType 참고)
-   default(_:for:position:) - 간단한 경우
-   AVCaptureDevice.DiscoverySession - 특정 조건을 준 카메라일 경우
-   capture device는 여러 설정 옵션을 제공함
    -   화면 포커스, 노출등등
    -   설정전에 lockForConfiguration()을 호출해야함(뮤텍스같은 느낌?)
-   카메라 권한 설정도 이곳에서 관리
    -   AVCaptureDevice.authorizationStatus
-   카메라 라이트 설정도 이곳에서 관리
-   등등등 뭔가 하드웨어적인 제어를 하는 곳

#### Capture Input

-   Capture Device에서 얻은 하드웨어 정보를 세션에 추가할 때 사용하는 클래스
    -   session.addInput(AVCaptureDeviceInput(device: device))


#### Capture Session(큐알)

-   beginConfiguration()으로 configuration 잠금
-   addInput()으로 입력 장치 설정
-   addOutput()으로 결과 설정
-   commitConfiguration()으로 configuration 해제

위 방법으로 만든 카메라 세션을 AVCaptureVideoPreviewLayer의 세션으로 설정한다.

그 viewLayer를 UIView.layer에 추가하여 커스텀 뷰 생성

#### Capture Output(큐알)

-   session.addOutput에 AVCaptureMetadataOutput을 넣어야함
-   metadataObjectTypes = [.qr]로 설정함
-   AVCaptureMetadataOutputObjectsDelegate를 채택한 클래스도 설정함
    -   이 델리겟에서는 metadataObjects라는 것으로 문자열 추출 가능


```swift
func metadataOutput(_ output: AVCaptureMetadataOutput, didOutput metadataObjects: [AVMetadataObject], from connection: AVCaptureConnection) {
        if let metaObject = metadataObjects.first {
            guard let readableObject = metaObject as? AVMetadataMachineReadableCodeObject else { return }
            guard let code = readableObject.stringValue else { return }
            scannedCode = code
        }
    }
```

이렇게 추출한 큐알코드의 내용을 가지고 다음 처리를 하면 됨


<br />

---

# 후기

