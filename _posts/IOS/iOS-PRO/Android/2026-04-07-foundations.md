---
title: Foundations
date: 2026-04-07
excerpt: "Android 학습"
categories:
- Android
tags:
- iOS-PRO
- Claude
- AI
- Android
---



<br />

---

# 1.1 Android 플랫폼 아키텍처

## 핵심 개념

Android는 5개 계층으로 구성된다 (아래→위):

```
┌─────────────────────────────┐
│        App Layer            │  ← 우리가 만드는 앱 (Kotlin/Java)
├─────────────────────────────┤
│    Android Framework        │  ← Activity, View, Manager들
├─────────────────────────────┤
│      ART (Runtime)          │  ← .dex 바이트코드 실행 엔진
├─────────────────────────────┤
│     HAL (하드웨어 추상화)      │  ← 다양한 제조사 하드웨어 통일
├─────────────────────────────┤
│      Linux Kernel           │  ← 메모리, 프로세스, 드라이버
└─────────────────────────────┘
```

## iOS와 비교

| 계층 | Android | iOS |
|---|---|---|
| 커널 | Linux Kernel | Darwin Kernel |
| 하드웨어 추상화 | HAL (필수) | **(거의 불필요)** - Apple 하드웨어만 |
| 런타임 | ART (바이트코드 실행) | **(없음)** - 네이티브 컴파일 |
| 프레임워크 | Android Framework | Cocoa Touch (UIKit/SwiftUI) |
| 앱 | Kotlin/Java | Swift/ObjC |

## 바이트코드와 ART

### 바이트코드란?

사람 언어도 아니고 기계어도 아닌 **중간 언어**. 어떤 기기든 ART만 있으면 실행 가능.

```
iOS:     Swift 코드  →  컴파일  →  기계어 (바로 실행)
Android: Kotlin 코드 →  컴파일  →  바이트코드(.dex)  →  ART가 번역  →  기계어
```

### ART vs JVM

Google이 JVM 대신 ART를 만든 이유: **모바일 환경의 제약** (메모리, 배터리, 발열)

| | JVM (PC) | ART (Android) |
|---|---|---|
| 실행 방식 | JIT (실행할 때마다 번역) | AOT + JIT 혼합 (설치 시 미리 번역) |
| 바이트코드 | `.class` (Java bytecode) | `.dex` (Dalvik bytecode) - 더 컴팩트 |
| 메모리 | 넉넉하게 사용 | 모바일 최적화 GC |

### HAL이 중요한 이유

- Android는 **오픈소스** → 제조사마다 하드웨어가 다름 (삼성, 샤오미, 구글...)
- HAL이 카메라, GPS, 블루투스 등을 **통일된 인터페이스**로 추상화
- iOS는 Apple 하드웨어만 지원하므로 이 계층이 거의 불필요

## 핵심 정리

1. **Android = Linux 기반, iOS = Darwin 기반** (둘 다 Unix 계열)
2. **ART 계층이 추가** - 다양한 하드웨어에서 실행하기 위한 바이트코드 방식
3. **HAL이 필수** - 오픈소스 → 하드웨어 파편화 대응


<br />

---

# 1.2 Android 프로젝트 구조

## 프로젝트 전체 구조

```
MyApp/
├── build.gradle.kts (프로젝트)  ← 전체 공통 설정
├── app/
│   ├── build.gradle.kts (모듈) ← 앱 모듈 설정
│   ├── src/main/
│   │   ├── AndroidManifest.xml ← 앱 메타데이터
│   │   ├── java/              ← Kotlin/Java 소스 코드
│   │   └── res/               ← 리소스
│   └── src/test/              ← 테스트 코드
└── gradle/                     ← Gradle 설정 파일들
```

## iOS와 대응표

| iOS | Android | 역할 |
|---|---|---|
| `.xcodeproj` | `build.gradle.kts` | 빌드 설정 |
| `Info.plist` | `AndroidManifest.xml` | 앱 메타데이터 |
| `Assets.xcassets` | `res/` 디렉토리 | 리소스 |
| `@2x/@3x` | `drawable-hdpi/xxhdpi/` | 해상도별 이미지 |
| `Localizable.strings` | `values-ko/strings.xml` | 다국어 |
| Swift Package | Gradle 모듈 | 모듈 분리 |

## Gradle: 멀티모듈 빌드

- iOS는 `xcodeproj` 하나로 관리
- Android는 **프로젝트 루트 gradle + 모듈별 gradle** 구조
- 모듈마다 독립 빌드 가능 → 바뀐 모듈만 재빌드 → 빌드 시간 단축

