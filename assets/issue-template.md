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
| Assignees | ✅ | 최소 1명 — 아직 배정 안 됐으면 생성 후 별도 `gh issue edit`으로 추가 |

## 선택 항목 / Optional Fields (body 헤더에 추가)

| 항목 / Item | 형식 / Format | 사용 시점 |
|---|---|---|
| ADD Decision | `**ADD Decision**: ADD-X-NN (전술명)` | 이슈가 특정 ADD 결정과 연결될 때 |
| Milestone (body) | `**Milestone**: M3` | 미래 마일스톤 이슈 (labels만으로 부족할 때) |
| Status (body) | `**Status**: Done` | Done 이슈 아카이브 마킹 |

---

## 이슈 타입별 템플릿 / Templates by Type

### 실험 태스크 / Experiment Task — `[EXP-NN]`

```markdown
**Sprint**: wX-Y (MM/DD–DD) | **Team**: Team N | **QA**: QAS-N 속성명
**ADD Decision**: ADD-X-NN (전술명)   ← optional, 해당 시만

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

## Dependency          ← optional, 블로킹 이슈가 있을 때만
Blocked by #이슈번호 결과

## Output
- 결과 → experiment-results.md §EXP-NN
```

**라벨**: `experiment`, `M2`, `wX-Y`, `teamN`, `QAS-N`

---

### 기능 구현 태스크 / Feature Task — `[FR-NN]`

```markdown
**Sprint**: wX-Y (MM/DD–DD) | **Team**: Team N | **QA**: QAS-N 속성명
**Milestone**: M3   ← optional, M3 이슈인 경우

## Objective
이 기능의 목표.

## Scope
- 구현 범위 항목 1
- 구현 범위 항목 2
- 지켜야 할 계약/제약 (예: Pause contract 위반 금지)

## Dependency          ← optional
Blocked by #이슈번호 결과

## Output
- 구현 완료 확인 방법 또는 연결 문서
```

**라벨**: `M2` or `M3`, `wX-Y`, `teamN`, `QAS-N`

---

### 아키텍처 태스크 / Architecture Task — `[ARCH]`

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

### 팀 태스크 / Team Task — `[P2-TN]` / `[P3-TN]`

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

### 문서 태스크 / Doc Task — `[M2-DOC]` / `[DOC]`

```markdown
**Sprint**: wX-Y (MM/DD–DD) | **Team**: All | **M2 Documentation**

## Objective
작성 또는 업데이트할 문서와 목표.

## Contents
- [ ] 항목 1
- [ ] 항목 2
- [ ] 한/영 bilingual 규칙 적용 (conventions.md 참조)

## Output
- `docs/경로/파일명.md`
```

**라벨**: `documentation`, `M2`, `wX-Y`, `all-teams`

---

### 버그 템플릿 / Bug — `[BUG]`

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

---

### 완료 아카이브 이슈 / Done Archive Issue — `[P1]`

Done 상태로 소급 기록하는 이슈 (스프린트 완료 후 회고용).

```markdown
**Sprint**: wX-Y (MM/DD–DD) | **Team**: Team N | **QA**: QAS-N 속성명
**Status**: Done

## What Was Done
- 완료된 작업 요약 (과거형)
- 적용한 전술/패턴

## Result
핵심 결과 수치 또는 확인 사항
```

**라벨**: `M2`, `wX-Y`, `teamN`, `QAS-N`

---

## 이슈 제목 규칙 / Title Convention

```
[PREFIX-N] 짧은 설명
```

| Prefix | 용도 |
|---|---|
| `EXP-NN` | 실험 태스크 (e.g. EXP-01) |
| `FR-NN` | 기능 구현 태스크 |
| `P1` / `P2-TN` / `P3-TN` | Phase별 팀 태스크 |
| `M2-DOC` / `DOC` | 문서 작업 |
| `ARCH` | 아키텍처 결정 태스크 |
| `BUG` | 버그 수정 |
| `M2` / `M3` | 마일스톤 단위 제출/리뷰 태스크 |

## 라벨 규칙 / Label Convention

| 라벨 / Label | 의미 |
|---|---|
| `M1` / `M2` / `M3` | 마일스톤 |
| `w1-1`, `w2-1`, `w3-1` … | 스프린트 주차 |
| `team1` / `team2` | 담당 팀 |
| `all-teams` | 전체 팀 참여 (DOC 등) — `teamN` 대신 사용 |
| `QAS-1` … `QAS-5` | 연관 품질 속성 시나리오 (복수 가능) |
| `experiment` | 실험 태스크 |
| `architecture` | 아키텍처 결정 |
| `documentation` | 문서 태스크 |
| `bug` | 버그 수정 |
