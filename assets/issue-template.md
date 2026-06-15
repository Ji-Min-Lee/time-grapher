# Issue Template / 이슈 템플릿

## 필수 항목 / Required Fields

| 필드 / Field | 필수 / Required | 설명 / Description |
|---|---|---|
| Title | ✅ | `[PREFIX-N] 짧은 설명` 형식 준수 |
| Body | ✅ | 아래 템플릿 구조 사용 |
| Status | ✅ | Sprint Backlog / Todo / In Progress / Done |
| Start Date | ✅ | `YYYY-MM-DD` |
| End Date | ✅ | `YYYY-MM-DD` |
| Labels | ✅ | 최소: 마일스톤(M1/M2/M3) + 스프린트(wX-Y) |
| Assignees | ✅ | 최소 1명 |

---

## 실험 태스크 템플릿 / Experiment Task Template

**제목**: `[EXP-NN] 실험 이름`

```markdown
**Sprint**: wX-Y (MM/DD–DD) | **Team**: Team N | **QA**: QAS-N 속성명

## Objective
실험을 통해 검증하려는 가설 또는 목표를 1-2문장으로 기술.

## Steps
- [ ] 단계 1
- [ ] 단계 2
- [ ] 단계 3

## Pass Criteria
| 항목 / Item | 기준 / Target |
|---|---|
| 지표 | 목표값 |

## Output
- 결과 → experiment-results.md §EXP-NN
```

**라벨**: `experiment`, `M2`, `wX-Y`, `teamN`, `QAS-N`

---

## 아키텍처 태스크 템플릿 / Architecture Task Template

**제목**: `[ARCH] 결정 제목`

```markdown
**Sprint**: wX-Y (MM/DD–DD) | **Team**: Team N | **Tactic**: 전술명

## Context
결정이 필요한 배경과 현재 상황.

## Decision Required
- [ ] 옵션 A 분석
- [ ] 옵션 B 분석
- [ ] ADD 기반 결정 및 문서화

## Acceptance Criteria
- ASR 추적 가능
- docs/에 결정 기록

## Output
- ADR → docs/architecture/decisions/
```

**라벨**: `architecture`, `M2`, `wX-Y`

---

## 팀 태스크 템플릿 / Team Task Template

**제목**: `[P2-TN] 태스크 설명`

```markdown
**Sprint**: wX-Y (MM/DD–DD) | **Team**: Team N | **QA**: QAS-N 속성명

## Objective
이 태스크의 목표.

## Steps
- [ ] 단계 1
- [ ] 단계 2

## Output
- 결과물 또는 확인 방법
```

**라벨**: `M2`, `wX-Y`, `teamN`, `QAS-N`

---

## 문서 태스크 템플릿 / Doc Task Template

**제목**: `[DOC] 문서 이름`

```markdown
**Sprint**: wX-Y (MM/DD–DD) | **Team**: Team N

## Scope
작성 또는 업데이트할 문서 목록.

## Steps
- [ ] 초안 작성
- [ ] 한/영 bilingual 규칙 적용 (conventions.md 참조)
- [ ] 리뷰 반영

## Output
- `docs/경로/파일명.md`
```

**라벨**: `documentation`, `M2`, `wX-Y`

---

## 버그 템플릿 / Bug Template

**제목**: `[BUG] 버그 설명`

```markdown
**Sprint**: wX-Y | **Severity**: High / Medium / Low

## Reproduce
1. 재현 단계

## Expected
기대 동작.

## Actual
실제 동작.

## Fix Plan
- [ ] 원인 분석
- [ ] 수정
- [ ] 회귀 테스트
```

**라벨**: `bug`, `M2`, `wX-Y`, `teamN`
