---
title: 더 좋은 앱을 만드는 방법
categories:
  - iOS
excerpt: "앱의 퍼포먼스를 향상시켜보자:)"
date: 2025-11-11
tags:
- iOS-PRO
---



<br />
<br />

---

# 개요

사용자는 앱이 버벅이지 않고 잘 작동하길 기대한다. 만약 잘 작동하지 않는다면 좋지 않은 앱으로 생각하여 지울것이다.

개발자는 앱의 지속적인 향상을 위해 아래의 4단계를 진행해야한다.

1. 앱의 현재 퍼포먼스에 대한 정보를 수집한다
2. 향상을 위한 가장 중요한 것을 결정한다.
3. 앱을 프로파일링한다.
4. 변화를 적용한다.

## 1

* Xcode Organizer를 이용하여 실행되는 시간, UI 반응성, 저장소, 메모리, 배터리에 대한 진단 보고서를 볼 수 있다.
* MetricKit을 이용하여 특정 수치들을 그래프로 보여주는 일종의 시각화 툴을 이용할 수 있다.
* TestFlight 테스터를 이용하여 앱의 베타버전의 피드백을 얻을 수 있다.
* 실제 사용자로부터 얻는다.

## 2

메모리, 디스크, 앱 실행시간, UI 등 앱의 향상을 위해 가장 중요한 것이 무엇인지 결정한다.

## 3

* 응답하지 않음 및 중단 :  Time Profiler 템플릿 이용
* 메모리 이슈 : Allocation & Leaks 템플릿 사용
* 배터리 이슈 : Energy Log 템플릿 사용
* I/O 이슈 : File Activity 템플릿 사용
* 네트워크 이슈 : Network 템플릿 사용

실제 장치에서 더 높은 앱 프로파일링 정확도를 가지며 퍼포먼스 이슈를 일으키는 코드를 찾는다.

그 변화는 클래스 단의 소규모 변화일 수도 앱의 아키텍쳐 변화일 수도 있다.

## 4

프로파일링한 변화를 구현하고, 이전 프로필과 이후 프로필에 대해 비교를 한다.

XCTest에서 측정한 퍼포먼스를 생각하며 이후의 퍼포먼스 이슈를 만들 가능성에 대해 생각해본다.



<br />

---

# 반응성

앱의 반응을 빠릿하게

<br />

## Hang & Hitch

-	Hang은 멈추는것, Hitch는 버벅이는 것
-	동기식 작업이 100ms(0.1초)가 넘어가면 안됨
-	부드러운 화면 움직임을 위해서는 16.7ms(60hz -초당 60번 새로고침) 8.3ms(120hz -초당 120번 새로고침)를 고려
-	앱이 메인스레드를 UI 상호작용으로만 사용하도록 설계
-	다른 모든 작업은 백그라운드 스레드로 토스
-	async를 적극 활용

```swift
// 적극 활용 예시
Button("I don't hang") {
    Task {
        await doLongRunningWork() // 백그라운드에서 실행됨
        await updateUI()            // 완료 후 메인 스레드에서 UI 업데이트
    }
}

// @MainActor가 아님
@MainActor
func updateUI() { /* ... */ }

// 이 함수는 nonisolated (Actor에 속하지 않음)
private func doLongRunningWork() async {
    /* ... 오래 걸리는 무거운 작업 ... */
}


//동기식으로 만들어야한다면
Button("I don't hang") {
    Task.detached { // MainActor 컨텍스트를 상속받지 않음
        doLongRunningWork() // 백그라운드에서 실행됨
        await MainActor.run { // UI 업데이트는 다시 MainActor로 복귀
            updateUI()
        }
    }
}

// @MainActor가 아님
func updateUI() { /* ... */ }

// 이 함수는 동기식(sync) 함수
private func doLongRunningWork() {
    /* ... 오래 걸리는 무거운 작업 ... */
}
```

-	가변 주사율 때문에 60HZ를 목표로 하는 것이 더 나은 방법
-	XCTest measure(:)로 측정 가능함
-	Time Profiler로 디버깅
-	렌더링 파이프라인
	1. 사용자가 클릭하면 하드웨어가 감지하고 OS로 보냄
	2. 시스템이 이벤트를 앱의 이벤트 큐로 넣음
	3. 앱의 메인스레드가 큐에서 이벤트를 가져와 처리함
	4. 메인스레드는 UI를 수정하고 뷰 계층과 레이어 트리에 적용
	5. 렌더 서버가 처리하고 비트맵 생성
	6. Vsync마다 디스플레이 업데이트함
