---
title: superclaude
date: 2026-04-02
excerpt: "superclaude 사용기"
categories:
- AI
tags:
- iOS-PRO
- Claude
- AI
---



<br />

---

# SuperClaude Commands

내가 지금 어떤 개발 작업 단계인가를 파악하고 알맞은 커맨드를 사용해야함

## 1순위 커맨드

-   /sc:implement : 단순 구현만해주는게 아니라 요구사항 분석 -> 구조 설계 -> 구현 -> 자체 검토의 워크플로우를 트리거, security-engineer가 같이 활성화됨
-   /sc:troubleshoot : 단순 디버깅만 해주는게 아니라 증상 -> 가설 수립 -> 원인 분석 -> 수정 방안의 워크플로우를 트리거, root-cause-analyst가 활성화되어 근본을 찾으려함
-   /sc:test : 단순 테스트 코드만 생성하는게 아니라 엣지 케이스와 경계 조건까지 체계적으로 커버함
-   /sc:explain : 생소한 코드를 잘 설명해줌 동작방식, 설계의도 패턴, 잠재적 문제점까지 설명해줌

<br />


## 2순위 커맨드

-   /sc:analyze : 코드나 아키텍쳐 전반을 분석함. 성능, 병목, 보안 취약점, 코드 냄새, 의존성 문제등을 알려줌
-   /sc:research : 기술비교나 최신동향을 종합적으로 해주는 딥 리서치 워크플로우

<br />

## 기획 & 설계

-   /sc:brainstorm : 아직 뭘 만들지 모를때 막연한 아이디어를 구체화할 때 사용, 잘 모르겠는데,,,이러면 루프를 트리거
-   /sc:design : 무엇이 확정된 다음 어떻게를 구체화할때 사용, 기술 아키텍처, 데이터 모델, api 명세를 만들수있음


<br />

## 구현

-   /sc:implement : 존재하지 않는 것을 만들때. 빈파일에서 완성된 코드까지 설계->구현->자체검증을 한번에 수행
-   /sc:build : 빌드 파이프라인을 실행.
-   /sc:improve : 이미 동작하는 코드를 더 좋게. 기능은 그대로 품질, 성능, 보안을 향상
    -   --safe : 외부 동작에 영향을 줄 수 있는 변경은 건너뛰고 가독성 같은 것만
    -   --interactive : 변경 하나하나를 직접 승인
    -   --validate : 변경 후 테스트 자동실행


<br />

## 테스트 & 품질

-   /sc:test : 미래의 버그를 방지 --type e2e같이 원하는 테스트
-   /sc:analyze : 현재 코드의 상태를 진단, 건강 검진같은 느낌, 분석 깊이는 --think같은것으로 
-   /sc:troubleshoot : 현재의 버그를 해결

<br />

## 코드 이해

-   둘다 코드를 이해하는 것은 같으나
-   /sc:explain : 실시간 설명으로 끝남
-   /sc:document : 문서로 남김, explain이 선행될 때 좋음


<br />

## 리팩토링

-   /sc:cleanup : 코드의 동작을 바꾸지 않고 미사용 코드, 중복선언등 불필요한것을 지움 --preview로 미리 보기 ㄱㄱ
-   /sc:reflect : 코드를 직접 바꾸지 않고 내가 맞는 방향인지 검증



<br />

## 오케스트라

지금까지의 커맨드는 모두 코드를 직접 건드림 그러나 오케스트라는 좀 더 큰 틀에서 프로젝트를 봄 지휘자를 만드는것이라고 봄

-   /sc:pm : 어디서부터 시작할지모를때. 막연한 요청을 brainstorm -> design -> workflow -> spawn -> task 파이프라인을 오케스트레이션
-   /sc:workflow : 설계가 끝나고 phase별 태스크 분해, 의존성 파악, 병렬 실행가능여부등 실제 구현계획 생성
-   /sc:spawn : phase를 task로 쪼갬
-   /sc:task : spawn이 만든 계획의 각 항목을 실행




<br />

---

# SuperClaude flag

-   엄청 많지만 자주쓰는거 위주로
-   --plan : 실행 계획, /build --plan 실행하기전에 빌드 단계를 확인해줘
-   --think : 다중파일 분석, 5개 이상의 파일 가져오기
-   --think-hard : 시스템 전체문제, 3개이상의 모듈에서 병목현상 발생 시
-   --ultrathink : 핵심 시스템 재설계, 복잡한 디버깅
-   --verbose : 상세하게
-   --delegate : 서브에이전트 활성화 files, folders, auto


<br />

---

# Agent

-   architect : 시스템 설계 및 아키텍쳐 계획
-   frontend : UI/UX 디자인 및 사용자 경험
-   scribe : 요구사항 문서화 및 사양 정의
-   backend : API 및 서비스 구현
-   security : 보안 구현 및 강화
-   qa : 테스트 전략 및 품질 보증
-   performance : 성능 테스트 및 최적화
-   analyzer : 버그 조사 및 근본 원인 분석
-   refactorer : 리팩토링
-   mentor : 선생님
-   devops : 배포 자동화 및 인프라