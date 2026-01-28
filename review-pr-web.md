---
name: review-pr-web
description: 웹 프로젝트 PR 리뷰. React, Next.js, TypeScript 코드의 품질, 성능, 접근성을 검토합니다.
argument-hint: <pr-number>
disable-model-invocation: true
allowed-tools: Bash(gh *), Read, Grep, Glob, WebFetch
---

# Web PR Review

React/Next.js 웹 프로젝트 PR을 리뷰합니다.

## 적용 가이드라인

1. **vercel-react-best-practices** - React/Next.js 성능 최적화
2. **vercel-composition-patterns** - 컴포넌트 합성 패턴
3. **web-design-guidelines** - UI/UX 및 접근성

## 리뷰 절차

### Step 1: PR 정보 수집

```bash
gh pr view $ARGUMENTS --json title,body,files,additions,deletions,author,baseRefName,headRefName
gh pr diff $ARGUMENTS
```

### Step 2: 가이드라인별 검토

#### Performance (vercel-react-best-practices)

| 우선순위 | 규칙 | 체크 항목 |
|----------|------|-----------|
| CRITICAL | async-parallel | Promise.all()로 병렬 처리 |
| CRITICAL | bundle-barrel-imports | barrel file 대신 직접 import |
| CRITICAL | bundle-dynamic-imports | next/dynamic 코드 스플리팅 |
| HIGH | server-parallel-fetching | 서버 컴포넌트 병렬 fetch |
| MEDIUM | rerender-derived-state-no-effect | useEffect에서 파생상태 금지 |
| MEDIUM | rerender-memo | 불필요한 리렌더링 방지 |
| MEDIUM | rendering-conditional-render | && 대신 삼항연산자 |

#### Component Architecture (vercel-composition-patterns)

| 우선순위 | 규칙 | 체크 항목 |
|----------|------|-----------|
| HIGH | architecture-avoid-boolean-props | boolean prop 3개 이상 시 variant 분리 |
| MEDIUM | architecture-compound-components | 복합 컴포넌트 패턴 |
| MEDIUM | patterns-explicit-variants | 명시적 variant 컴포넌트 |
| MEDIUM | patterns-children-over-render-props | renderX 대신 children |

#### Accessibility (web-design-guidelines)

| 우선순위 | 규칙 | 체크 항목 |
|----------|------|-----------|
| HIGH | 키보드 접근성 | onClick 있으면 onKeyDown 필요 |
| HIGH | 폼 라벨 | input에 label 또는 aria-label |
| HIGH | 아이콘 버튼 | aria-label 필수 |
| MEDIUM | 포커스 스타일 | focus-visible:ring-* |
| MEDIUM | 호버 상태 | hover: 스타일 |
| LOW | 모션 | prefers-reduced-motion 존중 |

### Step 3: 코드 품질 검토

- [ ] TypeScript 타입 정의
- [ ] 함수/컴포넌트 선언 일관성
- [ ] import 정리
- [ ] 문법 오류 (세미콜론, 들여쓰기)

### Step 4: 결과 출력

```markdown
## PR #[번호] Web Review: [제목]

**Author**: @[작성자]
**Branch**: [head] → [base]
**Changes**: +[additions] / -[deletions]

---

### Must Fix

| 파일:라인 | 규칙 | 설명 |
|-----------|------|------|

### Should Fix

| 파일:라인 | 규칙 | 설명 |
|-----------|------|------|

### Nice to Have

| 파일:라인 | 규칙 | 설명 |
|-----------|------|------|

### Good Points

- [잘된 점들]

---

**결론**: [머지 가능 여부]
```

## 심각도 기준

| 등급 | 기준 |
|------|------|
| Must Fix | 버그, 보안, 빌드에러, 문법오류 |
| Should Fix | 성능, 접근성, 안티패턴 |
| Nice to Have | 스타일, 가독성, 확장성 |

## 상세 규칙 참조

- `.claude/skills/vercel-react-best-practices/rules/`
- `.claude/skills/vercel-composition-patterns/rules/`
- `.claude/skills/web-design-guidelines/`