```
build.gradle.kts (프로젝트)  ← 전체 공통 설정
├── app/build.gradle.kts     ← 앱 모듈
├── core/build.gradle.kts    ← 코어 모듈
└── feature/build.gradle.kts ← 피처 모듈
```

## 리소스 시스템 (`res/`)

### 폴더 구조

```
res/
├── layout/              ← XML 레이아웃 (Storyboard/XIB 역할)
├── drawable/            ← 이미지, 아이콘
├── values/
│   ├── strings.xml      ← 문자열
│   ├── colors.xml       ← 색상
│   └── dimens.xml       ← 크기 값
├── mipmap/              ← 앱 아이콘 전용
└── ...
```

### Qualifier 시스템 (핵심!)

폴더 이름에 조건을 붙이면 기기에 따라 **OS가 자동으로** 맞는 리소스를 선택:

```
values/strings.xml          ← 기본 (영어)
values-ko/strings.xml       ← 한국어 폰 → 자동 적용
values-ja/strings.xml       ← 일본어 폰 → 자동 적용

drawable-hdpi/              ← 저해상도 기기용
drawable-xxhdpi/            ← 고해상도 기기용

layout/                     ← 기본 레이아웃
layout-sw600dp/             ← 태블릿용 → 자동 전환
```

### 왜 이렇게 설계했나?

- Android는 오픈소스 → 수백 종 기기 (화면 크기, 해상도, 언어 전부 다름)
- 리소스를 분리해두면 코드 수정 없이 기기별 대응 가능
- **Android Framework(OS 레벨)**이 qualifier 규칙에 따라 자동 선택
- 컨벤션 기반 설계: 폴더 이름 규칙만 따르면 시스템이 처리


<br />

---

# 1.3 Activity와 생명주기

## Activity란?

- iOS의 **UIViewController + AppDelegate**에 대응
- 화면 하나를 담당하면서, 앱의 진입점 역할도 겸함
- AndroidManifest.xml에 시작 Activity를 등록 → 시스템이 직접 실행

```
iOS:      AppDelegate → SceneDelegate → UIViewController
Android:  시스템이 직접 → Activity 실행
```

## 생명주기

```
onCreate   → 생성됨 (viewDidLoad)
onStart    → 화면에 보이기 시작
onResume   → 사용자와 상호작용 가능 (viewDidAppear)
onPause    → 상호작용 불가, 부분 가려짐 (viewWillDisappear)
onStop     → 완전히 안 보임 (viewDidDisappear)
onDestroy  → 소멸
```

## 화면 회전 = Activity 재생성 (핵심!)

### iOS vs Android

```
iOS:     ViewController 유지 → viewWillTransition 호출 → 끝
Android: onDestroy → 완전 소멸 → onCreate → 새로 생성!
```

### 왜 재생성하는가?

**리소스 qualifier 시스템** 때문!

```
가로 회전 시:
res/layout/       → res/layout-land/      (가로용 레이아웃)
res/values/dimens → res/values-land/dimens (가로용 크기값)
```

리소스가 통째로 바뀔 수 있으니 Activity를 새로 만드는 게 가장 확실한 방법.

### 연결 고리

```
1.1 하드웨어 파편화 → 1.2 리소스 qualifier → 1.3 Activity 재생성
```

iOS는 기기 몇 종류 → 레이아웃 조정으로 충분
Android는 수백 종 기기 → 아예 새로 그리는 전략

## 상태 보존 문제와 해결

Activity가 재생성되면 입력 중이던 데이터가 사라짐!

### 해결 1: onSaveInstanceState (레거시)

```
onPause → onStop → onSaveInstanceState(저장!) → onDestroy
                          ↓
onCreate(복원!) → onStart → onResume
```

### 해결 2: ViewModel (모던) - Phase 2에서 학습

```
Activity 죽음 → ViewModel은 살아있음 → 새 Activity가 ViewModel 연결
```

ViewModel이 등장한 핵심 이유 = Configuration Change 시 상태 보존

<br />

---

# 1.4 Intent와 화면 전환

## Intent란?

시스템에게 보내는 **"요청서"**. Android에서는 Activity를 직접 생성하지 않고, 시스템에게 요청한다.

```
iOS:     내가 직접 ViewController를 만들어서 전달
Android: 시스템한테 Intent로 "이 Activity 실행해줘" 요청
```

## 두 종류의 Intent

### Explicit Intent (명시적) - 앱 내부

