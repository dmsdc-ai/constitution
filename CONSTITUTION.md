# 소프트웨어 개발 헌법 (Constitution)

모든 프로젝트에서 참고해야 할 개발 원칙들을 아토믹하게 분류하고 점수화한 문서입니다.

---

## 점수 체계 설명

| 점수 | 의미 |
|------|------|
| ⭐⭐⭐⭐⭐ (5) | 필수 (모든 프로젝트에 반드시 적용) |
| ⭐⭐⭐⭐ (4) | 강력 권장 (대부분의 프로젝트에 적용) |
| ⭐⭐⭐ (3) | 권장 (상황에 따라 적용) |
| ⭐⭐ (2) | 선택적 (특정 상황에서만 유용) |
| ⭐ (1) | 참고용 (알아두면 좋음) |

---

## 1. 핵심 설계 원칙 (Core Design Principles)

### 1.1 SOLID 원칙

#### 1.1.1 Single Responsibility Principle (SRP) - 단일 책임 원칙
**점수: ⭐⭐⭐⭐⭐ (5)**

> 클래스는 하나의 책임만 가져야 하며, 변경의 이유도 하나여야 한다.

| 장점 | 단점 |
|------|------|
| 코드 이해도 향상 | 클래스 수 증가 |
| 유지보수 용이 | 초기 설계 시간 증가 |
| 테스트 용이 | 과도한 분리시 복잡도 증가 |
| 재사용성 향상 | |

**적용 예시:**
```
❌ UserService (유저 CRUD + 이메일 발송 + 로깅)
✅ UserService (유저 CRUD만), EmailService, LogService
```

---

#### 1.1.2 Open/Closed Principle (OCP) - 개방/폐쇄 원칙
**점수: ⭐⭐⭐⭐ (4)**

> 확장에는 열려있고, 수정에는 닫혀있어야 한다.

| 장점 | 단점 |
|------|------|
| 기존 코드 안정성 보장 | 추상화 레이어 증가 |
| 새 기능 추가 용이 | 과도한 인터페이스 생성 위험 |
| 버그 유입 최소화 | 초기 설계 복잡도 |

**적용 예시:**
```
❌ 새 결제 방식 추가시 기존 PaymentService 수정
✅ PaymentStrategy 인터페이스 + 각 결제 방식별 구현체
```

---

#### 1.1.3 Liskov Substitution Principle (LSP) - 리스코프 치환 원칙
**점수: ⭐⭐⭐⭐ (4)**

> 자식 클래스는 부모 클래스를 대체할 수 있어야 한다.

| 장점 | 단점 |
|------|------|
| 다형성 보장 | 상속 구조 설계 어려움 |
| 예측 가능한 동작 | 잘못된 상속 관계 발견 시 큰 리팩토링 필요 |
| 코드 재사용성 | |

**위반 예시:**
```
❌ Rectangle을 상속한 Square에서 width/height 독립 설정 불가
✅ Shape 인터페이스를 각각 구현
```

---

#### 1.1.4 Interface Segregation Principle (ISP) - 인터페이스 분리 원칙
**점수: ⭐⭐⭐⭐ (4)**

> 클라이언트는 자신이 사용하지 않는 인터페이스에 의존하지 않아야 한다.

| 장점 | 단점 |
|------|------|
| 불필요한 의존성 제거 | 인터페이스 수 증가 |
| 결합도 감소 | 관리 복잡도 증가 가능 |
| 테스트 용이 | |

**적용 예시:**
```
❌ IWorker (work, eat, sleep) - 로봇에게 eat/sleep 불필요
✅ IWorkable, IEatable, ISleepable 분리
```

---

#### 1.1.5 Dependency Inversion Principle (DIP) - 의존성 역전 원칙
**점수: ⭐⭐⭐⭐⭐ (5)**

> 고수준 모듈은 저수준 모듈에 의존하면 안 된다. 둘 다 추상화에 의존해야 한다.

| 장점 | 단점 |
|------|------|
| 모듈 간 결합도 감소 | DI 컨테이너 학습 필요 |
| 테스트 용이 (Mock 주입) | 초기 설정 복잡 |
| 유연한 구현체 교체 | |

**적용 예시:**
```
❌ OrderService가 MySQLRepository를 직접 의존
✅ OrderService → IRepository ← MySQLRepository
```

---

### 1.2 기본 원칙 (Fundamental Principles)

#### 1.2.1 DRY (Don't Repeat Yourself)
**점수: ⭐⭐⭐⭐⭐ (5)**

> 모든 지식은 시스템 내에서 단일하고, 모호하지 않은 표현을 가져야 한다.

| 장점 | 단점 |
|------|------|
| 유지보수 용이 | 과도한 추상화 위험 |
| 일관성 보장 | 잘못된 추상화시 더 큰 문제 |
| 버그 수정 한 곳에서 | |

**주의사항:**
- 비슷해 보여도 다른 맥락이면 분리 유지
- "3번 반복되면 추상화" 규칙 적용

---

