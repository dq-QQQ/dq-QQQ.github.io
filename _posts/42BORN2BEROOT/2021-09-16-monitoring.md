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

시스템의 모든 정보 출력

<br />

## The number of physical processors.

`grep  "physical id" /proc/cpuinfo | uniq | wc -l`

"physical id를 /proc/cpuinfo 경로에서 중복되는것 제외한 라인 수를 검색 

물리적인 프로세서는 중복될 수 없다.

<br />

## The number of virtual processors.

grep -c processor /proc/cpuinfo

/proc/cpuinfo 에서 processor가 나타내는 문자열 검색

논리 cpu는 하이퍼 스레딩이나 다중 코어때문에 여러개가 가능하다. 따라서 중복 제외 없이 processor의 수만 나타내면된다.

<br />

## The current available RAM on your server and its utilization rate as a percentage.

`free -m |grep Mem |awk '{printf "%d/%dMB (%.2f%%)\n", $3, $2, $3/$2 *100}'`

free 명령어를 이용해서 시스템에서 메모리 상태에 대해서 출력

Mem 부분만 검색해서 특정 문자열의 패턴을 검색하거나 처리하는 awk 명령어를 이용해서 출력

.2는 소수점 두자리까지만 출력하라는 의미

<br />

## The current available memory on your server and its utilization rate as a percentage.

`df -Bm |grep /dev/mapper/ | awk '{usedisk+=$3} END {printf "%d/", usedisk}' | tr -d '\n'`

디스크 