대상 Activity를 직접 지정:

```kotlin
val intent = Intent(this, DetailActivity::class.java)
intent.putExtra("memo_id", 42)        // key-value로 데이터 전달
intent.putExtra("memo_title", "제목")
startActivity(intent)

// 받는 쪽
val id = intent.getIntExtra("memo_id", 0)
val title = intent.getStringExtra("memo_title")
```

### Implicit Intent (암시적) - 다른 앱 호출

"행위"만 지정, 누가 할지는 시스템이 결정:

```kotlin
val intent = Intent(MediaStore.ACTION_IMAGE_CAPTURE)  // "사진 찍어줘!"
// → 시스템이 가능한 앱들을 찾아서 사용자에게 선택하게 함
```

```
"사진 찍어줘" → 기본 카메라, 필터 카메라, B612... → 사용자 선택
"URL 열어줘" → Chrome, Samsung Browser, Firefox... → 사용자 선택
```

## iOS 비교

| | Explicit (명시적) | Implicit (암시적) |
|---|---|---|
| 대상 | Activity 직접 지정 | **행위**만 지정 |
| 용도 | 앱 내부 화면 전환 | 다른 앱 기능 호출 |
| iOS 비교 | `pushViewController` | `UIApplication.shared.open` |

## 데이터 전달 방식 비교

```swift
// iOS: 타입 안전한 프로퍼티 직접 할당
detailVC.memoId = 42
detailVC.memoTitle = "제목"
```

```kotlin
// Android: 문자열 key → 오타 위험!
intent.putExtra("memo_id", 42)
intent.getIntExtra("memoId", 0)  // key 오타 → 0 반환, 크래시 안 남 → 더 위험
```

## 발전 과정

```
레거시: Intent + putExtra (문자열 key) → 오타 위험
  ↓
개선:  Safe Args (Navigation Component) → 타입 안전
  ↓
모던:  Compose Navigation → type-safe route (Phase 2)
```

<br />

---

# 1.5 XML 레이아웃 기초

## UI 구성 방식 비교

| iOS | Android | 방식 |
|---|---|---|
| Storyboard/XIB | XML 레이아웃 | 파일로 UI 정의 |
| UIKit 코드 | 코드로 View 생성 | 코드로 직접 |
| SwiftUI | Jetpack Compose | 선언형 |

## 크기 지정

```
match_parent  → 부모 크기에 맞춤 (iOS: leading+trailing = 0)
wrap_content  → 내용물 크기에 맞춤 (iOS: intrinsicContentSize)
```

## 주요 레이아웃 3가지

### LinearLayout → UIStackView

세로/가로 순서대로 배치:

```xml
<LinearLayout android:orientation="vertical">
    <TextView />   <!-- 위 -->
    <Button />     <!-- 아래 -->
</LinearLayout>
```

### FrameLayout → UIView (단순)

자식 뷰를 겹쳐놓기. 하나만 놓거나 겹칠 때 사용.

### ConstraintLayout → Auto Layout (실무 표준!)

constraint 기반 자유 배치:

```xml
<ConstraintLayout>
    <TextView
        android:id="@+id/title"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent" />
    <Button
        app:layout_constraintTop_toBottomOf="@id/title"
        app:layout_constraintStart_toStartOf="parent" />
</ConstraintLayout>
```

| iOS Auto Layout | Android ConstraintLayout |
|---|---|
| `topAnchor` | `constraintTop_to...` |
| `leadingAnchor` | `constraintStart_to...` |
| `trailingAnchor` | `constraintEnd_to...` |
| `bottomAnchor` | `constraintBottom_to...` |

## ConstraintLayout이 실무 표준인 이유

```xml
<!-- LinearLayout 중첩 → 성능 나빠짐 -->
<LinearLayout>              <!-- 1단계 -->
  <LinearLayout>            <!-- 2단계 -->
    <LinearLayout>          <!-- 3단계... -->
    </LinearLayout>
  </LinearLayout>
</LinearLayout>

<!-- ConstraintLayout → flat하게 한 계층으로 해결 -->
<ConstraintLayout>          <!-- 1단계에서 다 해결! -->
  <View A />
  <View B />
  <View C />
</ConstraintLayout>
```

- 중첩이 깊어지면 렌더링 성능 저하
- ConstraintLayout은 한 계층(flat)으로 복잡한 UI 구성 가능
- iOS는 Auto Layout이 UIView에 내장 → 이런 고민이 적음
- Compose(Phase 2)에서는 이 문제가 많이 해소됨
