---
title: SwiftUI로 QR코드 스캐너 만들기
date: 2024-02-13
excerpt: "SwiftUI로 QR코드 스캐너 만들기:)"
categories:
- iOS
tags:
- iOS-PRO
---



# 개요

애플에서 제공해주는 AVKit과 AVFoundation을 이용해서 QR 스캐너를 만들어보겠다.


<br />

---

# AVKit과 AVFoundation

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

# Capture Session

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/8cfadc0c-a369-41f4-8166-f2da7dc49f59">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/8cfadc0c-a369-41f4-8166-f2da7dc49f59" class="w8" />
	</a>
</figure>

<br />

위의 그림을 보면 AVCaptureDevice -> AVCaptureInput -> AVCaptureSession -> AVCaptureOutput의 흐름으로 처리가 된다.

차근차근 하나씩 알아보자

## Capture Device

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

## Capture Input

-   Capture Device에서 얻은 하드웨어 정보를 세션에 추가할 때 사용하는 클래스
    -   session.addInput(AVCaptureDeviceInput(device: device))


## Capture Session(큐알)

-   beginConfiguration()으로 configuration 잠금
-   addInput()으로 입력 장치 설정
-   addOutput()으로 결과 설정
-   commitConfiguration()으로 configuration 해제

위 방법으로 만든 카메라 세션을 AVCaptureVideoPreviewLayer의 세션으로 설정한다.

그 viewLayer를 UIView.layer에 추가하여 커스텀 뷰 생성

## Capture Output(큐알)

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
