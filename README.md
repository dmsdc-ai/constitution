# Software Development Constitution

모든 프로젝트에서 참고해야 할 소프트웨어 개발 원칙과 가이드라인을 정리한 헌법 문서입니다.

## 문서 구성

| 파일 | 설명 |
|------|------|
| [CONSTITUTION.md](./CONSTITUTION.md) | 전체 상세 문서 (13개 카테고리, 80+ 원칙) |
| [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) | 빠른 참조용 요약본 |

## 포함된 카테고리

### 설계 & 아키텍처
- **핵심 설계 원칙** - SOLID, DRY, KISS, YAGNI, SoC
- **아키텍처 원칙** - Clean Architecture, Hexagonal, Microservices

### 코드 품질
- **코딩 컨벤션** - 네이밍, 포맷팅, 주석 원칙
- **테스트 원칙** - TDD, 테스트 피라미드, AAA 패턴
- **코드 리뷰** - PR 가이드라인, Code Smell, Technical Debt

### 운영 & 보안
- **보안 원칙** - OWASP 기반 Defense in Depth, Least Privilege
- **에러 핸들링** - Fail Fast, Graceful Degradation, Circuit Breaker
- **성능 원칙** - Caching, Lazy Loading, 최적화 전략

### 인프라 & 프로세스
- **Git 버전 관리** - Branching Strategy, Commit Convention
- **API 설계** - REST 원칙, Backward Compatibility
- **CI/CD & DevOps** - CI/CD, IaC, DevSecOps

### 데이터 & UI
- **데이터베이스** - 정규화, 인덱싱, 쿼리 최적화
- **UI/UX** - 접근성, 반응형, 컴포넌트 디자인

## 점수 체계

| 점수 | 의미 |
|------|------|
| ⭐⭐⭐⭐⭐ (5) | 필수 - 모든 프로젝트에 적용 |
| ⭐⭐⭐⭐ (4) | 강력 권장 - 대부분의 프로젝트에 적용 |
| ⭐⭐⭐ (3) | 권장 - 상황에 따라 적용 |

## 사용법

### 새 프로젝트 시작 시
1. [CONSTITUTION.md](./CONSTITUTION.md)의 해당 섹션 검토
2. 프로젝트에 맞는 원칙 선정 및 적용

### PR/코드 리뷰 시
1. [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)의 체크리스트 활용
2. DO vs DON'T 예시 참고

### 팀 온보딩 시
1. Quick Reference로 핵심 원칙 공유
2. 상세 내용은 전체 문서 참조

## 참고 자료

- [SOLID Principles](https://medium.com/@hlfdev/kiss-dry-solid-yagni-a-simple-guide-to-some-principles-of-software-engineering-and-clean-code-05e60233c79f)
- [Clean Architecture](https://bitloops.com/docs/bitloops-language/learning/software-architecture/clean-architecture)
- [OWASP Security Principles](https://devguide.owasp.org/en/02-foundations/03-security-principles/)
- [Martin Fowler - Code Smell](https://martinfowler.com/bliki/CodeSmell.html)

## License

MIT