#### 1.2.2 KISS (Keep It Simple, Stupid)
**점수: ⭐⭐⭐⭐⭐ (5)**

> 단순한 솔루션이 복잡한 솔루션보다 낫다.

| 장점 | 단점 |
|------|------|
| 이해하기 쉬움 | 확장성 제한 가능 |
| 버그 감소 | 복잡한 요구사항에 부적합할 수 있음 |
| 유지보수 용이 | |

**체크리스트:**
- [ ] 이 코드를 6개월 후에 이해할 수 있는가?
- [ ] 새로운 팀원이 바로 이해할 수 있는가?
- [ ] 더 단순한 방법이 있는가?

---

#### 1.2.3 YAGNI (You Ain't Gonna Need It)
**점수: ⭐⭐⭐⭐⭐ (5)**

> 실제로 필요할 때까지 기능을 추가하지 마라.

| 장점 | 단점 |
|------|------|
| 개발 시간 절약 | 나중에 큰 변경 필요할 수 있음 |
| 코드베이스 간결 | 아키텍처 확장성 제한 가능 |
| 유지보수 비용 감소 | |

**위반 신호:**
- "나중에 필요할 것 같아서..."
- "혹시 모르니까..."
- 사용되지 않는 파라미터/메서드

---

#### 1.2.4 Separation of Concerns (SoC) - 관심사 분리
**점수: ⭐⭐⭐⭐⭐ (5)**

> 프로그램을 기능적으로 겹치지 않는 섹션으로 분리한다.

| 장점 | 단점 |
|------|------|
| 모듈성 향상 | 레이어 간 통신 오버헤드 |
| 병렬 개발 가능 | 과도한 분리시 복잡도 증가 |
| 변경 영향 최소화 | |

**대표적 적용:**
- MVC/MVP/MVVM 패턴
- 레이어드 아키텍처
- 프론트엔드/백엔드 분리

---

#### 1.2.5 Composition over Inheritance - 상속보다 조합
**점수: ⭐⭐⭐⭐ (4)**

> 상속보다 객체 조합을 선호하라.

| 장점 | 단점 |
|------|------|
| 유연한 런타임 변경 | 더 많은 보일러플레이트 |
| 깊은 상속 계층 회피 | 초기 설계 복잡 |
| 테스트 용이 | |

**적용 예시:**
```
❌ class Duck extends FlyingBird extends SwimmingBird...
✅ class Duck { flyBehavior: IFly, swimBehavior: ISwim }
```

---

#### 1.2.6 Law of Demeter (LoD) - 최소 지식 원칙
**점수: ⭐⭐⭐⭐ (4)**

> 객체는 직접 관련된 객체하고만 대화해야 한다.

| 장점 | 단점 |
|------|------|
| 결합도 감소 | 위임 메서드 증가 |
| 캡슐화 강화 | Wrapper 코드 증가 |
| 변경 영향 최소화 | |

**위반 예시:**
```
❌ user.getAddress().getCity().getName()
✅ user.getCityName()
```

---

## 2. 아키텍처 원칙 (Architecture Principles)

### 2.1 Clean Architecture
**점수: ⭐⭐⭐⭐ (4)**

> 의존성은 항상 안쪽(비즈니스 로직)을 향해야 한다.

| 레이어 | 역할 |
|--------|------|
| Entities | 핵심 비즈니스 규칙 |
| Use Cases | 애플리케이션 비즈니스 규칙 |
| Interface Adapters | 데이터 변환 |
| Frameworks & Drivers | 외부 도구/프레임워크 |

| 장점 | 단점 |
|------|------|
| 프레임워크 독립적 | 초기 학습 곡선 |
| 테스트 용이 | 보일러플레이트 증가 |
| UI 독립적 | 소규모 프로젝트에 과할 수 있음 |
| DB 독립적 | |

---

### 2.2 Hexagonal Architecture (Ports & Adapters)
**점수: ⭐⭐⭐ (3)**

> 애플리케이션 코어를 외부 요소와 격리한다.

| 장점 | 단점 |
|------|------|
| 외부 의존성 교체 용이 | 복잡도 증가 |
| 테스트 용이 | 소규모 프로젝트에 과함 |
| 명확한 경계 | |

---

### 2.3 Microservices 원칙
**점수: ⭐⭐⭐ (3)** (프로젝트 규모에 따라)

| 원칙 | 점수 | 설명 |
|------|------|------|
| Single Purpose | ⭐⭐⭐⭐ | 각 서비스는 하나의 비즈니스 기능 |
| Loose Coupling | ⭐⭐⭐⭐⭐ | 서비스 간 최소 의존성 |
| High Cohesion | ⭐⭐⭐⭐ | 관련 기능은 함께 |
| Database per Service | ⭐⭐⭐ | 서비스별 독립 DB |
| API Gateway | ⭐⭐⭐⭐ | 단일 진입점 |

---

## 3. 코딩 컨벤션 (Coding Conventions)

### 3.1 네이밍 컨벤션
**점수: ⭐⭐⭐⭐⭐ (5)**

