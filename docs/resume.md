# 이력서

## 정수환 | Java Backend Engineer

**Java · Spring · API Integration · Authentication/Authorization · Legacy Modernization**

- 경력: 2019.06 ~ 현재 (7년+)
- 소속: 콘텐트리중앙 · 미디어개발팀
- 희망 직무: Java/Spring 백엔드 개발
- 연락처: 2004ppo@naver.com
- GitHub: https://github.com/hwany0/portfolio

## 프로필

고객관리·수금·결제·멤버십 등 업무 시스템을 개발하고 운영해 온 Java 개발자입니다. Spring 기반 API와 외부 시스템 연동을 중심으로 인증·인가, 배치 처리, 데이터 정합성, 장애 분석 및 레거시 전환을 경험했습니다. 운영 중 발생한 문제를 재현 가능한 조건으로 좁혀 원인을 분석하고, 기존 업무 흐름을 고려해 공통 구조와 처리 절차를 개선하는 데 강점이 있습니다.

최근에는 Java 17/Spring Boot 3.5.x 기반 전환 프로젝트에서 Gradle/JAR 구조, 공통 API 응답 및 예외 처리, AOP 기반 인가 구조를 정비하고 있습니다. 또한 음성 인식과 LLM을 활용해 업무 메뉴 탐색을 줄이는 Direct Routing 흐름을 설계했습니다.

## 핵심 역량

- **백엔드 및 외부 연동:** Java/Spring API, 결제·수금 API, 배치 처리, 상태 조회 및 후속 확인 흐름
- **인증·인가:** 세션·토큰 기반 인증, Redis 토큰 재발급, PASS 본인인증, TOTP MFA, 사용자/매체 권한 검증
- **데이터 정합성 및 장애 분석:** 결제 상태 불일치, 대량 처리, 비표준 문자에 따른 직렬화 장애, 외부 API 응답 오류 분석
- **레거시 현대화:** Java 17/Spring Boot 전환 기반 구성, JSP→Thymeleaf 전환 구조 정비, eXBuilder XTM→JSP, PowerBuilder→.NET 전환 참여
- **운영 안정화:** 배치 처리 보완, Grafana/Prometheus 모니터링, IIS/ClickOnce 배포 이슈 대응
- **AI 기반 업무 UX:** vLLM/LLM 기반 메뉴·파라미터 추론, 필수값 재질문, 후보 추천, 권한 확인 및 비동기 로깅

## 주요 경력

### 콘텐트리중앙 | 미디어개발팀 | 풀스택 개발자
*2019.06 ~ 현재*

고객관리, 청구·수금·결제, 멤버십, 매체사 서비스의 개발과 운영을 담당했습니다. 백엔드 연동과 인증·보안, 레거시 전환, 배치 처리 및 운영 장애 분석을 수행했습니다.

## 대표 프로젝트

### 1. 옥외 광고 청약 시스템 SaaS 전환 및 공통 아키텍처 정비
*2026.09 ~ 진행 중*

- 기존 Java 8/Spring Framework 시스템을 Java 17/Spring Boot 3.5.x 기반으로 전환하는 기반 구성
- Maven/WAR 중심 구조를 Gradle/JAR 기반으로 정비
- JSP 화면의 Thymeleaf 전환을 위한 공통 렌더링 구조 및 화면 데이터 제공 방식 정비
- 공통 API 응답 DTO, 전역 예외 처리, 외부 설정 및 공통 Bean 구성 정비
- 조직·매체·사용자 그룹 권한을 구분하고 AOP 기반 공통 인가 구조 설계·적용 중

**기술:** Java 17, Spring Boot 3.5.x, Gradle, MyBatis, MSSQL, Thymeleaf

### 2. J-Mobile AI Direct Routing
*2025.09 ~ 2025.12*

- 음성 명령에서 업무 메뉴와 파라미터를 추론해 여러 단계의 메뉴 탐색 없이 업무 화면으로 이동하는 흐름 설계
- 필수 파라미터 누락 시 재질문하고, 메뉴별 파라미터 처리 및 추천 후보 생성을 분리
- DB 결과 검증, 사용자 권한 확인, 비동기 로그를 포함한 처리 흐름 구성

**기술:** Java, Spring Framework, JSP, vLLM API, Gemma-4, Speech Recognition

### 3. 방송 광고 관리 시스템 재구축 및 MFA
*2025.02 ~ 2025.12*

- eXBuilder XTM 기반 화면을 JSP로 전환
- SBUx/SBGrid 공통 UI 구조, Custom Tag 및 GridBuilder 정비
- 내부·외부 사용자 유형에 따른 TOTP 기반 MFA 인증 흐름 구현

**기술:** Java 8, Spring Framework 3.2.9, JSP, Oracle 11g, SBUx/SBGrid

### 4. HLL 통합 멤버십 사이트
*2023.06 ~ 2024.01*

- 매체사별 도메인 분리 환경에서 iframe/postMessage 기반 로그인 흐름 구현
- Redis 기반 토큰 재발급 및 PASS 본인인증 연동
- 외부 기프트샵 API와 포인트 적립·차감 처리 연동, MongoDB 이력과 RDB 데이터 정합성 고려

**기술:** Java 8, Spring Framework 5.1.7, MSSQL, MongoDB, Redis

### 5. 오픈지로 비대면 수금 서비스
*2022.12 ~ 2023.04*

- 외부 API를 통한 청구 생성, 납부 링크 발급, 알림톡 발송 및 수금 처리 흐름 구현
- 정기 배치와 주기적인 상태 조회를 통해 미확인 처리 결과를 확인하는 구조 구성
- 대량 API 호출 오류, 응답 불일치, 외부 연동 장애 등 운영 이슈 분석 및 개선

**기술:** Java 7, Spring Framework 3.1.0, MSSQL, REST API, Batch

### 6. 모바일 수금관리 시스템 재구축 및 고도화
*2019.08 ~ 2019.11 / 2021.01 ~ 2021.04*

- 유지보수가 어려워진 앱을 APP+WEB 하이브리드 구조로 재구축
- 고객 검색·수금·VOC 화면과 카드 결제 연동 구현
- 결제 요청·승인·최종 처리 상태를 분리하고 응답 누락 및 상태 불일치 대응 로직 보완
- 배달 현황, VOC 사진, 로그인 현황 및 Firebase FCM 공지 기능 추가

**기술:** Java 7, Spring Framework 4.2.1, JSP, MSSQL, WebView, Firebase FCM

## 기술 스택

- **Language:** Java, C#, JavaScript, SQL
- **Backend:** Spring Framework, Spring Boot, MyBatis, REST API
- **Database/Cache:** MSSQL, Oracle, MariaDB, MongoDB, Redis
- **Authentication/Security:** Session/Token, PASS, TOTP MFA, API-level access control
- **Integration/AI:** 결제·수금 API, 알림톡, Firebase FCM, vLLM API
- **Web/Legacy UI:** JSP, Thymeleaf, SBUx/SBGrid, WinForm
- **Operations:** WebToB, JEUS, WildFly, Tomcat, IIS, Grafana, Prometheus, Windows Exporter
- **Build/Version Control:** Maven, Gradle, GitLab

## 기타

- SQLD (한국데이터산업진흥원, 2023.12 취득)
- SaaS 전환 프로젝트는 진행 중이며, 완료된 범위와 설계·적용 중인 범위를 구분해 설명합니다.
- 정량 성과는 확인 가능한 자료가 없는 경우 임의로 기재하지 않았습니다.
