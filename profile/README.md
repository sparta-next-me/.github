<img width="1920" height="823" alt="image" src="https://github.com/user-attachments/assets/2de8151c-f4fc-48fd-a976-ca6892b8b0f6" />


## 📍 프로젝트 소개
- SmartLogis는 상품 주문부터 허브 간 이동, 최종 배송까지의 전체 물류 흐름을 통합 관리하는 B2B 물류 플랫폼입니다.<br/>
- Spring Cloud 기반의 마이크로서비스 아키텍처를 통해 업체 간 주문 관리, 허브 네트워크를 통한 배송 경로 최적화, 실시간 배송 추적, AI 기반 배송 알림 등<br/>
- 대규모 물류 비즈니스의 핵심 기능을 독립적이고 확장 가능한 서비스로 제공합니다.


### 주요 특징

  - **마이크로서비스 아키텍처**: 도메인별로 분리된 독립적인 서비스 구조
  - **이벤트 기반 통신**: RabbitMQ를 활용한 비동기 메시징으로 서비스 간 느슨한 결합
  - **서비스 디스커버리**: Eureka를 통한 동적 서비스 등록 및 발견
  - **중앙 집중식 설정 관리**: Spring Cloud Config Server를 통한 설정 관리
  - **인증 및 권한 관리**: Keycloak 기반의 토큰 인증
  - **분산 추적 및 모니터링**: Zipkin, Prometheus, Loki를 활용한 통합 관찰성
  - **AI 기반 알림**: Spring AI를 활용한 배송 알림 메시지 자동 생성 및 Slack 알림
  - **API Gateway**: 단일 진입점을 통한 라우팅, 인증, 로드 밸런싱

### 주요 기능

#### 사용자 관리
- 사용자 회원가입 및 인증 (Keycloak 연동)
- 역할 기반 권한 관리 (MASTER, HUB_MANAGER, DELIVERY_MANAGER, COMPANY_MANAGER)
- 사용자 정보 조회 및 수정
- 사용자 검색 (이름, 이메일, 역할별)
- 소프트 삭제 및 감사 추적

#### 주문 관리
- 주문 생성 (자동 주문자 정보 조회)
- 주문 단건/목록 조회
- 주문 상태 변경 (PENDING → COMPLETED / CANCELED)
- 주문 검색 (주문자, 상품, 공급/수령 업체별)
- 주문 삭제 (논리적 삭제)
- 배송 경로 계산 요청 (Hub Service 연동)

#### 배송 관리
- 배송 정보 자동 생성 (이벤트 기반)
- 배송 단건/목록 조회
- 배송 상태 업데이트
  - HUB_PENDING → HUB_MOVING → COMPANY_PENDING → COMPANY_MOVING → DELIVERED
- 배송 기록 관리 (DeliveryHistory)
  - 허브 간 이동 기록
  - 업체 배송 기록
  - 실제 거리/소요시간 기록
- 배송 기록 상태 업데이트 (구간별 상태 관리)
- 배송 검색 (주문, 허브, 담당자별)
- 자동 동기화 (모든 배송 기록 완료 시 배송 상태 자동 전환)

#### 허브 관리
- 허브 생성/조회/수정/삭제
- 허브 주소 기반 좌표 변환 (Kakao Geocoding API)
- 허브 간 경로 생성 및 관리
- 최적 배송 경로 계산 (Kakao Directions API)
- 경로 정보 캐싱 (Redis)
- 배송 경로 이벤트 발행 (RabbitMQ)
- 경로 재계산 기능

#### 상품 관리
- 상품 등록/수정/삭제
- 상품 조회: 단건/목록 조회(상품명별, 소속 허브별, 소속 업체별, 상품 상태별)
- 상품 재고 내역 관리
  - 모든 재고 변경에 대해 기록하여 관리
  - 재고 변경 타입 : 최초/재고 증가/감소/반환
- 재고 보충 자동화
  -  재고 부족 이벤트를 통한 자동화
- 정보 업데이트 자동화
  - 소속 업체 정보 수정 시 이벤트를 통해 정보 업데이트

#### 업체 관리
- 업체 등록/수정/삭제
- 상품 조회 : 단건/목록 조회(소속 허브별, 업체 상태별, 업체 타입별, 키워드 기준)
- 업체 유형 관리 (공급업체, 수령업체)
- 상태 업데이트 자동화
  - 소속 허브 상태 수정 시 이벤트를 통해 업체 및 상품 상태 업데이트
- 재고 보충 자동화
  - 재고 부족 시 재고 보충 이벤트를 발행을 통한 자동화

#### AI & 알림
- Spring AI 기반 최종 발송 시한 예측 및 배송 알림 메시지 자동 생성
- Slack을 통한 배송 담당자 실시간 알림
- AI 및 Slack 실행 이력 조회 및 관리


