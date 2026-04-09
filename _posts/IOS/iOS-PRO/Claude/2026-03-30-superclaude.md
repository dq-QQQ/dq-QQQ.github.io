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

# SuperClaude란?

Claude Code의 기본 기능 위에 전문화된 워크플로우를 추가한 시스템:
- **전문 에이전트** 호출 (보안, 성능, 아키텍처 등)
- **복잡한 태스크 자동 분해** 및 위임
- **MCP 도구 통합** (Serena, context7, Playwright 등)
- **세션 컨텍스트 지속성** (save/load)

# 명령어 분류표

## 🏗️ 핵심 (Core)

| 명령어 | 기능 | 사용 시나리오 |
|--------|------|---------------|
| `/sc` | 커맨드 디스패처 | SuperClaude 진입점 |
| `/sc:help` | 모든 명령어 목록 | 명령어 찾기 |
| `/sc:recommend` | 최적 명령어 추천 | 어떤 명령어를 쓸지 모를 때 |
| `/sc:select-tool` | MCP 도구 선택 | 복잡도 기반 최적 도구 추천 |

## 📋 프로젝트 관리 (Management)

| 명령어 | 기능 | 사용 시나리오 |
|--------|------|---------------|
| `/sc:pm` | 프로젝트 매니저 에이전트 | 전체 워크플로우 조율 |
| `/sc:task` | 태스크 실행 + 위임 | 복잡한 멀티스텝 작업 |
| `/sc:spawn` | 태스크 분해 + 오케스트레이션 | 대규모 작업 병렬화 |
| `/sc:workflow` | PRD에서 워크플로우 생성 | 기능 구현 계획 |
| `/sc:estimate` | 개발 견적 | 작업 규모 추정 |

## 💻 개발 (Development)

| 명령어 | 기능 | 사용 시나리오 |
|--------|------|---------------|
| `/sc:implement` | 기능 구현 | 코드 작성 |
| `/sc:design` | 아키텍처/API 설계 | 시스템 설계 |
| `/sc:build` | 빌드/컴파일 | 빌드 오류 해결 |
| `/sc:test` | 테스트 + 커버리지 | 테스트 실행/분석 |
| `/sc:git` | 스마트 Git 작업 | 커밋/브랜치/PR |

## 🔍 분석 (Analysis)

| 명령어 | 기능 | 사용 시나리오 |
|--------|------|---------------|
| `/sc:analyze` | 코드 품질/보안/성능 분석 | 종합 코드 분석 |
| `/sc:improve` | 체계적 코드 개선 | 리팩토링 |
| `/sc:cleanup` | 데드코드 제거 | 코드 정리 |
| `/sc:troubleshoot` | 이슈 진단 | 버그 해결 |
| `/sc:explain` | 코드/개념 설명 | 이해가 필요할 때 |
| `/sc:reflect` | 태스크 검증 | 작업 결과 리뷰 |

## 📖 문서 (Documentation)

| 명령어 | 기능 | 사용 시나리오 |
|--------|------|---------------|
| `/sc:document` | 컴포넌트/API 문서 생성 | 특정 기능 문서화 |
| `/sc:index` | 프로젝트 지식 베이스 생성 | 종합 문서화 |
| `/sc:index-repo` | 레포지토리 인덱싱 | 94% 토큰 절감 인덱스 |

## 🧠 기획 (Planning)

| 명령어 | 기능 | 사용 시나리오 |
|--------|------|---------------|
| `/sc:brainstorm` | 소크라테스식 요구사항 발견 | 기획 초기 |
| `/sc:spec-panel` | 멀티 전문가 스펙 리뷰 | 사양서 검증 |
| `/sc:business-panel` | 비즈니스 전략 분석 | 사업 의사결정 |

## 🔧 유틸리티 (Utility)

| 명령어 | 기능 | 사용 시나리오 |
|--------|------|---------------|
| `/sc:research` | 웹 심층 리서치 | 기술 조사 |
| `/sc:save` | 세션 컨텍스트 저장 | 작업 중단 시 |
| `/sc:load` | 세션 컨텍스트 복원 | 작업 재개 시 |
| `/sc:agent` | 에이전트 직접 실행 | 커스텀 에이전트 |

# SuperClaude 활용 실전 패턴

## 기능 개발

### 패턴 1: 새 기능 구현 (풀 플로우)
```
/sc:brainstorm → /sc:design → /sc:workflow → /sc:implement → /sc:test → /sc:git
```
요구사항 발견 → 아키텍처 설계 → 구현 계획 → 코드 작성 → 테스트 → 커밋

### 패턴 2: 빠른 기능 추가 (간소화)
```
/sc:implement → /sc:test → /sc:git
```
명확한 요구사항이 이미 있을 때, 바로 구현

