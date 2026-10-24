# 옥외 광고 청약 시스템 SaaS 전환 및 공통 아키텍처 정비

- 기간: 2026.09 ~ 진행 중
- 역할: 백엔드 공통 구조 정비, 레거시 전환, 인증/인가 구조 설계 및 구현
- 기술 스택: Java 17, Spring Boot 3.5.x, Gradle, MyBatis, MSSQL, Thymeleaf, JSP(전환 대상)

## 프로젝트 개요

기존 Java 8 / Spring Framework 기반 업무 시스템을 Java 17 / Spring Boot 3.5.x 기반으로 전환하는 프로젝트다. 단순한 버전 업그레이드에 그치지 않고, 레거시 의존성을 줄이고 공통 설정과 요청 처리 구조를 정리해 이후 기능 개발과 유지보수가 일관되게 이루어질 수 있는 기반을 마련하고 있다.

현재 진행 중인 작업이며, 아래 내용은 완료된 기능과 설계·적용 중인 항목을 구분해 기술한다.

## 주요 수행 내용

### 1. 실행 환경 및 빌드 구조 전환

- Java 8에서 Java 17로 전환하고 Spring Boot 3.5.x 기반 실행 구조를 구성
- 기존 Maven/WAR 중심 구성을 Gradle/JAR 기반으로 정비
- 기존 전자정부프레임워크 의존성을 확인하고 Spring Boot 표준 구성으로 대체하는 작업 진행
- 외부 설정과 공통 Bean 구성을 정리해 환경별 설정 변경 지점을 명확하게 관리

### 2. 화면 렌더링 구조 전환

- 기존 JSP 화면을 Thymeleaf 기반으로 전환하는 공통 구조를 정비
- 기존 화면의 메뉴·iframe 흐름과 레거시 JavaScript 구성에 대한 호환성을 고려
- 화면 전환에 필요한 공통 데이터와 라이선스 설정을 공통 모델 구성에서 제공하도록 정리

### 3. API 응답 및 예외 처리 표준화

- API 응답 DTO를 공통화해 성공·실패 응답 형식을 일관되게 관리
- 전역 예외 처리 구조를 마련해 Controller별 반복 예외 처리 코드를 줄이는 방향으로 정비
- 메시지 코드와 메시지 조회 구성을 정리해 오류 응답의 일관성을 높이는 작업 진행

### 4. 인증·인가 구조 정비

- 로그인 세션에 저장된 인증 정보를 기준으로 조직 권한, 매체 권한, 사용자 그룹 권한을 분리해 다룰 수 있도록 구조를 정리
- Controller에 권한 검사 코드를 반복 작성하지 않도록 AOP 기반 공통 권한 검사 방식을 설계·적용 중
- 요청 파라미터의 매체 ID와 사용자가 접근 가능한 매체 범위를 비교해야 하는 API를 고려해 리소스 단위 권한 검증 지점을 분리
- 공통코드 관리와 같은 관리자 기능은 조직 권한과 사용자 그룹 권한을 함께 확인하도록 접근 정책을 구분
- 화면 메뉴 표시 여부와 API 접근 권한을 별개의 검증 대상으로 보고, UI에서 숨기는 것만으로 보안을 보장하지 않도록 구성

## 기술적으로 고려한 점

- **전환 범위 통제:** 화면과 업무 로직을 한 번에 재작성하기보다 공통 설정과 요청 처리 기반부터 정비해 기존 기능 변경 범위를 줄인다.
- **공통 관심사 분리:** API 응답, 예외 처리, 권한 검증을 각 Controller의 반복 코드에서 분리해 누락 가능성을 줄인다.
- **인가 정책의 명시성:** 조직·매체·사용자 그룹 권한을 하나의 관리자 여부로 뭉뚱그리지 않고, API가 요구하는 권한을 명확히 구분한다.
- **화면과 서버의 보안 경계:** 메뉴 노출 제어는 사용성 목적이며, 실제 데이터 접근은 서버 측 API 권한 검증으로 보호한다.
- **점진적 적용:** 기존 세션·화면 구조와 연동되는 부분을 확인하며 전환 범위를 단계적으로 확장한다.

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

### AOP 기반 권한 검증의 개념 예시

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface RequireMediaAccess {
    String mediaIdParameter() default "mediaId";
}
```

```java
@RequireMediaAccess(mediaIdParameter = "mediaId")
public MediaDetailResponse getMediaDetail(String mediaId) {
    return mediaService.getDetail(mediaId);
}
```

Controller는 업무 처리에 집중하고, 공통 권한 검증 계층이 인증 사용자와 요청 매체 ID를 비교하는 방식이다. 실제 적용 시에는 파라미터 해석 방식, 메서드 오버로드, 복수 권한 조건, 목록 조회처럼 여러 매체를 다루는 API를 명확히 정의하고, 권한 검증 누락을 테스트로 확인해야 한다.

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