| 타입 | 컨벤션 | 예시 |
|------|--------|------|
| 클래스/타입 | PascalCase | `UserService`, `OrderRepository` |
| 함수/메서드 | camelCase | `getUserById()`, `calculateTotal()` |
| 변수 | camelCase | `userName`, `orderCount` |
| 상수 | SCREAMING_SNAKE_CASE | `MAX_RETRY_COUNT`, `API_BASE_URL` |
| 파일 (컴포넌트) | PascalCase | `UserProfile.tsx` |
| 파일 (유틸) | camelCase/kebab-case | `dateUtils.ts`, `api-client.ts` |
| 불리언 | is/has/can/should 접두사 | `isActive`, `hasPermission` |

**네이밍 원칙:**
- 의도를 드러내는 이름 사용
- 축약어 사용 자제 (명확성 > 짧음)
- 일관성 유지 (팀/프로젝트 내)

---

### 3.2 코드 포맷팅
**점수: ⭐⭐⭐⭐⭐ (5)**

| 원칙 | 설명 |
|------|------|
| 들여쓰기 일관성 | 스페이스 2/4칸 또는 탭 (팀 규칙) |
| 줄 길이 제한 | 80-120자 권장 |
| 공백 규칙 | 연산자 주위, 쉼표 뒤 |
| 중괄호 스타일 | K&R 또는 Allman (일관성 유지) |

**자동화 도구:**
- Prettier (JS/TS)
- ESLint, Pylint, RuboCop
- EditorConfig

---

### 3.3 주석 원칙
**점수: ⭐⭐⭐⭐ (4)**

| DO | DON'T |
|----|-------|
| WHY를 설명 | WHAT을 설명 (코드가 말함) |
| 복잡한 알고리즘 설명 | 모든 코드에 주석 |
| TODO/FIXME 표시 | 오래된 주석 방치 |
| API/라이브러리 문서화 | 자명한 코드에 주석 |

```
❌ // i를 1 증가
   i++;

✅ // 재시도 횟수 제한: 무한 루프 방지 및 서버 부하 방지 목적
   const MAX_RETRIES = 3;
```

---

## 4. 보안 원칙 (Security Principles)

### 4.1 Defense in Depth - 심층 방어
**점수: ⭐⭐⭐⭐⭐ (5)**

> 여러 계층의 보안 통제를 적용하여 단일 실패점을 방지한다.

| 계층 | 예시 |
|------|------|
| 네트워크 | 방화벽, WAF |
| 애플리케이션 | 입력 검증, 인증/인가 |
| 데이터 | 암호화, 접근 제어 |
| 물리적 | 서버 보안 |

---

### 4.2 Principle of Least Privilege - 최소 권한 원칙
**점수: ⭐⭐⭐⭐⭐ (5)**

> 코드와 사용자에게 필요한 최소한의 권한만 부여한다.

| 장점 | 적용 예시 |
|------|----------|
| 공격 표면 최소화 | DB 사용자는 필요한 테이블만 접근 |
| 피해 범위 제한 | API 키에 최소 권한 부여 |
| | 서비스 계정 권한 제한 |

---

### 4.3 Fail Secure - 안전한 실패
**점수: ⭐⭐⭐⭐⭐ (5)**

> 오류 발생 시 안전한 상태로 기본 설정된다.

| DO | DON'T |
|----|-------|
| 인증 실패시 접근 거부 | 예외 발생시 모든 권한 허용 |
| 에러 메시지에 민감정보 제외 | 스택 트레이스 노출 |
| 기본값은 거부 | 기본값은 허용 |

---

### 4.4 Input Validation - 입력 검증
**점수: ⭐⭐⭐⭐⭐ (5)**

> 모든 외부 입력은 신뢰하지 않고 검증한다.

| 검증 대상 | 방어 대상 |
|----------|----------|
| 사용자 입력 | XSS, SQL Injection |
| API 요청 | Injection 공격 |
| 파일 업로드 | 악성 파일 |
| URL 파라미터 | Path Traversal |

**원칙:**
- 화이트리스트 > 블랙리스트
- 클라이언트 + 서버 양쪽 검증
- 파라미터화된 쿼리 사용

---

### 4.5 Minimize Attack Surface - 공격 표면 최소화
**점수: ⭐⭐⭐⭐⭐ (5)**

| 방법 | 예시 |
|------|------|
| 불필요한 기능 제거 | 사용하지 않는 엔드포인트 제거 |
| 불필요한 포트 닫기 | 필요한 포트만 개방 |
| 기능 접근 제한 | 인증된 사용자만 접근 |

---

## 5. 테스트 원칙 (Testing Principles)

### 5.1 테스트 피라미드
**점수: ⭐⭐⭐⭐⭐ (5)**

```
        /\
       /  \    E2E Tests (적음)
      /----\
     /      \   Integration Tests (중간)
    /--------\
   /          \  Unit Tests (많음)
  --------------
```

