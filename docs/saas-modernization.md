# 옥외 광고 청약 시스템 SaaS 전환 및 공통 아키텍처 정비

- 기간: 2026.09 ~ 진행 중
- 역할: 백엔드 공통 구조 정비, 레거시 전환, 인증/인가 구조 설계 및 구현
- 기술 스택: Java 17, Spring Boot 3.5.x, Gradle, MyBatis, MSSQL, Thymeleaf, JSP(전환 대상)

## 프로젝트 개요

기존 Java 8 / Spring Framework 기반 업무 시스템을 Java 17 / Spring Boot 3.5.x 기반으로 전환하는 프로젝트다. 단순한 버전 업그레이드에 그치지 않고, 레거시 의존성을 줄이고 공통 설정과 요청 처리 구조를 정리해 이후 기능 개발과 유지보수가 일관되게 이루어질 수 있는 기반을 마련하고 있다.

현재 진행 중인 작업이며, 아래 내용은 완료된 기능과 설계·적용 중인 항목을 구분해 기술한다.

## 주요 수행 내용

### 1. 실행 환경 및 빌드 구조 전환

- Java 8 / Spring Framework 기반 시스템을 Java 17 / Spring Boot 3.5.x 기반으로 전환
- 기존 Maven/WAR 중심 구성을 Gradle/JAR 기반으로 정비
- 전자정부프레임워크 의존성이 높은 구조와 직접 배치·중복 관리되던 JAR 의존성을 검토하고 Gradle 기반 의존성 관리로 정리
- Gradle Dependency Locking을 적용해 의존성 버전을 고정하고, 빌드·배포 시 라이브러리 구성의 일관성을 확보하도록 개선
- XML 기반 Spring 설정을 Java Config 방식으로 전환하고 외부 설정과 공통 Bean 구성을 정리

### 2. Thymeleaf 기반 화면 공통 구조 재구성

- 기존 JSP의 include 구조를 Thymeleaf의 layout·fragment·view 구조로 재구성
- 공통 화면 요소의 재사용성을 높이고 공통 레이아웃과 개별 화면의 역할을 분리
- 기존 메뉴·iframe 흐름과 레거시 JavaScript 구성의 호환성을 고려해 전환 기반 정비

### 3. 공통 API 응답 및 전역 예외 처리

- 공통 API 응답 DTO와 전역 예외 처리기를 구현하고 주요 API에 적용
- Controller별 `try-catch` 중심의 반복적인 예외 처리 방식을 공통 처리 구조로 전환해 Controller가 서비스 호출과 요청 처리 흐름에 집중할 수 있도록 개선
- 메시지 코드 및 메시지 조회 구성을 공통 처리 흐름과 연계해 정비

### 4. AOP 기반 API 인가 및 데이터 조회 범위 통제

- 기존 프론트엔드 중심의 화면 접근 권한 제어를 서버 측 API 인가 및 데이터 범위 검증으로 확장
- 사용자 메뉴 권한과 메뉴 URI를 기준으로 API 접근 여부를 검증하는 공통 구조 구현
- 공통코드 API는 `@CommonAPI`로 별도 표시하고, 적용 사유를 설명하는 `reason` 속성을 필수화해 정책 적용 의도를 명시적으로 관리
- `@CheckScope` 어노테이션으로 API별 소속·매체 데이터 검증 대상과 최대 허용 범위를 선언하고, AOP에서 메서드 파라미터를 분석해 DTO 또는 개별 파라미터의 소속·매체 코드를 추출한 뒤 공통 검증 수행
- `OWN`을 기본 범위로 두고, 예외적으로 넓은 조회가 필요한 API에는 `ANY` 및 소속·매체 전체 조회 허용 옵션을 명시하도록 구성
- Scope 관련 어노테이션 속성의 유효성을 검사하는 Validator를 구현해 잘못된 설정을 Spring 시작 시점에 검출
- URI별 권한 정책을 하드코딩하는 방식 대신 업무 화면별 Controller에 정책을 명시해, API 코드에서 조회 가능 범위를 파악하기 쉽게 설계
- 신규 메서드에 어노테이션이 누락되면 해당 데이터 범위 검증이 실행되지 않는 한계가 있어, README에 적용 기준을 정리하고 코드 리뷰를 통한 확인을 보완책으로 마련

### 5. SaaS 인증 API 연동 계획

- 2026년 11월 제공 예정인 인증 API 가이드를 확인한 후 세부 연동 방식을 확정할 예정
- 인증 API에서 받은 토큰은 인증 요청에 활용하고, Redis에 사용자 정보와 메뉴 권한을 저장해 각 시스템에서 활용하는 방향을 검토 중
- 권한은 각 업무 시스템에서 관리하며, 권한 변경 사항이 빠르게 반영되도록 Redis 기반 정보 관리를 활용하는 것이 목표
- Redis 데이터의 갱신·무효화 방식과 권한 변경 반영 시점은 아직 확정되지 않음

## 기술적으로 고려한 점

