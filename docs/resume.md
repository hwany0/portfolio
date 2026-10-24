# 이력서

## 정수환 | Backend Engineer

**Java · Spring · API 연동 · 인증/인가 · 레거시 현대화**

- 경력: 2019.06 ~ 현재
- 현재 회사: 콘텐트리중앙 · 미디어개발팀
- 지원 직무: Java/Spring 백엔드 개발
- 기술 키워드: Java, Spring Framework, Spring Boot, MyBatis, MSSQL, Oracle, Redis, MongoDB, REST API, 인증/인가, 배치, 레거시 전환

## 프로필

고객관리·수금·결제 업무 시스템을 개발하고 운영해 온 개발자입니다. Java/Spring 기반 백엔드와 외부 API 연동을 중심으로 인증·인가, 데이터 정합성, 배치 처리, 장애 분석 및 레거시 현대화를 경험했습니다. 기존 시스템의 업무 흐름을 유지하면서 공통 구조를 정리하고, 운영 이슈를 재현·분석해 안정적인 개선 방안을 찾는 데 강점이 있습니다.

## 핵심 역량

- **백엔드 개발 및 연동:** Java/Spring 기반 업무 API, 외부 결제·수금 API, 상태 조회 및 배치 처리
- **인증·인가 및 보안:** 통합 멤버십 인증, Redis 토큰 재발급, PASS 본인인증, TOTP 기반 MFA, 사용자·매체 접근 권한 검증
- **레거시 현대화:** Java/Spring 기반 시스템 전환, Java 17/Spring Boot 3.5.x 전환 기반 구성, JSP→Thymeleaf 전환 구조 정비, PowerBuilder→.NET 전환 참여
- **운영 안정화:** 외부 API 오류 및 응답 불일치 분석, 결제 상태 정합성 보완, 배치 처리 개선, 서버 모니터링
- **업무 UX 개선:** 음성 인식과 LLM/vLLM을 활용한 업무 메뉴 Direct Routing 구조 설계

## 주요 경력

### 콘텐트리중앙 | 풀스택 개발자
*2019.06 ~ 현재 · 미디어개발팀*

고객관리, 구독 청구, 수금·결제, 멤버십, 매체사 서비스의 개발과 운영을 담당했습니다. 백엔드 연동과 인증·보안, 레거시 전환, 공통 UI/설정, 배치 및 장애 대응을 수행했습니다.

## 주요 프로젝트

### 옥외 광고 청약 시스템 SaaS 전환 및 공통 아키텍처 정비
*2026.09 ~ 진행 중*

- Java 8/Spring Framework 기반 시스템을 Java 17/Spring Boot 3.5.x로 전환하는 기반 구성
- Maven/WAR 중심 구조에서 Gradle/JAR 기반 구조로 정비
- JSP 화면의 Thymeleaf 전환과 공통 설정·API 응답 DTO·전역 예외 처리 구조 정비
- 조직·매체·사용자 그룹 권한을 구분하고 AOP 기반 공통 인가 구조 설계·적용 중

**기술:** Java 17, Spring Boot 3.5.x, Gradle, MyBatis, MSSQL, Thymeleaf

### J-Mobile AI Direct Routing
*2025.09 ~ 2025.12*

- 음성 명령에서 업무 메뉴와 파라미터를 추론해 사용자가 메뉴를 단계적으로 탐색하지 않고 업무에 진입할 수 있는 흐름 설계
- 필수 파라미터 누락 시 재질문, 메뉴별 파라미터 해석, 후보 추천 및 DB 검증 흐름 구성
- 사용자 권한 검증과 비동기 로그 기록 구조 설계

**기술:** Java, Spring Framework, JSP, vLLM API, 음성 인식

### HLL 통합 멤버십 사이트
*2023.06 ~ 2024.01*

- 매체사별 도메인 분리 환경에서 iframe/postMessage 기반 로그인 상태 유지 구조 구현
- Redis 기반 토큰 재발급 및 PASS 본인인증 연동
- 포인트 적립·차감과 외부 기프트샵 API 연동, MongoDB 이력과 RDB 데이터 정합성 관리

**기술:** Java 8, Spring Framework, MSSQL, MongoDB, Redis

### 방송 광고 관리 시스템 재구축
*2025.02 ~ 2025.12*

- eXBuilder XTM 기반 화면을 JSP로 전환
- SBUx/SBGrid 공통 UI 구조, Custom Tag 및 GridBuilder 정비
- 내부·외부 사용자 MFA 인증 흐름 구현

**기술:** Java 8, Spring Framework, JSP, Oracle, SBUx/SBGrid

### 오픈지로 비대면 수금 서비스
*2022.12 ~ 2023.04*

- 외부 API 연동으로 청구 생성, 납부 링크 발급, 알림톡 발송 및 수금 처리 자동화
- 배치 기반 상태 조회와 미확인 결과 재확인 흐름 구현
- 대량 API 호출 오류와 응답 불일치 등 운영 이슈 분석 및 개선

**기술:** Java, Spring Framework, MSSQL, REST API, Batch

### 모바일 수금관리 시스템 재구축
*2019.08 ~ 2019.11*

- 기존 앱 유지보수가 어려워진 환경에서 APP+WEB 하이브리드 구조로 재구축
- 고객 검색·수금·VOC 화면 및 카드 결제 연동 구현
- 결제 요청·승인·최종 처리 상태를 구분하고 응답 누락 및 상태 불일치 대응 로직 보완

**기술:** Java 7, Spring Framework, JSP, MSSQL, WebView

## 기술 스택

- **Language:** Java, C#
- **Backend:** Spring Framework, Spring Boot, MyBatis, REST API
- **Database/Cache:** MSSQL, Oracle, MariaDB, MongoDB, Redis
- **Frontend/Legacy UI:** JSP, Thymeleaf, JavaScript, SBUx/SBGrid, WinForm
- **Integration/Security:** 외부 API, PASS, TOTP MFA, Firebase FCM, 세션/토큰 기반 인증
- **Operations:** Linux/Windows 서버 운영 대응, WebToB, JEUS, WildFly, Tomcat, Grafana, Prometheus, Windows Exporter
- **Build/Version Control:** Maven, Gradle, GitLab

## 참고

- SaaS 전환 프로젝트는 진행 중이며, 완료된 범위와 설계·적용 중인 범위를 구분해 설명합니다.
- 성과 수치가 확인되지 않은 항목은 임의의 수치로 표현하지 않았습니다.
