# 실전! 스프링 부트와 JPA 활용2 - API 개발과 성능 최적화

## 소개
이 프로젝트는 스프링 부트와 JPA를 활용하여 실무 수준의 API를 개발하고 성능을 최적화하는 방법을 학습하기 위해 진행되었습니다. RESTful API를 설계하고, JPA의 다양한 성능 최적화 기법을 적용하며, 실무에서 필수적으로 고려해야 할 요소들을 다루었습니다.

---

## 프로젝트 목표
- **API 설계 및 구현**: RESTful API를 설계하고 개발하는 과정 학습
- **JPA 활용**: 영속성 관리 및 성능 최적화를 위한 JPA 적용
- **DTO 변환**: 엔티티를 DTO로 변환하여 API 응답의 안정성 유지
- **지연 로딩 및 최적화**: 지연 로딩과 성능 최적화를 위한 다양한 기법 적용
- **페이징과 한계 돌파**: 데이터 조회 시 성능을 고려한 최적화 기법 활용
- **OSIV 설정**: Open Session In View 패턴을 이해하고 실무에서의 활용 방안 학습
- **Spring Data JPA 및 QueryDSL 적용**: 반복적인 쿼리 작성 없이 JPA와 QueryDSL을 활용한 동적 쿼리 처리

---

## 프로젝트 구조
```
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com.example.jpashop
│   │   │       ├── api  # API 컨트롤러
│   │   │       ├── domain  # 엔티티 클래스
│   │   │       ├── repository  # JPA 리포지토리
│   │   │       ├── service  # 비즈니스 로직
│   │   │       ├── dto  # DTO 클래스
│   │   │       └── config  # 설정 관련 클래스
│   │   └── resources
│   │       ├── application.yml  # 스프링 부트 설정 파일
│   │       ├── data.sql  # 초기 데이터 로드
│   │       └── messages.properties  # 다국어 지원
│   └── test  # 테스트 코드
├── README.md  # 프로젝트 설명서
└── .gitignore  # Git 관리 제외 파일
```

---

## 핵심 기능 및 사용 기술

### 1. RESTful API 설계 및 구현
- **이유**: 클라이언트와 서버 간 명확한 통신을 위한 구조화된 API 필요
- **내용**:
  - 회원 등록, 조회, 수정 API 구현
  - 주문 및 주문 내역 조회 API 개발

### 2. DTO 변환을 통한 API 응답 처리
- **이유**: 엔티티를 직접 노출하는 문제를 방지하고 API 응답의 안정성 유지
- **내용**:
  - 엔티티 대신 DTO를 사용하여 API 응답 구성
  - `@JsonIgnore`를 활용하여 무한 루프 방지

### 3. JPA 지연 로딩 및 성능 최적화
- **이유**: 성능을 고려한 효율적인 데이터 조회 필요
- **내용**:
  - 기본적으로 `LAZY` 설정을 유지하고 필요한 경우 `fetch join` 사용
  - `hibernate.default_batch_fetch_size`를 설정하여 N+1 문제 해결

### 4. 페이징과 한계 돌파
- **이유**: 대량 데이터를 처리할 때 성능을 유지하기 위함
- **내용**:
  - `fetch join`을 사용할 경우 페이징이 어려우므로 `@BatchSize` 설정을 적용
  - `spring.jpa.properties.hibernate.default_batch_fetch_size=1000` 활용

### 5. OSIV 설정 및 성능 최적화
- **이유**: 실무에서 효율적인 트랜잭션 관리를 위해 필요
- **내용**:
  - `spring.jpa.open-in-view=false` 설정으로 불필요한 데이터베이스 커넥션 유지 방지
  - `@Transactional`을 활용하여 서비스 계층에서 데이터 조회

### 6. Spring Data JPA 및 QueryDSL 적용
- **이유**: 반복적인 쿼리 작성을 줄이고, 가독성을 높이기 위함
- **내용**:
  - `JpaRepository`를 사용하여 기본적인 CRUD 처리
  - QueryDSL을 활용하여 동적 쿼리 작성

---

## 실행 방법
1. **환경 구성**
   - JDK 17 이상 설치
   - Maven 또는 Gradle 설치
2. **프로젝트 클론**
   ```bash
   git clone https://github.com/username/jpa-api-optimization.git
   cd jpa-api-optimization
   ```
3. **의존성 설치 및 실행**
   ```bash
   mvn clean install
   mvn spring-boot:run
   ```
4. **API 테스트**
   - `Postman` 또는 `Swagger UI`를 사용하여 API 요청 확인
   - `http://localhost:8080/swagger-ui.html`에서 API 문서 확인

---

## 향후 개선 방향
- Redis를 활용한 캐싱 적용하여 성능 최적화
- Kafka 또는 RabbitMQ를 활용한 비동기 이벤트 처리
- CI/CD 환경 구축을 통한 자동화된 배포 적용

---

이 프로젝트는 스프링 부트와 JPA를 활용한 API 개발과 성능 최적화 기법을 학습하고 실무에서의 활용법을 익히기 위해 제작되었습니다.