-	Hang: 3이 오래 걸리는 것, 메인스레드에서 50ms이상의 동기식 작업을 수행중
-	Hitch: 3,4,5에서 오래걸려서 Vsync 타이밍을 놓침
-	UI 작업과 Non-UI 작업을 분리 필수


<br />

## SwiftUI

-	스유에서 반응성은 body 계산 속도에 달려있다.
-	계산이 너무 오래걸리거나 너무 자주 업데이트 되면 오버헤드가 발생하고 16.67안에 계산 못하고 Hitch발생함
-	Instrument/SwiftUI를 이용해서 디버깅
	-	Update Groups: 스유가 앱의 업데이트를 계산하는 데 사용한 시간 
	-	Long View Body Updates: 500us(0.5ms)이상은 주황색, 1000us(1ms)이상은 빨간색
	-	Long Platform View Updates: 오래걸리는 uikit뷰
	-	Other Long Updates: 지오메트리 계산, 텍스트 레이아웃등 기타 작업
-	뷰 계산이 오래걸리는 경우
	-	계산을 비동기 작업으로 분리 및 결과는 캐시
-	뷰 업데이트가 너무 많음 
	-	ObservableObject는 뷰가 사용하지 않는 프로퍼티가 변경되어도 업데이트함 따라서 @Observable을 사용 권장
	-	최대한 뷰를 가볍게, 단일 UI만 나오도록 설계
-	body는 UI 구조를 선언하는 곳이지 비즈니스 로직을 처리하는 곳이 아님
-	init, body, onappear, onchange, 뷰의 상태를 바꿀 수 있는 modifier에서 오래걸리는 작업은 하지마라
-	body 안에서는 매우 엄격하게 로직을 처리하면 안됨. print 조차도. body는 0.5ms만 넘어도 느리다고 간주
-	modifier는 기준이 Hang으로 100ms까지는 여유있지만 하지마
-	SwiftUI의 모든 뷰는 기본적으로 @MainActor에서 실행되므로 거기서 호출하는 코드는 모두 메인스레드
-	백그라운드에서 실행될 애가 있으면 Task.detached를 이용해서 백그라운드로 보내야함 but UI업데이트할거는 await MainActor.run으로
-	GeometryReader, ScrollViewReader는 부모뷰의 변경을 관찰하여 자신을 다시 계산 따라서 해당 부분은 별도 뷰로 분리
-	자식뷰의 데이터가 필요하지않다면 클로저를 저장하지마라, 클로저는 상태를 캡처할 수 있음, 그 상태중 하나라도 바뀌면 뷰는 다시 계산됨
-	자주 변경되는 상태(@State)와, 그 상태와 관련 없는 '비싼 자식 뷰'를 같은 body 안에 두지 말아라
-	뷰 안에서 var ~~:view랑 함수로 뷰를 만드는것보다 별도의 뷰 구조체로 빼는게 압도적으로 좋다.
	-	SwiftUI가 diff 할 수 있는 독립적인 단위가 된다.
	-	부모뷰의 body가 실행되어도 독립적인 뷰의 body를 이전과 다음을 diff한다음 재사용함

```swift
// 클로저 저장했을 때
struct BadView<Content: View>: View {
    let content: () -> Content 
    @State private var internalCounter = 0

    var body: some View {
        let _ = print("BadView body re-calculated")
        content() // 여기서 클로저가 실행됨
    }
}
// 부모뷰
struct ContentView: View {
    @State private var unrelatedCounter = 0 

    var body: some View {
        VStack {
            Button("Increase Unrelated Counter") {
                unrelatedCounter += 1 // 부모의 @State 변경
            }
			// 뷰 다시 그림
            BadView(content: {
                Text("Hello") // 이 클로저는 ContentView의 'self'를 캡처하여 클로저 값이 달라짐
            })
        }
    }
}


// 올바른 예시
struct GoodView<Content: View>: View {
    let content: Content 
    @State private var internalCounter = 0 

    init(@ViewBuilder content: () -> Content) {
        self.content = content() 
    }

    var body: some View {
        let _ = print("GoodView body re-calculated")
        content
    }
}


```

<br />

## 앱 launch 시간

-	앱 실행은 main()함수가 실행되기 전 pre-main과 실행된 후로 나뉨
-	pre-main
	-	동적 링커(dyld-dynamic linker editor)가 실행을 준비함
	-	의존성이 있는 dynamic framework를 메모리로 로드
	-	포인터 주소를 재조정하고 심볼등을 연결
	-	전역변수 실행 및 로드