- **전환 범위 통제:** 화면과 업무 로직을 한 번에 재작성하기보다 공통 설정과 요청 처리 기반부터 정비해 기존 기능 변경 범위를 줄임
- **의존성 재현성:** Gradle Dependency Locking으로 라이브러리 버전을 고정해 개발·배포 환경의 의존성 차이를 줄이도록 구성
- **공통 관심사 분리:** API 응답, 예외 처리, 권한 검증을 Controller의 반복 코드에서 분리
- **인가 정책의 명시성:** URI 매핑만으로 정책을 관리할 때의 하드코딩 및 가시성 문제를 고려해 어노테이션에 API별 데이터 접근 정책을 선언
- **설정 검증과 누락 관리 구분:** 어노테이션의 잘못된 속성 설정은 시작 시점에 검출하지만, 어노테이션 누락 자체는 자동 검출하지 않으므로 README와 코드 리뷰로 보완
- **화면과 서버의 보안 경계:** 메뉴 노출 제어는 사용성 목적이며, 실제 API 접근과 데이터 범위는 서버 측에서 검증
- **진행 상태 구분:** 인증 API 연동과 Redis 권한 정보 갱신 방식은 가이드 수령 후 확정할 예정이며, 아직 완료 성과로 표현하지 않음

## 포트폴리오용 대표 코드 예시

아래 코드는 실제 운영 소스의 복사본이 아니라, 프로젝트에서 정비 중인 구조를 설명하기 위한 축약 예시다. 실제 클래스명과 세부 정책은 구현 내용에 맞춰 별도로 검증해야 한다.

### 공통 API 응답 DTO

```java
public record ApiResponse<T>(
        boolean success,
        T data,
        String code,
        String message
) {
    public static <T> ApiResponse<T> ok(T data) {
        return new ApiResponse<>(true, data, null, null);
    }

    public static <T> ApiResponse<T> fail(String code, String message) {
        return new ApiResponse<>(false, null, code, message);
    }
}
```

공통 응답 형식을 통해 Controller마다 서로 다른 응답 구조를 만드는 일을 줄이고, 클라이언트가 성공·실패 결과를 일관되게 처리하도록 하는 패턴이다.

### `@CheckScope` 적용 예시

아래는 프로젝트에서 사용하는 `@CheckScope`의 정책 선언 형태를 보여주는 축약 예시다. 실제 API에는 해당 API가 허용해야 하는 범위와 전체 조회 정책에 맞는 값을 지정한다.

```java
@CheckScope(
    value = {"Media", "Company"},
    company = ANY,
    media = ANY,
    allowCompanyAll = true,
    allowMediaAll = true
)
public ApiResponse<SearchResponse> search(SearchRequest request) {
    return ApiResponse.ok(searchService.search(request));
}
```

이 예시는 소속과 매체를 모두 검증 대상으로 지정하고, 해당 API에서 허용 범위 및 전체 조회를 넓게 설정하는 경우를 나타낸다. 모든 API에 `ANY`와 전체 조회 허용 옵션을 적용한다는 뜻은 아니다. 실제 정책은 API의 업무 요구사항과 사용자 권한에 맞게 제한해야 한다.

AOP는 메서드 파라미터를 분석해 DTO 또는 개별 파라미터에서 소속·매체 코드를 추출하고, 사용자 권한과 어노테이션에 선언된 정책을 기준으로 공통 검증을 수행한다. Validator는 어노테이션 속성의 잘못된 사용을 애플리케이션 시작 시점에 검출한다. 다만 어노테이션 자체의 누락을 자동 검출하는 기능은 아니므로, README의 적용 기준과 코드 리뷰를 보완책으로 사용한다.

### 전역 예외 처리의 개념 예시

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(BusinessException.class)
    public ResponseEntity<ApiResponse<Void>> handleBusinessException(
            BusinessException exception) {
        ApiResponse<Void> body =
                ApiResponse.fail(exception.getCode(), exception.getMessage());

        return ResponseEntity
                .status(exception.getHttpStatus())
                .body(body);
    }
}
```

업무 예외를 공통 응답 형식으로 변환하는 예시다. 실제 HTTP 상태 코드와 오류 메시지는 서비스의 API 규약 및 정보 노출 정책에 맞춰 결정한다.

## 진행 상태 및 다음 단계

- [x] Java 17 / Spring Boot 3.5.x 전환 기반 구성
- [x] Gradle 기반 프로젝트 구조 및 공통 설정 정비 착수
- [ ] 기존 화면의 Thymeleaf 전환 범위 확대
- [ ] 공통 응답·예외 처리의 API별 적용 및 검증
- [ ] 조직·매체·사용자 그룹 권한 정책별 테스트 보강
- [ ] 레거시 의존성 제거 및 전환 결과 회귀 검증

> 이 프로젝트는 진행 중이다. 완료되지 않은 항목은 이력서나 면접에서 완료 성과로 표현하지 않고, 현재 설계·구현 범위를 기준으로 설명한다.
