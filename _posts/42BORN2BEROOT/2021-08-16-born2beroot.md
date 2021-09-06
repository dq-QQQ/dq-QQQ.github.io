---
title: Born2beroot
date: 2021-08-16
excerpt: "VirtualBox를 이용해서 데비안 리눅스를 설치하고 나만의 리눅스 환경을 만들어보자:)"
categories:
- 42_BORN2BEROOT
tags:
- 42seoul
---


<br />
<br />

---

# 개요

---

본투비루트 과제는 간단하게 가상환경에서 특정 조건에 맞게 리눅스를 설치하고 환경설정을 해주는 것이다.
여기서 사용하는 가상환경은 Oracle사의 VirtualBox를 이용하며 설치할 리눅스 종류는 Debian이다.

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/129500999-36347c74-707f-49d2-8687-90de257d4843.png">
		<img src="https://user-images.githubusercontent.com/79088896/129500999-36347c74-707f-49d2-8687-90de257d4843.png"  width="400px;">
	</a>
</figure>

<br />
<br />



# BORN2BEROOT 프로젝트 요구사항 분석

## 프로젝트의 개요
Oracle사의 VirtualBox을 이용하여 가상환경을 구축하고 Debian Linux를 프로젝트에서 요구하는 설정값에 따라서 설치합니다.

## 프로젝트의 목표

가상환경에 대해 알아보고 리눅스 운영체제가 무엇인지 공부하는 것입니다.

그러한 환경에서 리눅스를 설치해봄에 따라 리눅스에 대한 이해와 운영체제에 대한 이해를 하는 것입니다.

## 프로젝트의 요구사항

* 사용가능한 가상환경은 VirtualBox와 UTM인데 VirtualBox의 사용이 불가능할 때의 대체재로 UTM을 선택한다.

* 사용가능한 리눅스 운영체제는 CentOS와 Debian인데 Debian의 설치를 권하고 있다.

* * 이번 과제에서는 그래픽 인터페이스는 사용하지 않으므로 리눅스 서버를 설치하고 셋업할 때 최소한의 기능들만 설치해야한다.

* LVM을 이용해서 최소 2개의 암호화된 파티션들을 만들어야한다.

아래의 그림과 같이 파티션들을 분할하면 된다.

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/129502444-40060166-722e-477b-92c9-84f01bf611f4.png">
		<img src="https://user-images.githubusercontent.com/79088896/129502444-40060166-722e-477b-92c9-84f01bf611f4.png"  width="600px;">
	</a>
</figure>

<br />
<br />

* SSH 기능은 4242 포트에서만 작동되야한다. 보안 문제 때문에 루트에는 SSH 연결을 허용하면 안된다.

* UFW 방화벽을 구성해야하고 4242 포트만 열려있어야한다. 방화벽은 가상머신이 작동될 때 활성화 되어야한다.

* 가상머신의 호스트네임은 42로 끝나야하며 평가 중에 수정할 것이다.

* 프로젝트에서 요구하는 비밀번호 정책을 구현하고 이 정책에 따라 sudo를 만들어야한다.

* 루트 사용자 외에 사용자 이름으로 로그인한 사용자가 있어야 하며 이 유저는 user42와 sudo그룹에 속하게 만들어야한다.

* 환경설정을 세팅한 후에는 루트 계정을 포함하여 모든 계정의 비밀번호를 바꿔야한다.

* 프로젝트에서 요구하는 조건에 따라서 sudo 그룹의 환경설정을 세팅해줘야한다.

* monitoring.sh라는 이름의 스크립ㄴ트 파일을 만들어야 한다.

* 서버가 시작할 때 스크립트는 아래그림과 같이 가상환경 관련 정보를 10분마다 아래에 표시해야한다. 
  배너는 옵션이며 어떤 에러도 나서는 안된다.

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/129503851-1d6ef13f-ac5a-4a20-944c-6b486614eb2b.png">
		<img src="https://user-images.githubusercontent.com/79088896/129503851-1d6ef13f-ac5a-4a20-944c-6b486614eb2b.png"  width="600px;">
	</a>
</figure>

<br />
<br />

---

# 가상머신

---

가상머신의 기본 개념은 단일 컴퓨터의 하드웨어를 여러 가지 실행 환경으로 추상화하여 개별 환경이 자신의 개인용 컴퓨터에서 실행되고 있다는 착각을 불러일으키는 것이다. 