-	main
	-	application(_:didFinishLaunchingWithOptions:) / SwiftUI의 @main
	-	무조건 가볍게 유지해야됨
	-	첫화면을 그리는 데 필수적이지 않는것을 모두 지연시켜야됨




<br />

---

# 메모리

-	기기의 램은 앱, os, 커널과 공유하는 한정된 자원
-	iOS는 백그라운드 앱이 메모리를 너무 많이 쓰면 ssd로 옮김

<br />

---

## Dirty Memory

-	iOS 메모리 구조를 이해하기 위해선 가상 메모리와 페이징에 대한 이해가 필요
-	iOS는 앱에게 메모리 영역을 할당해주는데 물리 램 주소가 아닌 가상 메모리 주소임
-	실제 램에 접근하는 일은 iOS에서 담당하며 프로그램은 가상공간 상에서 동작
-	가상공간은 온전히 프로세스에게 할당된 공간이고 프로세스에서 사용한 메모리들은 물리 램에 흩어져서 존재함
-	가상메모리에서 일정한 크기로 나눈 블럭을 page(16kb)라고 하며 실제 메모리에서는 Frame이라고 한다.
-	각 프로세스는 어떤 페이지가 어떤 물리주소에 매핑되어야 하는지를 저장한 페이지 테이블을 가지고 있다.

<br />

<figure>
	<a href="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/a5c8eb45-e1fd-4c2c-8b04-35f8233e3895">
		<img src="https://github.com/dq-QQQ/dq-QQQ.github.io/assets/79088896/a5c8eb45-e1fd-4c2c-8b04-35f8233e3895" class="w8" />
	</a>
</figure>

-	앱이 사용하고 있는 메모리는 `Clean`, `Dirty`, `Compressed`로 나눠짐
	-	Clean 메모리는 기록될 수 있는 깨끗한 메모리를 의미. (malloc(10))
	-	Dirty는 앱에서 수정한 데이터들, 프레임워크 dirty 메모리를 포함(a[0] = 1)
		-	그러면 이 dirty 공간을 포함한 16kb 전체가 dirty화
	-	Compressed 메모리는 일정기간동안 사용되지 않은 메모리를 압축
-	iOS는 디스크 스왑 공간이 없다. Swap 공간은 RAM이 모두 찼을 때 RAM에서 잘 사용하지 않는 page들을 옮겨 두는 disk 공간이다.
-	앱이 사용할 수 있는 메모리는 기기별로 다른데 보통 램의 50% 미만, 70%가 넘으면 크래쉬
-	시뮬레이터에서는 macOS위에서 실행되며 ios 메모리 정책을 따르지 않음 따라서 실기기에서 테스트해야됨


<br />

---

## 이미지의 메모리 로드

이미지의 메모리 사용량은 파일 크기와 관련이 있는 것이 아니라 이미지의 크기와 관련되어있다.

크기가 590kb이고 1536px X 2048px의 이미지가 있다고 생각해보자. 이 이미지의 메모리 사용량은 590kb가 아니라 1536 * 2048 * 4bytes 로 10mb정도이다.

iOS는 이미지를 메모리에 올리기 위해 `load`, `decode`, `render`의 단계를 거친다.

* load : 590kb를 메모리에 올린다.
* decode : GPU가 읽을 수 있도록 압축을 바이트 단위로 풀어 포멧을 변경한다.
* render : 압축 해제된 코드에 따라 화면에 뿌려준다.

<br />

---

### 이미지 랜더링 포멧

* Luminance and alpha 8 Format : 픽셀당 2Bytes로 grayscale값과 alpha 값만 지원하여 메탈 셰이딩할 때 사용
* SRGB : 픽셀당 4Bytes로 기본 포멧
* Wide : 픽셀당 8Bytes 더 많고 정확한 색을 표현할 수 있고 필요한 경우에만 사용

iOS는 최적의 이미지 포맷을 선택해준다.

<br />

---

## 메모리 사용을 줄이는 방법


-	앱이 보여주는 크기에 맞게 asset을 최적화. 
-	네트워크나 사진 라이브러리에서 불러오는 이미지는 `Image I/O` 프레임워크를 이용하여 최적화.
-	UIImage를 이용하면 원본 데이터가 메모리에 Dirty로 올라간 뒤 리사이징됨, ImageIO는 아님
-	CoreData 작업 최적화
	-	Core Data는 NSManagedObject의 변경 사항을 NSManagedObjectContext라는 메모리 공간에 저장
	-	context.save()를 호출하기 전까지, 이 모든 변경 사항은 메모리에 계속 쌓임