| 테스트 유형 | 비율 | 특징 |
|------------|------|------|
| Unit | 70% | 빠름, 격리됨 |
| Integration | 20% | 모듈 간 상호작용 |
| E2E | 10% | 느림, 전체 플로우 |

---

### 5.2 TDD (Test-Driven Development)
**점수: ⭐⭐⭐⭐ (4)**

> Red → Green → Refactor 사이클

| 장점 | 단점 |
|------|------|
| 요구사항 명확화 | 초기 개발 속도 저하 |
| 설계 품질 향상 | 학습 곡선 |
| 리팩토링 안전망 | 모든 상황에 적합하지 않음 |
| 문서화 효과 | |

---

### 5.3 테스트 베스트 프랙티스
**점수: ⭐⭐⭐⭐⭐ (5)**

| 원칙 | 설명 |
|------|------|
| AAA 패턴 | Arrange → Act → Assert |
| 격리 | 테스트 간 독립성 유지 |
| 명확한 이름 | `should_returnError_when_userNotFound` |
| 단일 검증 | 하나의 테스트는 하나만 검증 |
| 인프라 독립 | Mock/Stub 활용 |
| Negative 테스트 | 실패 케이스도 테스트 |

---

### 5.4 테스트 커버리지
**점수: ⭐⭐⭐ (3)**

| 권장 커버리지 | 설명 |
|--------------|------|
| 70-80% | 현실적인 목표 |
| 핵심 비즈니스 로직 | 100% 목표 |
| 유틸리티 함수 | 높은 커버리지 |

**주의:** 커버리지 높음 ≠ 테스트 품질 높음

---

## 6. 에러 핸들링 (Error Handling)

### 6.1 Fail Fast - 빠른 실패
**점수: ⭐⭐⭐⭐⭐ (5)**

> 문제 발생시 즉시 알리고 빠르게 실패한다.

| 장점 | 적용 예시 |
|------|----------|
| 문제 조기 발견 | 초기 입력 검증 |
| 디버깅 용이 | null 체크 즉시 |
| 연쇄 에러 방지 | 설정 검증 시작시 |

---

### 6.2 Graceful Degradation - 우아한 성능 저하
**점수: ⭐⭐⭐⭐ (4)**

> 일부 기능 실패 시에도 핵심 기능은 유지한다.

| 예시 | 설명 |
|------|------|
| 캐시 실패 | DB에서 직접 조회 |
| 추천 서비스 실패 | 기본 목록 표시 |
| 이미지 로드 실패 | 플레이스홀더 표시 |

---

### 6.3 Circuit Breaker - 서킷 브레이커
**점수: ⭐⭐⭐⭐ (4)** (분산 시스템)

> 연속 실패 시 일정 시간 요청을 차단한다.

| 상태 | 동작 |
|------|------|
| Closed | 정상 요청 처리 |
| Open | 요청 즉시 실패 |
| Half-Open | 일부 요청으로 테스트 |

---

### 6.4 로깅 원칙
**점수: ⭐⭐⭐⭐⭐ (5)**

| 레벨 | 용도 |
|------|------|
| ERROR | 즉시 조치 필요 |
| WARN | 잠재적 문제 |
| INFO | 주요 이벤트 |
| DEBUG | 개발/디버깅용 |

**원칙:**
- 구조화된 로깅 (JSON)
- 민감정보 마스킹
- 상관관계 ID (Correlation ID)
- 적절한 레벨 사용

---

## 7. 성능 원칙 (Performance Principles)

### 7.1 Premature Optimization 회피
**점수: ⭐⭐⭐⭐⭐ (5)**

> "조기 최적화는 모든 악의 근원이다" - Donald Knuth

| DO | DON'T |
|----|-------|
| 먼저 측정 | 추측으로 최적화 |
| 병목 지점 식별 | 모든 코드 최적화 |
| 프로파일링 도구 사용 | 가독성 희생 |

---

### 7.2 Lazy Loading
**점수: ⭐⭐⭐⭐ (4)**

> 필요할 때까지 리소스 로딩을 지연한다.

| 장점 | 주의점 |
|------|--------|
| 초기 로드 시간 감소 | N+1 문제 주의 |
| 대역폭 절약 | 과도한 지연 로딩 피하기 |
| 리소스 효율 | |

---

### 7.3 Caching 전략
**점수: ⭐⭐⭐⭐ (4)**

| 전략 | 설명 | 적합한 경우 |
|------|------|------------|
| Cache-Aside | 캐시 미스시 DB 조회 후 캐시 | 읽기 중심 |
| Write-Through | 쓰기시 캐시+DB 동시 | 일관성 중요 |
| Write-Behind | 쓰기시 캐시만, 나중에 DB | 쓰기 성능 중요 |

**원칙:**
- 비싼 연산만 캐시
- TTL 설정 필수
- 캐시 무효화 전략 수립

---

## 8. 코드 리뷰 & 품질 (Code Review & Quality)

### 8.1 Pull Request 가이드라인
**점수: ⭐⭐⭐⭐⭐ (5)**

