---
title: 정보처리기사 요약
categories: 
  - certification
excerpt: "정보처리기사의 주요 개념을 요약해봤다:)"
date: 2022-04-27
tags:
- certification
- 정보처리기사
---

# 개요

시나공 정보처리기사 실기 책을 기반으로 한 개념정리

<br />
<br />

---

# 1장-요구사항 확인

---

<br />

## 소프트웨어 생명주기

---

* 폭포수 모형
* 프로토타입 모형
* 나선형 모형
* 애자일 모형

<br />

---

## 폭포수 모형

---

각 단계를 확실히 끝내고 다음 단계를 진행


<br />

---

## 프로토타입 모형

---

개발될 소프트웨어의 견본품을 만들어 최종 결과물을 예측

<br />

---

## 나선형 모형

---

여러번의 소프트웨어 개발과정을 거쳐 점진적으로 개발

`계획수립` -> `위험 분석` -> `개발 및 검증` -> `고객 평가`

<br />

---

## 애자일 모형

---

고객의 요구사항 변화에 유연하게 대응할 수 있도록 일정한 주기를 반복하면서 개발

폭포수와 대조적

<br />

---

### 애자일 핵심가치

---

* 프로세스와 도구보다 개인과의 상호작용 중시
* 문서보다 실행되는 소프트웨어 중시
* 계약 협상보다는 고객과 협업 중시
* 계획을 따르기보다 변화에 반응 중시

<br />

---

## 스크럼

---

팀이 중심이 되어 개발의 효율성을 높이는 기법

<br />

---

## XP(eXtreme Programming)

---

고객의 요구사항에 유연하게 대응하기 위해 고객의 참여와 개발과정의 반복을 통해 생산성을 향상시키는 기법

<br />

---

### XP의 5가지 핵심가치

---

* 의사소통
* 단순성
* 용기
* 존중
* 피드백 

<br />

---

### XP의 12가지 실천방법

---

* pair Programming
* collective ownership
* test-driven development
* whole team
* continuous integration
* refactoring
* small releases
* planning game
* design improvement
* coding standards
* simple design
* system metaphor
* sustainable pace

<br />

---

## 운영체제

---

컴퓨터 자원을 효율적으로 관리하고, 사용자가 컴퓨터를 편리하게 사용할 수 있게 해주는 소프트웨어

<br />

---

### 고려사항

---

* 가용성
* 성능
* 기술지원
* 주변기기
* 구축비용

<br />

---

## DBMS

---

사용자와 DB 사이에서 정보를 생성해주고 DB를 관리해주는 소프트웨어

<br />

---

### 고려사항

---

* 가용성
* 성능
* 기술 지원
* 상호 호환성
* 구축 비용

<br />

---

## 웹 어플리케이션 서버(WAS)

---

동적인 컨텐츠를 처리하기 위해 사용되는 미들웨어

<br />

---

## 요구사항

---

소프트웨어가 어떤 문제를 해결하기 위해 제공하는 서비스에 대한 설명과 운영되는데 필요한 제약조건

<br />

---

### 요구사항 유형

---

* 기능 요구사항
* 비기능 요구사항
* 사용자 요구사항
* 시스템 요구사항

<br />

---

## 요구사항 개발 프로세스

---

`도출` -> `분석` -> `명세` -> `확인`

<br />

---

## 요구사항 분석

---

자료흐름도

자료사전

<br />

<figure>
	<a href="https://user-images.githubusercontent.com/79088896/165488949-614706a1-17e9-4ed9-a133-ff715938130b.jpeg">
		<img src="https://user-images.githubusercontent.com/79088896/165488949-614706a1-17e9-4ed9-a133-ff715938130b.jpeg" class="w8" />
	</a>
</figure>


<br />

---

## UML

---

시스템 개발 과정에서 의사소통이 원활하게 이루어지도록 표준화한 객체지향 모델링 언어

<br />

---

## UML 구성 요소

---

* 사물
* 관계
* 다이어그램

<br />

---

## UML 관계

---

사물과 사물 사이의 연관성을 표현

* 연관(Association) : 서로 관련이 있는 관계 (숫자써있으면)
* 집합(Aggregation) : 서로 독립적인 포함관계 (마름모)
* 포함(Composition) : 서로 독립되지 않은 포함관계 (색칠된 마름모)
* 일반화(Generalization) : 일반적이거나 구체적인 관계 (선과 삼각형 화살표 위 아래로)
* 의존(Dependency) : 서로에게 영향을 줄때면 연관을 유지하는 관계 (점선 , 화살표)
* 실체화(Realization) : 할 수 있거나 해야하는 기능 (점선과 삼각형 화살표 위 아래로)

<br />

---

## UML 다이어그램

