---
title: Born2beroot
date: 2021-08-16
excerpt: "VirtualBox를 이용해서 데비안 리눅스를 설치하고 나만의 리눅스 환경을 만들어보자:)"
categories:
- 42seoul
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