| 원칙 | 권장값 |
|------|--------|
| PR 크기 | 400줄 이하 |
| 리뷰 시작 | 2시간 이내 |
| 리뷰 세션 | 60분 이내 |

**체크리스트:**
- [ ] 기능이 요구사항대로 동작하는가?
- [ ] 테스트가 포함되었는가?
- [ ] 코딩 컨벤션을 따르는가?
- [ ] 보안 취약점은 없는가?
- [ ] 성능 문제는 없는가?

---

### 8.2 Code Smell 인식
**점수: ⭐⭐⭐⭐ (4)**

| Code Smell | 해결책 |
|------------|--------|
| Long Method | 메서드 분리 |
| Large Class | 클래스 분리 |
| Duplicate Code | 추출/추상화 |
| Long Parameter List | 객체로 그룹화 |
| Feature Envy | 메서드 이동 |
| Data Clumps | 클래스로 묶기 |

---

### 8.3 Technical Debt 관리
**점수: ⭐⭐⭐⭐ (4)**

| 유형 | 대응 |
|------|------|
| 소규모 (몇 시간) | 발견 즉시 수정 |
| 중규모 (며칠) | Tech Debt Friday / 백로그 |
| 대규모 (몇 주) | 전담 팀 또는 별도 계획 |

**도구:**
- SonarQube
- CodeClimate
- ESLint/TSLint

---

## 9. Git & 버전 관리 (Version Control)

### 9.1 Branching Strategy
**점수: ⭐⭐⭐⭐⭐ (5)**

| 전략 | 적합한 경우 | 복잡도 |
|------|------------|--------|
| GitHub Flow | CI/CD, 빠른 배포 | 낮음 |
| GitFlow | 정기 릴리스 | 높음 |
| Trunk-Based | 고도화된 CI/CD | 중간 |

**권장:** 팀 규모와 배포 주기에 맞게 선택

---

### 9.2 Commit Message 컨벤션
**점수: ⭐⭐⭐⭐⭐ (5)**

**Conventional Commits:**
```
<type>(<scope>): <subject>

<body>

<footer>
```

| Type | 설명 |
|------|------|
| feat | 새 기능 |
| fix | 버그 수정 |
| docs | 문서 변경 |
| style | 포맷팅 |
| refactor | 리팩토링 |
| test | 테스트 |
| chore | 빌드/설정 |

---

## 10. API 설계 원칙 (API Design)

### 10.1 RESTful API 원칙
**점수: ⭐⭐⭐⭐⭐ (5)**

| 원칙 | 설명 |
|------|------|
| 자원 기반 URL | `/users/{id}` |
| HTTP 메서드 활용 | GET, POST, PUT, DELETE |
| 상태 코드 적절히 사용 | 200, 201, 400, 404, 500 |
| 일관된 응답 형식 | JSON |
| 버전 관리 | `/api/v1/` |

---

### 10.2 Backward Compatibility - 하위 호환성
**점수: ⭐⭐⭐⭐⭐ (5)**

| DO | DON'T |
|----|-------|
| 필드 추가 (additive) | 필드 제거 |
| Deprecation 경고 | 갑작스러운 Breaking Change |
| 버전 관리 | 기존 응답 형식 변경 |

---

## 11. CI/CD & DevOps 원칙

### 11.1 Continuous Integration (CI) 원칙
**점수: ⭐⭐⭐⭐⭐ (5)**

> 코드 변경사항을 자주, 작게 통합하여 문제를 조기에 발견한다.

| 원칙 | 설명 |
|------|------|
| 자주 커밋 | 작은 단위로 자주 통합 |
| 자동 빌드 | 모든 커밋에 자동 빌드 |
| 자동 테스트 | 빌드 후 자동 테스트 실행 |
| 빠른 피드백 | 10분 이내 결과 확인 |

| 장점 | 단점 |
|------|------|
| 버그 조기 발견 | 초기 파이프라인 구축 비용 |
| 통합 문제 최소화 | 러닝 커브 |
| 코드 품질 향상 | |

---

### 11.2 Continuous Deployment (CD) 원칙
**점수: ⭐⭐⭐⭐⭐ (5)**

> 검증된 코드를 자동으로 프로덕션에 배포한다.

| 배포 전략 | 설명 | 적합한 경우 |
|----------|------|------------|
| Blue/Green | 새 버전을 별도 환경에 배포 후 전환 | 다운타임 최소화 |
| Canary | 일부 사용자에게 먼저 배포 | 리스크 최소화 |
| Rolling | 점진적으로 인스턴스 교체 | 리소스 효율 |

**필수 요소:**
- [ ] 자동화된 롤백 전략
- [ ] 배포 모니터링
- [ ] Feature Flags 활용

---

### 11.3 Infrastructure as Code (IaC)
**점수: ⭐⭐⭐⭐⭐ (5)**

> 인프라를 코드로 정의하고 버전 관리한다.

| 장점 | 도구 예시 |
|------|----------|
| 일관성 보장 | Terraform |
| 버전 관리 가능 | AWS CDK |
| 자동화 | Pulumi |
| 리뷰 가능 | Ansible |