각 시스템들은 자신이 네이티브 운영체제이고 모든 권한이 있다고 생각한다.


<br />
<br />

---

## 가상머신의 구조

---


<figure>
	<a href="https://user-images.githubusercontent.com/79088896/130194101-92995cea-4d8b-40cf-8cdc-9c209b62405e.jpeg">
		<img src="https://user-images.githubusercontent.com/79088896/130194101-92995cea-4d8b-40cf-8cdc-9c209b62405e.jpeg"  width="600px;">
	</a>
</figure>

<br />
<br />

가상 머신의 구현은 여러 구성요소를 포함한다.

`호스트`  : 가상 머신을 실행하는 기본 하드웨어 시스템

`가상 머신 관리자` : VMM 또는 하이퍼바이저라고 불리며 호스트와 동일한 인터페이스를 제공하여 가상 머신을 생성하고 실행한다.

`커널`: 운영 체제(OS)의 주요 구성 요소이며 컴퓨터 하드웨어와 프로세스를 잇는 핵심 인터페이스이다. 메모리 관리, 프로세스 관리, 장치 드라이버, 시스템 호출 및 보안의 역할을 한다.

`게스트` : 호스트의 가상 복사본이 제공되는 대상(운영체제)


<br />
<br />


---

## 가상머신의 종류

---

가상 시스템을 생성할 때 생성자는 VMM에 특정 매개 변수를 제공한다. 이러한 매개 변수에는 일반적으로 VMM이 고려해야할 CPU의 수, 메모리 크기, 네트워크, 저장장치 세부 사항이 포함된다. VMM은 이러한 매개 변수를 사용하여 가상 머신을 생성한다.

---

### 유형 0 하이퍼바이저

---

펌웨어를 통해 가상 머신 생성 및 관리를 지원하는 하드웨어 기반 VMM

이 유형은 실제의 하드웨어 실행에 매우 가까우며 각각의 게스트 운영체제는 하드웨어 부분집합을 가진 네이티브 운영체제라고 할 수 있다.
이 유형의 예시로는 IBM LPAR, Oracle LDOM이 있다.

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/130199598-73ba2dc6-eac9-4641-b1b4-33ee9b197212.jpeg">
		<img src="https://user-images.githubusercontent.com/79088896/130199598-73ba2dc6-eac9-4641-b1b4-33ee9b197212.jpeg"  width="600px;">
	</a>
</figure>

<br />
<br />



---

### 유형 1 하이퍼바이저

---

가상화를 제공하기 위해 구축된 운영체제와 유사한 소프트웨어
이 유형은 커널모드에서 실행되며 게스트 가상 머신을 생성, 실행 및 관리하는 데 필요한 환경과 기능을 제공한다.
각 게스트는 운영체제, 장치드라이버, 응용 프로그램등 완전한 네이티브 시스템과 같은 소프트웨어를 모두 포함한다.
VMware ESX, Joyent SmartOS, Citrix XenServer이 유형 1 하이퍼바이저에 속한다. 

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/130202114-e484d646-6980-41f8-9b66-dbeeb1c7d6de.jpeg">
		<img src="https://user-images.githubusercontent.com/79088896/130202114-e484d646-6980-41f8-9b66-dbeeb1c7d6de.jpeg"  width="600px;">
	</a>
</figure>

<br />
<br />

---

### 유형 2 하이퍼바이저

---

표준 운영체제에서 실행되지만 게스트 운영체제에 VMM 기능을 제공하는 응용 프로그램
이 유형의 하이퍼바이저는 다른 운영체제에서 실행되는 응용 프로그램으로 가상화가 되고 있음을 모른다. 호스트의 지원이 없으므로 프로세스 단계에서 모든 가상화 활동을 수행한다.
이 유형의 예시로는 VMware Workstation, VirtualBox, Parallels 등이 있다.

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/130201799-f75b00af-4e4f-4f50-be2a-3468d0ec1fec.jpeg">
		<img src="https://user-images.githubusercontent.com/79088896/130201799-f75b00af-4e4f-4f50-be2a-3468d0ec1fec.jpeg"  width="600px;">
	</a>
</figure>

<br />
<br />


