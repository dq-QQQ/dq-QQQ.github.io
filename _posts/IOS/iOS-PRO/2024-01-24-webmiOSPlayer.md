---
title: iOS에서 webm을 재생시켜보자
date: 2024-01-24
excerpt: "iOS기기에서 webm 비디오를 재생시켜보자:)"
categories:
- iOS
tags:
- iOS-PRO
---

# 개요

우리 회사 제품은 크게 iOS, Android, HTML5, ActiveX 뷰어 제품이 있다.

어떤 동영상을 저장하고 각 뷰어에서 실행시켜줘야 하는 기능을 추가하는 중에 트러블이 발생했다.

다른 뷰어와는 다르게 iOS에서는 webm 코덱의 비디오가 재생되지 않는 문제였다.

안드로이드나 웹은 webm 코덱을 지원한다. 모든 경우 중 iOS에서 webm을 실행시키는 경우만 문제가 된다.

애초에 저장할 때 호환성이 높은 mp4로 저장할 수도 있지만 

저장 빈도 vs iOS에서 webm 실행 빈도 수와 같은 비용 문제를 고려한 결과

iOS에서도 webm 포맷의 비디오를 지원하는 방법으로 결정했다.

내가 처음 생각한 방법은 다음 3가지였다.

-   webm을 mp4로 변환
-   webm player를 앱에 심기
-   webView

각 방법에 대해서 살펴보겠다.


<br />

---

# webm을 mp4로 변환

FFmpeg을 사용했다.

## FFmpeg

-   오디오와 비디오와 같은 미디어 파일을 다루는 오픈소스 멀티미디어 프레임워크
-   멀티미디어를 다루는 거의 모든 소프트웨어에서 표준으로 사용한다고 보면 됨
-   `brew install ffmpeg`로 설치하여 command Line Tool로 사용 가능
-   특징
    -   ffmpeg : 미디어 포맷 변환 도구
    -   ffplay : 간이 파일 재생기
    -   ffprobe : 미디어 정보 표시 도구
    -   ffserver : 라이브 방송을 하는 멀티미디어 스트리밍 서버. 버전 3.4이후 제거되었다.
    -   libavcodec : 오디오/비디오 코덱 라이브러리
    -   libavformat : 멀티미디어 컨테이너의 디먹서/먹서 라이브러리
    -   libavdevice : 입출력 장치 제어 라이브러리
    -   libavfilter : 미디어 필터 라이브러리
    -   libswscale : 이미지 처리 라이브러리
    -   libswresample : 오디오 처리 라이브러리

## FFmpeg-kit

-   iOS/Android에서 FFmpeg을 사용하게 해주는 오픈 소스 라이브러리
-   MacOS용 제품이면 별도의 작업 없이 NSTask를 이용해서 FFmpeg 사용가능
-   iOS용 제품은 해당 [라이브러리](https://github.com/arthenica/ffmpeg-kit)를 이용하면 됨



## iOS 프로젝트에 적용

다음과 같은 단계로 적용하였다.


-   PodFile에 `pod 'ffmpeg-kit-ios-full'`를 작성해 의존성 주입
-   사용할 파일에 `#import <ffmpegkit/FFmpegKit.h>`를 작성해 import

```
NSArray *command = @[
        @"-y",
        @"-i", webmFilePath,
        @"-c:v", @"h264",
        @"-c:a", @"aac",
        mp4FilePath
    ];
```

-   FFmpeg은 Command Line Tool이라 하였다. 위의 커맨드들을 실행하는 개념으로 구현되어있는듯하다.
-   `webmFile` in `webmFilePath`  -->> `h264/aac 코덱의 mp4File` in `mp4FilePath`
-   변환한 mp4 파일을 AVPlayer에서 재생

## 결과

-   느림
-   쉬움
-   하드웨어 가속, 스레드 수 설정 같은것으로 작업 성능 조절 가능
-   해상도가 변경됨(이유는 잘 모르겠음)
-   변환하는 작업의 시간적, 공간적 오버헤드 발생
-   라이센스 문제
-   미디어 관련 도메인 지식 필요해보임


<br />

---

# webm player를 앱에 심기

VLC media player를 사용했다.

## VLC

-  VideoLan Project에서 개발하는 오픈소스 media player
-  호환성 99%(os, video)
-  크로스플랫폼을 목적으로 개발
-  iOS용 제품은 해당 [라이브러리](https://github.com/videolan/vlckit)를 이용하면 됨
-  iOS 앱을 사용해봤는데 음...개판이다


## iOS 프로젝트에 적용

-   PodFile에 `pod 'MobileVLCKit'`를 작성해 의존성 주입
-   사용할 파일에 `#import "MobileVLCKit/MobileVLCKit.h"`를 작성해 import
-   `VLCMediaPlayerDelegate`을 채택한 뷰컨트롤러 생성
-   `VLCMediaPlayer`, `UIView` 생성
-   생성한 플레이어의 `.drawable`에 생성한 뷰 대입
-   `[플레이어 play]`로 비디오 실행

## 결과

-   빠름
-   복잡함
-   해상도 좋음
-   라이센스 문제
-   미디어 관련 도메인 지식 필요해보임
-   변환을 하지 않나,,,? 로컬에서는 바로 실행됨
-   서버 통신에 필요한 시간적 오버헤드가 있어보임


<br />

---

# webView

기본으로 제공해주는 WKWebView를 사용하고자 했다.

## WKWebView

-   iOS의 웹 뷰 컴포넌트
-   Safari 웹 브라우저의 엔진인 WebKit 기반
-   Safari에서 사용되는 Nitro JavaScript 엔진 사용