-	앱이 백그라운드로 갔을 때 고용량의 데이터를 메모리에 유지하는 것은 낭비임 다 없애주고 나타날 때 다시 로드해야됨
-	릭 잘잡아야됨
-	데이터 사용 끝나면 초기화 해줘야됨



<br />

---

## 앱 크기를 줄이는 방법

-	Optimization Level 선택하기
-	이미지를 폴더째 프로젝트로 넣지 말고 asset 이용할 것
-	jpg,png 대신 heif 포맷 사용
-	H.264 대신 HEVC(H.265) 사용
-	32bit png,jpg파일은 이미지 압축을 이용(web용 리소스)
-	오디오는 ACC, MP3코덱 사용
-	bit rate를 낮추고, sample rate는 44.1kHz 이하로 낮은 레이트 사용
-	On Demand Resource 활용
-	version.json과 같이 자주 바뀌는 리소스는 따로 뺌(업데이트 diff 때문)


<br />

---

# 배터리

-	기기는 앱이 사용하지 않는 부품(Wi-Fi, 셀룰러 칩 등)의 전원을 꺼서 배터리를 아낌
-	하드웨어를 사용하는 작업이 배터리 소모가 매우 큼
-	제일 중요한것은 작업 자체를 줄여라
-	CPU 작업을 효율적으로 스케줄링하라
	-	효율적인 알고리즘 선택하라
	-	캐싱을 이용하라
	-	객체를 해제하고 다시만드는 작업을 불필요하게 하지마라
	-	이벤트가 발생하면 처리하는 설계를 하라
	-	Apple의 api를 사용하라
-	멀티스레딩을 활용하라
	-	async/await, gcd를 적극 활용하라
		-	너무 자잘하게(1ms 미만 작업 1000개) 쪼개면 스케줄링하고 스레드간 이동시키는 비용이 더 비쌈
		-	너무 크게 쪼개면 일하는애만 일해서 각각의 작업이 10ms~100ms 사이가 이상적임
	-	백그라운드로 보낼 때 QoS를 반드시 설정하라. 낮으면 고효율 cpu가 처리하므로 배터리 절약에 도움
	-	나중에 해도 되는 큰(몇분 단위) 작업은 BGTaskScheduler를 활용하라
		-	앱의 콘텐츠 미리 받아두기
		-	앱 내부에 쌓인 로그나 캐시 삭제
		-	콘텐츠 다운로드(넷플릭스 오프라인 다운로드)
		-	ML 모델 학습
		-	서버에 앱의 데이터를 백업할 때
-	렌더링을 효율적으로 하라
	-	Hang과 Hitch를 줄여라
	-	애니메이션의 Frame rate를 설정하라
	-	setNeedsDisplay() 대신 업데이트가 필요한 영역을 넘겨라
	-	서로 멀리 떨어진 뷰를 하나의 뷰로 묶지 마라
	-	다크 모드(Dark Mode)를 지원하라
-	하드웨어 사용을 줄여라
	-	필요한 경우가 아니라면 고화질 카메라 캡쳐는 피하라
	-	URLSession의 인스턴스를 불필요하게 만들지 마라, 각각의 인스턴스가 서버와 별개의 연결을 함
	-	실시간 핸드쉐이킹을 해야하는게 아니라면 일괄처리하라
	-	URLSessionConfiguration을 이용하여 네트워크 상태에 따른 통신을 설정하라
	-	백그라운드 통신이 실패한 경우 바로 재시도 하지 말고 대기시간을 2배씩 늘려라(5분뒤 재시도 -> 10분뒤 재시도)
	-	높은 정확도의 위치파악이 필요하지 않으면 CLLocationManager 대신 CLMonitor를 사용하라
	-	distanceFilter를 이용해서 위치를 업데이트하는 빈도를 최소화해라
	-	ssd에 대한 쓰기 작업 횟수를 줄여야함(캐싱 적극 활용)
	-	JSON, XML, plist 저장을 피하라. 1바이트만 수정해도 파일 전체를 수정해야됨, SwiftData, CoreData를 사용
	-	복구가 가능한 데이터는 Caches, tmp 폴더에 저장하라
	-	FileManager의 copyItem은 원본데이터의 참조를 생성하는 것으로 적극 활용
