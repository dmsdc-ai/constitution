# 개발 헌법 Quick Reference

> 빠른 참조를 위한 핵심 원칙 요약본 | [전체 문서 보기](./CONSTITUTION.md)

---

## 목차 (Quick Navigation)

| 카테고리 | 바로가기 |
|---------|---------|
| 설계 원칙 | [SOLID](#-solid-원칙) · [기본 원칙](#-기본-원칙) |
| 아키텍처 | [아키텍처](#-아키텍처) |
| 코드 품질 | [컨벤션](#-코딩-컨벤션) · [테스트](#-테스트) · [리뷰](#-코드-리뷰) |
| 운영 | [보안](#-보안) · [에러처리](#-에러-핸들링) · [성능](#-성능) |
| 인프라 | [Git](#-git--버전관리) · [API](#-api-설계) · [CI/CD](#-cicd--devops) |
| 데이터 | [DB 설계](#-데이터베이스) |
| 프론트엔드 | [UI/UX](#-uiux) |

---

## 핵심 원칙 한눈에 보기

### 🏗 SOLID 원칙

| 원칙 | 한 줄 요약 |
|------|-----------|
| **SRP** | 클래스는 하나의 책임만, 변경 이유도 하나만 |
| **OCP** | 확장에 열림, 수정에 닫힘 |
| **LSP** | 자식은 부모를 대체할 수 있어야 함 |
| **ISP** | 사용하지 않는 인터페이스에 의존하지 말 것 |
| **DIP** | 구현이 아닌 추상화에 의존할 것 |

### 📐 기본 원칙

| 원칙 | 한 줄 요약 |
|------|-----------|
| **DRY** | 중복 금지, 3번 반복되면 추상화 |
| **KISS** | 단순하게, 6개월 후 이해할 수 있게 |
| **YAGNI** | 지금 필요 없으면 만들지 말 것 |
| **SoC** | 관심사를 분리하여 모듈화 |
| **LoD** | 직접 관련된 객체하고만 대화 |

### 🏛 아키텍처

| 원칙 | 적용 |
|------|------|
| **Clean Architecture** | 의존성은 항상 안쪽(비즈니스)으로 |
| **Loose Coupling** | 모듈 간 최소 의존성 |
| **High Cohesion** | 관련 기능은 함께 |

### 📝 코딩 컨벤션

```
클래스/타입     → PascalCase      (UserService)
함수/메서드     → camelCase       (getUserById)
변수           → camelCase       (userName)
상수           → SCREAMING_SNAKE  (MAX_RETRY)
불리언         → is/has/can 접두사 (isActive)
```

### 🔒 보안

| 원칙 | 한 줄 요약 |
|------|-----------|
| **Defense in Depth** | 여러 계층의 보안 적용 |
| **Least Privilege** | 필요한 최소 권한만 부여 |
| **Fail Secure** | 오류시 안전한 상태로 (기본=거부) |
| **Input Validation** | 모든 외부 입력 검증 (화이트리스트) |

### 🧪 테스트

```
테스트 피라미드:
    /\        E2E (10%)
   /  \       Integration (20%)
  /    \      Unit (70%)
 --------

패턴: Arrange → Act → Assert
이름: should_returnError_when_userNotFound
```

### ⚠️ 에러 핸들링

| 원칙 | 적용 |
|------|------|
| **Fail Fast** | 문제 발생시 즉시 알림 |
| **Graceful Degradation** | 일부 실패해도 핵심 기능 유지 |
| **Circuit Breaker** | 연속 실패시 요청 차단 |

### ⚡ 성능

| 원칙 | 적용 |
|------|------|
| **측정 먼저** | 추측 금지, 프로파일링 후 최적화 |
| **Lazy Loading** | 필요할 때 로드 (N+1 주의) |
| **Caching** | 비싼 연산만, TTL 필수 |

### 🔀 Git & 버전관리

**Commit Convention:**
```
feat: 새 기능
fix: 버그 수정
docs: 문서
refactor: 리팩토링
test: 테스트
chore: 빌드/설정
```

**Branching:** GitHub Flow (빠른 배포) / GitFlow (정기 릴리스)

### 🔌 API 설계

| DO | DON'T |
|----|-------|
| 자원 기반 URL `/users/{id}` | 동사 URL `/getUser` |
| HTTP 메서드 활용 | GET으로 수정 |
| 필드 추가 (additive) | 필드 제거 (breaking) |
| Deprecation 경고 | 갑작스러운 변경 |

### 🚀 CI/CD & DevOps

```
Pipeline: Build → Test → Security → Deploy(Staging) → Test → Deploy(Prod)
```

| 원칙 | 적용 |
|------|------|
| **IaC** | 인프라를 코드로, Git으로 관리 |
| **DevSecOps** | 보안을 초기부터 통합 |
| **자동 롤백** | 배포 실패시 자동 복구 |

### 🗄 데이터베이스

| 원칙 | 적용 |
|------|------|
| **정규화** | 1NF~3NF 적용, 필요시 비정규화 |
| **인덱싱** | WHERE/JOIN/ORDER BY 컬럼만 |
| **쿼리** | SELECT * 금지, EXPLAIN 분석 |

### 🎨 UI/UX

| 원칙 | 적용 |
|------|------|
| **단순성** | 최소 요소로 최대 효과 |
| **일관성** | 동일 패턴/스타일 유지 |
| **접근성** | WCAG AA, 44x44px 터치 |
| **반응형** | Mobile First |

---

## PR 전 체크리스트

### 코드 품질
- [ ] SRP: 각 클래스/함수가 하나의 책임만?
- [ ] DRY: 중복 코드 없음?
- [ ] KISS: 불필요한 복잡성 없음?
- [ ] 네이밍 컨벤션 준수?

### 보안
- [ ] 입력값 검증됨?
- [ ] 민감정보 노출 없음?
- [ ] SQL Injection/XSS 방지?

### 테스트
- [ ] 단위 테스트 작성?
- [ ] 엣지 케이스 테스트?
- [ ] 테스트 통과?

### 성능
- [ ] N+1 쿼리 없음?
- [ ] 불필요한 API 호출 없음?

---

## 빠른 참조: DO vs DON'T

### 설계
```
❌ user.getAddress().getCity().getName()
✅ user.getCityName()

❌ class Duck extends FlyingBird extends SwimmingBird
✅ class Duck { flyBehavior: IFly, swimBehavior: ISwim }

❌ UserService (CRUD + 이메일 + 로깅)
✅ UserService + EmailService + LogService
```

### 코드
```
❌ // i를 1 증가
   i++;
✅ // 재시도 횟수 제한: 무한루프 방지 목적
   const MAX_RETRIES = 3;

❌ function proc(d, f, t) { ... }
✅ function processOrder(data, fromDate, toDate) { ... }
```

### DB
```
❌ SELECT * FROM users WHERE ...
✅ SELECT id, name, email FROM users WHERE ...

❌ 모든 컬럼에 인덱스
✅ WHERE/JOIN/ORDER BY 컬럼만 인덱싱
```

### API
```
❌ GET /getUsers, POST /createUser
✅ GET /users, POST /users

❌ 기존 필드 삭제
✅ 필드 추가 + deprecated 표시
```

---

## 점수 범례

| 점수 | 의미 | 적용 |
|------|------|------|
| ⭐⭐⭐⭐⭐ | 필수 | 모든 프로젝트 |
| ⭐⭐⭐⭐ | 강력 권장 | 대부분 |
| ⭐⭐⭐ | 권장 | 상황별 |

---

> 📖 상세 내용은 [CONSTITUTION.md](./CONSTITUTION.md) 참조