| DO | DON'T |
|----|-------|
| 모든 인프라 코드화 | 수동 콘솔 설정 |
| 버전 관리 (Git) | 로컬에만 저장 |
| 모듈화/재사용 | 중복 코드 |
| 환경별 분리 | 하드코딩된 값 |

---

### 11.4 파이프라인 원칙
**점수: ⭐⭐⭐⭐⭐ (5)**

| 원칙 | 설명 |
|------|------|
| DRY Pipeline | 재사용 가능한 파이프라인 구성 |
| Quality Gates | 각 단계에서 품질 검증 |
| Fail Fast | 초기 단계에서 빠른 피드백 |
| Parallelization | 독립적인 작업 병렬 실행 |

**파이프라인 단계:**
```
Build → Test → Security Scan → Deploy (Staging) → Test → Deploy (Prod)
```

---

### 11.5 DevOps 문화 원칙
**점수: ⭐⭐⭐⭐ (4)**

| 원칙 | 설명 |
|------|------|
| 공유 소유권 | 개발+운영 함께 책임 |
| 지속적 학습 | 실패에서 학습, 비난 없는 문화 |
| 자동화 우선 | 반복 작업은 모두 자동화 |
| 측정 기반 | 메트릭 기반 의사결정 |

---

### 11.6 보안 통합 (DevSecOps)
**점수: ⭐⭐⭐⭐⭐ (5)**

> 보안을 개발 프로세스 초기부터 통합한다.

| 단계 | 보안 활동 |
|------|----------|
| 코드 작성 | 정적 분석 (SAST) |
| 빌드 | 의존성 취약점 스캔 |
| 배포 | 컨테이너 이미지 스캔 |
| 운영 | 동적 분석 (DAST), 모니터링 |

**도구 예시:**
- SonarQube, Snyk, Trivy, OWASP ZAP

---

## 12. 데이터베이스 설계 원칙

### 12.1 정규화 (Normalization)
**점수: ⭐⭐⭐⭐⭐ (5)**

> 데이터 중복을 최소화하고 데이터 무결성을 보장한다.

| 정규형 | 설명 | 적용 |
|--------|------|------|
| 1NF | 원자값만 허용, 반복 그룹 제거 | 필수 |
| 2NF | 부분 함수 종속 제거 | 필수 |
| 3NF | 이행 함수 종속 제거 | 권장 |
| BCNF | 모든 결정자가 후보키 | 선택적 |

| 장점 | 단점 |
|------|------|
| 데이터 일관성 | 조인 증가 |
| 저장 공간 효율 | 쿼리 복잡도 증가 |
| 업데이트 이상 방지 | 읽기 성능 저하 가능 |

**비정규화 고려 시점:**
- 읽기 중심 워크로드
- 데이터 웨어하우스
- 성능이 중요한 경우

---

### 12.2 인덱싱 전략
**점수: ⭐⭐⭐⭐⭐ (5)**

> 쿼리 성능을 위한 전략적 인덱스 설계

| 인덱스 유형 | 적합한 경우 |
|------------|------------|
| B-Tree | 범위 검색, 정렬 |
| Hash | 정확한 일치 검색 |
| Composite | 다중 컬럼 조건 |
| Covering | 자주 조회되는 컬럼 포함 |

| DO | DON'T |
|----|-------|
| WHERE, JOIN, ORDER BY 컬럼 인덱싱 | 모든 컬럼 인덱싱 |
| 선택도 높은 컬럼 우선 | 자주 변경되는 컬럼 과다 인덱싱 |
| EXPLAIN으로 분석 | 추측으로 인덱스 추가 |

**주의:**
- 인덱스 = 읽기 ↑, 쓰기 ↓
- 과도한 인덱스 = 저장공간 ↑, 유지보수 ↓

---

### 12.3 쿼리 최적화
**점수: ⭐⭐⭐⭐⭐ (5)**

| 원칙 | 설명 |
|------|------|
| SELECT 명시 | `SELECT *` 피하기 |
| 조기 필터링 | WHERE 조건 최적화 |
| 조인 최적화 | 필요한 조인만, 순서 고려 |
| 서브쿼리 주의 | 가능하면 JOIN으로 대체 |
| 페이지네이션 | LIMIT/OFFSET 또는 커서 기반 |

**분석 도구:**
- `EXPLAIN` / `EXPLAIN ANALYZE`
- Slow Query Log
- Query Profiler

---

### 12.4 데이터 무결성
**점수: ⭐⭐⭐⭐⭐ (5)**

| 제약조건 | 용도 |
|----------|------|
| PRIMARY KEY | 고유 식별자 |
| FOREIGN KEY | 참조 무결성 |
| UNIQUE | 중복 방지 |
| NOT NULL | 필수값 보장 |
| CHECK | 값 범위 제한 |

---

### 12.5 스키마 설계 원칙
**점수: ⭐⭐⭐⭐⭐ (5)**