## 👔 팀원 및 역할
<table>
  <tr>
    <td align="center">
      <a href="https://github.com/hyeon48615">
        <img width="80" height="150" src="https://github.com/hyeon48615.png" alt="이서현"/>
        <br/><strong>이서현</strong><br/>
        <a>(LEADER)</a>
      </a>
    </td>
    <td align="left">
      - Keycloak 기반 인증/인가 구현<br/>
      - Gateway 블랙리스트와 역할(ROLE) 캐싱으로 권한 검증 성능 향상 및 차단 구현<br/>
      - Spring AI와 Vertex AI를 통한 최종 발송 시한 계산 및 자동 메세지 생성 구현<br/>
      - RabbitMQ 및 Spring Cloud 기반 배송-알림 서비스 이벤트 구현<br/>
      - 공통 모듈 개발 및 배포, 인프라 구성(Eureka, Config Server, Gateway Server)
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="https://github.com/sojsnake">
        <img width="80" height="150" src="https://github.com/sojsnake.png" alt="박소정"/>
        <br/><strong>박소정</strong><br/>
        <a>(MEMBER)</a>
      </a>
    </td>
    <td align="left">
      - 업체 정보 관리, 상품 운영, 재고 이력 관리를 위한 API 구현<br/>
      - RabbitMQ를 활용하여 업체-상품 간 이벤트 기반 연동 구현<br/>
      - 재고 업데이트 자동화 로직 구현 및 재고 내역 기록하여 관리<br/>
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="https://github.com/hoonssac">
        <img width="80" height="150" src="https://github.com/hoonssac.png" alt="서상훈"/>
        <br/><strong>서상훈</strong><br/>
        <a>(MEMBER)</a>
      </a>
    </td>
    <td align="left">
      - RabbitMQ, Spring Cloud Stream을 활용한 주문-배송 이벤트 기반 연동 구현<br/>
      - OpenFeign을 통한 마이크로서비스 통신 및 주문-배송 도메인 개발<br/>
      - 배송 상태 관리 API 및 배송 기록 기반 자동 동기화 로직 구현<br/>
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="https://github.com/nineeko">
        <img width="80" height="150" src="https://github.com/nineeko.png" alt="이채은"/>
        <br/><strong>이채은</strong><br/>
        <a>(MEMBER)</a>
      </a>
    </td>
    <td align="left">
      - 허브 서비스 개발 및 RabbitMQ 기반 도메인 이벤트 처리 구현 <br/>
      - Redis 캐싱(허브/허브 간 이동 정보 조회) 기능 개발 <br/>
      - 카카오 맵 API를 활용한 거리·시간 계산 및 도로명 주소 좌표 변환 로직 구현 <br/>
      - PostgreSQL + pgvector 기반 허브 위치 벡터 저장 구조 설계<br/>
    </td>
  </tr>
</table>



## ⚒️ 서비스 구성

#### Infrastructure

| 서비스 | 설명 |
|--------|------|
| **eureka-server** | 서비스 디스커버리 - 마이크로서비스 등록 및 발견 |
| **config-server** | 중앙 설정 관리 - 서비스별 설정 중앙화 |
| **gateway-server** | API Gateway - 클라이언트 요청 라우팅 및 인증 |
| **common-module** | 공통 라이브러리 - 인증, 예외처리, API 응답 표준화 |

#### Business

| 서비스 | 설명 |
|--------|-------|
| **user-service** | 사용자 관리 - Keycloak 연동, 권한 관리 |
| **order-service** | 주문 관리 - 주문 생성, 조회, 상태 변경 |
| **delivery-service** | 배송 관리 - 배송 정보, 경로 추적, 상태 업데이트 |
| **hub-service** | 허브 관리 - 허브 정보, 허브 네트워크, 경로 계산, Redis 캐싱 |
| **product-service** | 상품 관리 - 상품 정보, 재고 관리 |
| **company-service** | 업체 관리 - 업체 정보, 업체별 배송 관리 |
| **ai-service** | AI 서비스 - Spring AI 기반 발송 최종 시한 예측 및 알림 메시지 생성 |
| **notification-service** | 알림 서비스 - 메시지 Slack 발송 |



## ⚒️ 기술 스택
#### Backend
- **Language**: Java 21
- **Framework**: Spring Boot 3.5.7, Spring Cloud 2025.0.0
- **Database**:
  - MySQL 8.0
  - PostgreSQL
- **Cache**: Redis
- **Message Queue**: RabbitMQ
- **ORM**: Spring Data JPA, QueryDSL

#### Infrastructure
- **Service Discovery**: Netflix Eureka
- **Configuration**: Spring Cloud Config Server
- **API Gateway**: Spring Cloud Gateway
- **Authentication**: Keycloak
- **Client**: OpenFeign, Spring Cloud LoadBalancer

#### External APIs & AI
- **Maps**: Kakao Maps API (경로 계산 및 지오코딩)
- **AI**: Spring AI (Vertex AI Gemini)
- **Notification**: Slack API

#### Monitoring & Observability
- **Metrics**: Micrometer, Prometheus
- **Tracing**: Zipkin
- **Logging**: Logback, Loki

#### Documentation
- **API Docs**: SpringDoc OpenAPI (Swagger UI)

## ⚒️ 시스템 아키텍처
<img width="1920" alt="System Architecture" src="https://github.com/user-attachments/assets/d0197e5b-0e5f-4c65-adac-4603a13420aa" />

<img width="1920" alt="ERD" src="https://github.com/user-attachments/assets/0f1a4156-d254-485c-9609-58a66d74d0db" />

## 실행 방법
#### 1. **인프라 서비스 실행**
 ```bash
 # Docker Compose 사용 시
 docker-compose up -d
 ```

#### 2. **환경 변수 설정**
  ```bash
  # .env.example 파일을 복사하여 .env 파일 생성
  cp .env.example .env
  # .env 파일에 실제 값 입력 (API 키, DB 정보 등)
  ```
#### 3. **서비스 실행**
실행 순서: eureka-server → config-server → gateway-server → 기타 서비스들
  ```bash
  # 각 서비스 디렉토리에서
  ./gradlew bootRun
  ```

#### 4. **API 문서**
Gateway를 통해 모든 서비스의 API 문서를 통합하여 제공합니다.<br/>
통합 API 문서: `http://localhost:3000/api-docs.html`



---

> TeamSparta 대규모 AI 시스템 프로젝트<br>
> 개발 기간 : 2025.11.17 ~ 2025.11.28
