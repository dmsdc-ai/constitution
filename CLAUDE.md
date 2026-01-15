# Software Development Constitution

이 저장소는 모든 프로젝트에서 참조해야 할 개발 원칙과 가이드라인을 정의합니다.

## 다른 프로젝트에서 참조하기

다른 프로젝트의 CLAUDE.md에 다음을 추가하세요:

```markdown
## 개발 헌법 참조

이 프로젝트는 [Software Development Constitution](https://github.com/dmsdc-ai/constitution)을 따릅니다.

- 전체 문서: https://github.com/dmsdc-ai/constitution/blob/main/CONSTITUTION.md
- 빠른 참조: https://github.com/dmsdc-ai/constitution/blob/main/QUICK_REFERENCE.md
```

---

## 핵심 원칙 요약

### 필수 설계 원칙 (항상 적용)

| 원칙 | 설명 |
|------|------|
| **SRP** | 클래스/함수는 하나의 책임만 |
| **DIP** | 구현이 아닌 추상화에 의존 |
| **DRY** | 중복 금지, 3번 반복시 추상화 |
| **KISS** | 단순하게, 6개월 후 이해 가능하게 |
| **YAGNI** | 지금 필요 없으면 만들지 말 것 |

### 네이밍 컨벤션

```
클래스/타입     → PascalCase      (UserService)
함수/메서드     → camelCase       (getUserById)
변수           → camelCase       (userName)
상수           → SCREAMING_SNAKE  (MAX_RETRY)
불리언         → is/has/can 접두사 (isActive)
```

### 보안 필수 사항

- **입력 검증**: 모든 외부 입력은 화이트리스트 기반 검증
- **최소 권한**: 필요한 최소한의 권한만 부여
- **안전한 실패**: 오류시 기본값은 거부

### 코드 품질

- **테스트**: Unit 70% / Integration 20% / E2E 10%
- **PR 크기**: 400줄 이하 권장
- **커밋**: Conventional Commits (feat/fix/docs/refactor/test/chore)

### Git 워크플로우

```bash
# 브랜치 생성
git checkout -b feature/기능명

# 커밋
git commit -m "feat: 새 기능 추가"

# PR 생성
gh pr create --title "feat: 새 기능" --body "설명"
```

---

## PR 전 체크리스트

```markdown
### 코드 품질
- [ ] SRP: 각 클래스/함수가 하나의 책임만?
- [ ] DRY: 중복 코드 없음?
- [ ] 네이밍 컨벤션 준수?

### 보안
- [ ] 입력값 검증됨?
- [ ] 민감정보 노출 없음?

### 테스트
- [ ] 테스트 작성 및 통과?
```

---

## 상세 문서

- [CONSTITUTION.md](./CONSTITUTION.md) - 전체 원칙 상세 설명
- [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) - 빠른 참조용 요약

## 참고

이 문서의 모든 원칙은 5점 척도로 점수화되어 있습니다:
- ⭐⭐⭐⭐⭐ (5): 필수 - 모든 프로젝트에 적용
- ⭐⭐⭐⭐ (4): 강력 권장 - 대부분 적용
- ⭐⭐⭐ (3): 권장 - 상황별 적용