| 원칙 | 설명 |
|------|------|
| 명확한 네이밍 | `user_id`, `created_at` 등 일관된 규칙 |
| 적절한 데이터 타입 | 저장/성능 최적화 |
| 문서화 | ERD, 스키마 설명 필수 |
| 마이그레이션 전략 | 버전 관리된 마이그레이션 |

**안티패턴:**
- EAV (Entity-Attribute-Value) 남용
- 다목적 컬럼 (JSON 남용)
- 자연키를 PK로 사용 (변경 가능성)

---

### 12.6 확장성 고려
**점수: ⭐⭐⭐⭐ (4)**

| 전략 | 설명 | 적합한 경우 |
|------|------|------------|
| 수직 확장 | 서버 성능 향상 | 초기 단계 |
| 수평 확장 | 서버 추가 | 대규모 |
| 파티셔닝 | 테이블 분할 | 대용량 테이블 |
| 샤딩 | DB 분산 | 초대규모 |
| 읽기 복제 | Read Replica | 읽기 중심 |

---

## 13. UI/UX 개발 원칙

### 13.1 핵심 UX 원칙
**점수: ⭐⭐⭐⭐⭐ (5)**

| 원칙 | 설명 |
|------|------|
| 단순성 | 최소한의 요소로 최대 효과 |
| 일관성 | 동일한 패턴과 스타일 유지 |
| 피드백 | 사용자 행동에 즉각 반응 |
| 사용자 제어 | 실행 취소, 명확한 네비게이션 |
| 오류 방지 | 실수를 미리 방지하는 설계 |

---

### 13.2 시각적 계층구조
**점수: ⭐⭐⭐⭐⭐ (5)**

> 중요도에 따라 시각적 강조를 다르게 한다.

| 요소 | 적용 방법 |
|------|----------|
| 크기 | 중요한 요소는 크게 |
| 색상 | 주요 액션에 강조 색상 |
| 대비 | 배경과 전경 명확히 구분 |
| 여백 | 그룹핑과 분리에 활용 |
| 타이포그래피 | 제목/본문 명확히 구분 |

---

### 13.3 접근성 (Accessibility) - A11Y
**점수: ⭐⭐⭐⭐⭐ (5)**

> 모든 사용자가 사용할 수 있도록 설계한다.

| 원칙 | 적용 방법 |
|------|----------|
| 색상 외 정보 전달 | 텍스트 라벨, 패턴 사용 |
| 키보드 네비게이션 | Tab 순서, 포커스 표시 |
| 스크린 리더 호환 | 시맨틱 HTML, ARIA |
| 충분한 터치 영역 | 최소 44x44px |
| 색상 대비 | WCAG 기준 4.5:1 이상 |

**WCAG 레벨:**
| 레벨 | 설명 |
|------|------|
| A | 최소 기준 |
| AA | 권장 기준 (목표) |
| AAA | 최고 수준 |

**체크리스트:**
- [ ] 모든 이미지에 alt 텍스트
- [ ] 폼 요소에 라벨 연결
- [ ] 에러 메시지 명확히 전달
- [ ] 키보드만으로 모든 기능 접근 가능

---

### 13.4 반응형 디자인 (Responsive Design)
**점수: ⭐⭐⭐⭐⭐ (5)**

> 모든 디바이스에서 최적의 경험을 제공한다.

| 원칙 | 설명 |
|------|------|
| Mobile First | 모바일부터 설계 후 확장 |
| Fluid Layout | 고정 픽셀 대신 비율 사용 |
| Breakpoints | 디바이스별 레이아웃 전환 |
| 유연한 이미지 | 컨테이너에 맞게 조절 |

**일반적인 Breakpoints:**
```
Mobile: ~576px
Tablet: 577px~992px
Desktop: 993px~
```

| DO | DON'T |
|----|-------|
| 다양한 디바이스 테스트 | 데스크탑만 고려 |
| 터치 친화적 인터랙션 | 작은 클릭 영역 |
| 콘텐츠 우선 | 장식 요소 과다 |

---

### 13.5 컴포넌트 디자인 패턴
**점수: ⭐⭐⭐⭐⭐ (5)**

> 재사용 가능하고 일관된 UI 컴포넌트를 설계한다.

| 원칙 | 설명 |
|------|------|
| 디자인 시스템 | 공통 스타일/컴포넌트 정의 |
| 일관된 버튼 | 위치, 스타일, 동작 통일 |
| 예측 가능한 인터랙션 | 관례 따르기 |
| 컴포지션 | 작은 컴포넌트 조합 |

**Atomic Design:**
```
Atoms → Molecules → Organisms → Templates → Pages
```

| 레벨 | 예시 |
|------|------|
| Atoms | 버튼, 인풋, 라벨 |
| Molecules | 검색 바, 폼 그룹 |
| Organisms | 헤더, 카드 리스트 |
| Templates | 페이지 레이아웃 |
| Pages | 실제 콘텐츠 페이지 |

---

### 13.6 성능 최적화 (UI)
**점수: ⭐⭐⭐⭐ (4)**