---

사물과 관계를 도형으로 표현한 것

<br />

---

## 구조적 다이어그램

---

* 클래스 : 클래스 관계
* 객체 : 객체와 객체들의 관계, 럼바우 객체 모델링에 활용
* 컴포넌트 : 컴포넌트 관계 (구현단계에서 사용)
* 배치 : 물리적 요소들의 위치 (구현단계에서 사용)
* 복합체 구조 : 복합 구조
* 패키지 : 모델 요소들을 그룹화한 패키지들의 관계

<br />

---

## 행위 다이어그램

---

* 유스케이스 : 사용자의 요구
* 시퀀스 : 상호작용하는 시스템이나 객체들이 주고받는 메시지
* 커뮤니케이션 : 동작에 참여하는 객체들간의 연관관계
* 상태 : 상태 변화, 럼바우 동적 모델링에서 사용
* 활동 : 처리의 흐름을 순서에 따라 표현
* 상호작용 개요 : 상호작용
* 타이밍 : 객체상태변화와 시간제약을 명시적으로 표현

<br />

---

## 스테레오 타입

---

기본 기능외에 추가적인 기능을 표현하는 것

`<< >>`


<br />

---

## 소프트웨어 재사용

---

이미 개발되어 인정받은 소프트웨어를 다른 소프트웨어 개발이나 유지에 사용하는 것

* 합성 중심 : 블록을 만들어서 끼워맞추는 것
* 생성 중심 : 명세를 구체화하여 만드는 것

<br />

---

## 소프트웨어 재공학

---

기존 시스템을 이용하여 나은 시스템을 구축하고, 새로운 기능을 추가해서 성능을 향상시키는 것

<br />

---

## CASE

---

Computer Aided Software Engineering

소프트웨어 개발 과정에서 사용되는 과정을 컴퓨터와 도구를 사용하여 자동화 하는 것

<br />

---

## 하향식 비용 산정 기법

---

과거의 경험을 바탕으로 개발자들이 회의를 통해 비용을 산정하는 기법

<br />

---

## 델파이 기법

---

많은 전문가의 의견을 종합하여 산정하는 기법

<br />

---

## 상향식 비용 산정 기법

---

세부적인 작업 단위별로 비용을 산정한 후 집계하여 전체 비용을 산정하는 기법

<br />

---

## LOC

---

* 노력 = 기간 X 인원 = LOC / 1인당 월평균 라인 수
* 비용 = 노력 X 1인당 인건비
* 기간 = 노력 / 인원
* 생산성 = LOC / 노력

<br />

---

## 수학적 산정 기법

---

상향식 비용 산정 기법

* COCOMO
* Putnam
* 기능 점수 모형

<br />

---

## COCOMO 모형

---

LOC에 의한 비용 산정기법

<br />

---

## COCOMO 개발 유형

---

* 조직형(organic) : 중.소 규모의 소프트웨어, 5만 라인 이하
* 반분리형(Semi-Detached Mode) : 중간 규모의 소프트웨어, 30만 라인 이하
* 내장형(Embedded Mode) : 대규모의 소프트웨어, 30만 라인 이상

<br />

---

## Putnam 모형

---

소프트웨어 생명 주기의 전 과정 동안에 사용될 노력의 분포를 예상하는 모형

Rayleigh-Norden 곡선의 노력분포도를 기반으로 함


<br />

---

## 기능 점수 모형

---

소프트웨어의 기능을 증대시키는 요인별로 기능 점수를 구한 후 비용을 산정하는 기법

<br />

---

## 소프트웨어 개발 표준

---

소프트웨어 개발 단계에서 수행하는 품질 관리에 사용되는 국제 표준

* ISO/IEC 12207
* CMMI
* SPICE

<br />

---

## ISO/IEC 12207

---

ISO에서 만든 표준 소프트웨어 생명 주기 프로세스

<br />

---

## CMMI

---

소프트웨어 개발 조직의 업무능력 및 성숙도를 평가하는 모델

`초기` -> `관리` -> `정의` -> `정량적 관리` -> `최적화`


<br />

---

## SPICE

---

소프트웨어의 품질 및 생산성 향상을 위해 소프트웨어 프로세스를 평가 및 개선하는 국제 표준

`불완전` -> `수행` -> `관리` -> `확립` -> `예측` -> `최적화`


<br />

---

## 소프트웨어 개발 프레임워크

---

소프트웨어 개발에 공통적으로 사용되는 구성요소와 아키텍쳐를 일반화하여 제공해주는 반제품형태의 소프트웨어


<br />

---

### 소프트웨어 개발 프레임워크 특징

---

* 모듈화 
* 재사용성 
* 확장성
* 제어의 역흐름
