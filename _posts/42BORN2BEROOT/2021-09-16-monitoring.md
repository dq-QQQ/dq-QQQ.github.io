---
title: 리눅스 모니터링 스크립트
date: 2021-09-16
excerpt: "리눅스의 모니터링 스크립트를 만들어보자:)"
categories:
- 42_BORN2BEROOT
tags:
- 42seoul
- monitoring
---


<br />
<br />

---

# 개요

---

리눅스의 상태를 모니터링하는 스크립트를 만들어보겠다.



<br />
<br />

---

# cron

---

백그라운드에서 돌면서 미리 스케줄된 명령에 따라 프로그램

소프트웨어 유틸리티 cron은 시간 기반 잡 스케줄러이다.

명령을 고정된 시간, 날짜, 간격에 주기적으로 실행할 수 있도록 스케줄링하기 위해 cron을 사용한다.

crontab 파일에 따라서 작동한다.

## crontab

분 시 일 월 요일 실행할 명령어

<br />
<br />

---

# monitoring.sh

---

## The architecture of your operating system and its kernel version.

`uname -a`

시스템의