| 원칙 | 방법 |
|------|------|
| 초기 로드 최소화 | 코드 스플리팅, 레이지 로딩 |
| 이미지 최적화 | WebP, 적절한 크기, srcset |
| 번들 최적화 | Tree shaking, 압축 |
| 캐싱 활용 | 정적 자산 캐싱 |
| 애니메이션 | GPU 가속 (transform, opacity) |

**측정 도구:**
- Lighthouse
- Web Vitals (LCP, FID, CLS)
- Chrome DevTools

---

## 요약: 우선순위별 원칙

### 최우선 (⭐⭐⭐⭐⭐) - 항상 적용

**설계 원칙:**
1. SRP (단일 책임)
2. DIP (의존성 역전)
3. DRY (중복 금지)
4. KISS (단순하게)
5. YAGNI (불필요한 것 금지)
6. SoC (관심사 분리)

**보안:**
7. Defense in Depth (심층 방어)
8. Least Privilege (최소 권한)
9. Fail Secure (안전한 실패)
10. Input Validation (입력 검증)

**품질 & 프로세스:**
11. Fail Fast (빠른 실패)
12. 테스트 피라미드
13. 네이밍/포맷팅 컨벤션
14. PR 가이드라인
15. Git 컨벤션
16. API 하위 호환성

**CI/CD & DevOps:**
17. Continuous Integration
18. Continuous Deployment
19. Infrastructure as Code
20. DevSecOps

**데이터베이스:**
21. 정규화 (1NF~3NF)
22. 인덱싱 전략
23. 쿼리 최적화
24. 데이터 무결성

**UI/UX:**
25. 핵심 UX 원칙 (단순성, 일관성, 피드백)
26. 시각적 계층구조
27. 접근성 (A11Y)
28. 반응형 디자인
29. 컴포넌트 디자인 패턴

### 강력 권장 (⭐⭐⭐⭐) - 대부분 적용
1. OCP, LSP, ISP
2. Composition over Inheritance
3. Law of Demeter
4. Clean Architecture
5. TDD
6. Graceful Degradation
7. Circuit Breaker
8. 캐싱/Lazy Loading
9. Code Smell 인식
10. Technical Debt 관리
11. DevOps 문화 원칙
12. DB 확장성 전략
13. UI 성능 최적화

### 상황별 (⭐⭐⭐) - 필요시 적용
1. Hexagonal Architecture
2. Microservices 원칙
3. 테스트 커버리지 목표

---

## 참고 자료

### 설계 원칙
- [SOLID Principles - Medium](https://medium.com/@hlfdev/kiss-dry-solid-yagni-a-simple-guide-to-some-principles-of-software-engineering-and-clean-code-05e60233c79f)
- [Clean Architecture - Bitloops](https://bitloops.com/docs/bitloops-language/learning/software-architecture/clean-architecture)
- [Separation of Concerns - GeeksforGeeks](https://www.geeksforgeeks.org/software-engineering/separation-of-concerns-soc/)

### 보안
- [OWASP Security Principles](https://devguide.owasp.org/en/02-foundations/03-security-principles/)
- [OWASP Secure Coding Practices](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)

### 테스트 & 품질
- [Unit Testing Best Practices - Microsoft](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)
- [Code Smell - Martin Fowler](https://martinfowler.com/bliki/CodeSmell.html)
- [Code Review Checklist - Qodo](https://www.qodo.ai/blog/code-review-checklist/)

### Git & API
- [Git Branching Strategies - GeeksforGeeks](https://www.geeksforgeeks.org/git/branching-strategies-in-git/)
- [API Versioning Best Practices - Moesif](https://www.moesif.com/blog/technical/api-design/Best-Practices-for-Versioning-REST-and-GraphQL-APIs/)

### CI/CD & DevOps
- [CI/CD Best Practices - Codefresh](https://codefresh.io/learn/ci-cd/11-ci-cd-best-practices-for-devops-success/)
- [Infrastructure as Code Best Practices - Harness](https://www.harness.io/harness-devops-academy/infrastructure-as-code-best-practices)
- [CI/CD Best Practices - JetBrains](https://www.jetbrains.com/teamcity/ci-cd-guide/ci-cd-best-practices/)

### 데이터베이스
- [Database Design Best Practices - KP Infotech](https://kpinfo.tech/database-design-best-practices/)
- [SQL Query Optimization - ThoughtSpot](https://www.thoughtspot.com/data-trends/data-modeling/optimizing-sql-queries)
- [Index Design Guide - Microsoft](https://learn.microsoft.com/en-us/sql/relational-databases/sql-server-index-design-guide)

### UI/UX
- [UI/UX Design Principles - Microsoft Dynamics](https://learn.microsoft.com/en-us/dynamics365/guidance/develop/ui-ux-design-principles)
- [UI Design Principles - Figma](https://www.figma.com/resource-library/ui-design-principles/)
- [Accessibility Principles - UX Playbook](https://uxplaybook.org/articles/7-principles-for-inclusive-accesible-ux-designs)
- [Material Design Foundations](https://m3.material.io/foundations)
