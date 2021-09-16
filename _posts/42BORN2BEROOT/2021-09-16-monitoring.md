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

`df -Bg |grep /dev/mapper/ | awk '{fulldisk += $2} END {printf "%dGb (", fulldisk}' | tr -d '\n'`

`df -Bm |grep /dev/mapper/ | awk '{fulldisk += $2} {usedisk += $3} END {printf "%d%%)\n", usedisk/fulldisk * 100}'
`

파일 시스템 디스크 사용 현황을 보고하는 명령어인 df를 이용한다. -B옵션은 사이즈를 선택한다는 것이다. m이 붙으면 메가바이트 g가 붙으면 기가바이트이다. 

내 서버의 파일시스템은 /dev/mapper/로 시작하기 때문에 검색

변수이용해서 다 더한다. 

tr -d 옵션으로 개행을 삭제한다.


<br />

## The current utilization rate of your processors as a percentage.

grep 'cpu ' /proc/stat |awk '{use=($2 + $4)/($2+$4+$5) * 100} END {print use "%"}'


user : 유저(user) 모드에서 실행되는 normal 프로세스

system : 커널(kernel) 모드에서 실행되는 프로세스

nice : 유저(user) 모드에서 실행되는 nice 프로세스 nice는 우선 순위를 가진 utility나, 쉘 스크립트를 호출하는데 사용

idle : I/O 완료가 아닌 대기 시간

iowait : I/O가 완료될 때까지 기다리는 시간

irq : 하드웨어 IRQ(Interrupt request) 인터럽트(interrupt) 

softirq: 소프트웨어 IRQ(Interrupt request) 인터럽트(interrupt) 

steal : involuntary wait

guest : 실행 중인 normal guest

guest_nice : 실행 중인 nice guest

유저모드 cpu 사용률 = user + nice / user + nice + idle  * 100

<br />

## The date and time of the last reboot.

`uptime -s`

uptime -s를 이용해서 시스템이 언제부터 작동되었는지 출력

<br />

## Whether LVM is active or not.

`if [ "$(lsblk | grep lvm |wc -l)" -eq 0]; then printf "no\n"; else printf "yes\n"; fi`

yes or no 이므로 lsblk |grep lvm |wc -l 으로 lvm을 포함하는 문자열의 수를 검색하고 0이랑 비교해서 조건문으로 같으면 no 다르면 yes 출력

<br />

## The number of active connections

`ss | grep -i tcp | wc -l | tr -d '\n'`

소켓을 조사하는 명령어 즉 네트워크 상태를 확인하는 명령어

<br />

## The number of users using the server.

`who |wc -l`

로그인되어있는 유저 수를 나타내는 명령어


<br />

## The IPv4 address of your server and its MAC (Media Access Control) address.

`hostname -I |tr -d '\n'`

hostname I 옵션으로 호스트의 주소 출력

`ip link show | grep ether |awk '{print $2}' |sed -n '1p'| tr -d '\n'`


<br />

## The number of commands executed with the sudo program.

`cat /var/log/sudo/sudo.log |grep 'COMMAND=' |wc -l |tr -d '\n'`