### 패턴 3: UI 중심 기능 구현
```
/sc:brainstorm → /sc:design → /sc:implement --magic → /sc:test --play → /sc:git
```
Magic MCP로 컴포넌트 생성 + Playwright로 브라우저 테스트

## 코드 품질

### 패턴 4: 코드 품질 개선
```
/sc:analyze → /sc:improve → /sc:cleanup → /sc:test → /sc:reflect
```
분석 → 개선 → 정리 → 테스트 → 결과 검증

### 패턴 5: 보안 감사
```
/sc:analyze --focus security → /sc:implement (fix) → /sc:test → /sc:document
```
보안 취약점 발견 → 패치 → 테스트 → 보안 문서화

### 패턴 6: 성능 최적화
```
/sc:analyze --focus performance → /sc:troubleshoot → /sc:improve → /sc:test → /sc:reflect
```
성능 병목 발견 → 원인 진단 → 최적화 → 테스트 → 검증

## 리팩토링

### 패턴 7: 대규모 리팩토링
```
/sc:analyze --ultrathink → /sc:workflow → /sc:spawn --delegate auto → /sc:test → /sc:git
```
전체 분석 → 단계별 계획 → 서브에이전트 병렬 실행 → 테스트 → 커밋

### 패턴 8: 모듈 단위 리팩토링
```
/sc:analyze --scope module → /sc:improve → /sc:test → /sc:git
```
특정 모듈만 집중 분석 후 개선

## 이슈 대응

### 패턴 9: 프로덕션 이슈 대응
```
/sc:troubleshoot --think-hard → /sc:implement --safe-mode → /sc:test → /sc:git
```
심층 진단 → 안전 모드로 수정 → 테스트 → 커밋

### 패턴 10: 원인 불명 버그 추적
```
/sc:troubleshoot --ultrathink → /sc:explain → /sc:implement (fix) → /sc:test → /sc:reflect
```
최대 깊이 분석 → 원인 설명 → 수정 → 테스트 → 수정 검증

## 기획/리서치

### 패턴 11: 기술 의사결정
```
/sc:research --depth deep → /sc:spec-panel --mode debate → /sc:design
```
기술 조사 → 전문가 패널 토론 → 최종 설계

### 패턴 12: 프로젝트 킥오프
```
/sc:brainstorm → /sc:spec-panel → /sc:estimate → /sc:workflow → /sc:design
```
요구사항 발견 → 스펙 검증 → 견적 → 구현 계획 → 설계

### 패턴 13: 비즈니스 분석
```
/sc:research → /sc:business-panel → /sc:document
```
시장/기술 조사 → 비즈니스 전문가 패널 분석 → 문서화

## 문서/온보딩

### 패턴 14: 프로젝트 문서화
```
/sc:index-repo → /sc:index → /sc:document
```
레포 인덱싱(94% 토큰 절감) → 지식 베이스 생성 → 상세 문서

### 패턴 15: 코드 이해 (온보딩)
```
/sc:index-repo → /sc:explain → /sc:analyze
```
프로젝트 구조 파악 → 핵심 코드 설명 → 품질/아키텍처 분석

## 세션 관리

### 패턴 16: 장기 작업 세션
```
/sc:load → (작업) → /sc:save → (다음 세션) → /sc:load → /sc:reflect
```
컨텍스트 복원 → 작업 → 저장 → 복원 → 진행 상황 검증



<br />

---

# 실전 사용 예시

## 코드 분석 및 개선
```bash
# 인증 모듈 보안 심층 분석
/sc:analyze --think-hard --focus security src/auth/

# 성능 개선 + 실행 전 검증
/sc:improve --focus performance --validate

# 레거시 모듈 정리
/sc:cleanup --scope module src/legacy/
```

## 기능 구현 (풀 플로우)
```bash
# 1. 요구사항 발견
/sc:brainstorm "사용자 대시보드 기능"

# 2. 아키텍처 설계
/sc:design --think-hard "대시보드 아키텍처"

# 3. UI 구현 (Magic MCP로 컴포넌트 생성)
/sc:implement --magic --validate "대시보드 UI 구현"

# 4. 테스트
/sc:test --scope module
```

## 대규모 리팩토링
```bash
# 프로젝트 전체 최대 깊이 분석
/sc:analyze --ultrathink --scope project

# 서브에이전트 5개 병렬로 리팩토링
/sc:spawn --delegate auto --concurrency 5 "인증 모듈 리팩토링"

# 프로젝트 전체 품질 테스트
/sc:test --scope project --focus quality
```

## 프로덕션 이슈 대응
```bash
# 이슈 원인 심층 진단
/sc:troubleshoot --think-hard "API 응답 지연 이슈"

# 시스템 전체 성능 분석
/sc:analyze --focus performance --scope system

# 안전 모드로 패치 (검증 포함)
/sc:implement --safe-mode --validate "성능 패치"
```

## 리서치 및 기획
```bash
# 기술 심층 조사
/sc:research --depth deep "OAuth 2.1 vs 2.0 차이점"

# 전문가 패널 스펙 리뷰 (비판 모드)
/sc:spec-panel --mode critique "인증 시스템 스펙"

# 작업량 추정
/sc:estimate --think "마이그레이션 작업량"
```

## 세션 관리
```bash
# 작업 중단 시 전체 컨텍스트 저장
/sc:save --type all

# 다음 세션에서 체크포인트 복원
/sc:load --type checkpoint
```

## 플래그 조합 팁

| 목적 | 플래그 조합 |
|------|------------|
| 분석 깊이 조절 | `--think` < `--think-hard` < `--ultrathink` |
| 프로덕션 안전 | `--safe-mode --validate` |
| 토큰 절약 | `--uc --token-efficient` (30-50% 절감) |
| 병렬 처리 | `--delegate auto --concurrency 5` |
| MCP 전체 활성화 | `--all-mcp` |
| MCP 없이 실행 | `--no-mcp` |
| 특정 도메인 집중 | `--focus [performance\|security\|quality\|architecture]` |
| 분석 범위 지정 | `--scope [file\|module\|project\|system]` |


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

# Agent (23개)

## 아키텍트

| 에이전트 | 역할 | 전문 분야 |
|----------|------|-----------|
| system-architect | 시스템 설계 | 확장성(10x 성장 대비), 컴포넌트 경계, 아키텍처 패턴 |
| backend-architect | 백엔드 설계 | API 설계, DB 아키텍처, 보안, 시스템 신뢰성 |
| frontend-architect | 프론트엔드 설계 | 접근성(WCAG 2.1), Core Web Vitals, 컴포넌트 아키텍처 |
| ios-architect | iOS 앱 설계 | Swift/SwiftUI/UIKit, MVVM/TCA, Core Data, Combine |
| android-architect | Android 앱 설계 | Kotlin/Jetpack Compose, MVVM/MVI, Room, Play Store |
| devops-architect | 인프라/배포 | CI/CD 파이프라인, IaC, 모니터링, 컨테이너 오케스트레이션 |

## 품질/보안

| 에이전트 | 역할 | 전문 분야 |
|----------|------|-----------|
| security-engineer | 보안 전문가 | OWASP Top 10, CWE 패턴, 위협 모델링, 컴플라이언스 |
| quality-engineer | QA 전문가 | 테스트 전략, 엣지케이스 탐지, 테스트 자동화, 품질 메트릭 |
| performance-engineer | 성능 전문가 | 프론트/백엔드 성능, 리소스 최적화, 병목 분석 |
| refactoring-expert | 리팩토링 전문가 | SOLID 원칙, 기술 부채 감소, 코드 단순화, 품질 메트릭 |

## 분석/리서치

| 에이전트 | 역할 | 전문 분야 |
|----------|------|-----------|
| root-cause-analyst | 근본 원인 분석 | 증거 수집, 가설 검증, 패턴 분석, 타임라인 조사 |
| deep-research-agent | 심층 리서치 | 적응형 계획, 멀티홉 추론, 자기성찰, 출처 인용 |
| deep-research | 정보 수집 | 정보 탐색 및 종합 |

## 프로젝트/교육

| 에이전트 | 역할 | 전문 분야 |
|----------|------|-----------|
| pm-agent | 프로젝트 매니저 | PDCA 사이클, 세션 관리, 자기개선, 패턴 라이브러리 |
| socratic-mentor | 소크라테스식 멘토 | 발견 학습, 전략적 질문, 디자인 패턴, 수준별 교육 |
| requirements-analyst | 요구사항 분석가 | 요구사항 도출, 수락 기준 정의, 스코프 관리 |
| technical-writer | 기술 문서 작성 | API 문서, 기술 문서 시스템, 문서 명확성 |
| learning-guide | 학습 가이드 | 학습 경로 설계, 교육 콘텐츠 |
| practice-creator | 연습 문제 생성 | 실습 과제, 퀴즈 생성 |

## 도메인/지원

| 에이전트 | 역할 | 전문 분야 |
|----------|------|-----------|
| python-expert | Python 전문가 | 프로덕션 코드, SOLID, 보안, 성능 최적화 |
| business-panel-experts | 비즈니스 패널 | 9인 전문가 (Christensen, Porter, Drucker, Godin 등) |
| self-review | 구현 검증 | 구현 후 검증, 품질 보증 |
| repo-index | 레포 인덱싱 | 레포지토리 구조 분석, 문서화 |