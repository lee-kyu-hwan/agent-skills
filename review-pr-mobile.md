---
name: review-pr-mobile
description: 모바일 프로젝트 PR 리뷰. React Native, Expo 코드의 품질, 성능, 애니메이션을 검토합니다.
argument-hint: <pr-number>
disable-model-invocation: true
allowed-tools: Bash(gh *), Read, Grep, Glob, WebFetch
---

# Mobile PR Review

React Native/Expo 모바일 프로젝트 PR을 리뷰합니다.

## 적용 가이드라인

1. **vercel-react-native-skills** - React Native 성능 최적화
2. **vercel-composition-patterns** - 컴포넌트 합성 패턴

## 리뷰 절차

### Step 1: PR 정보 수집

```bash
gh pr view $ARGUMENTS --json title,body,files,additions,deletions,author,baseRefName,headRefName
gh pr diff $ARGUMENTS
```

### Step 2: 가이드라인별 검토

#### Animation & Performance (vercel-react-native-skills)

| 우선순위 | 규칙 | 체크 항목 |
|----------|------|-----------|
| HIGH | animation-gpu-properties | transform/opacity만 애니메이션 |
| HIGH | animation-derived-value | useDerivedValue 활용 |
| HIGH | animation-gesture-detector-press | GestureDetector로 press 처리 |
| MEDIUM | react-compiler-reanimated-shared-values | shared value 최적화 |

#### List Performance (vercel-react-native-skills)

| 우선순위 | 규칙 | 체크 항목 |
|----------|------|-----------|
| CRITICAL | list-performance-virtualize | FlatList/FlashList 사용 |
| HIGH | list-performance-item-memo | 리스트 아이템 memo |
| HIGH | list-performance-callbacks | useCallback으로 콜백 안정화 |
| MEDIUM | list-performance-inline-objects | 인라인 객체/배열 금지 |
| MEDIUM | list-performance-images | 이미지 최적화 |

#### UI Components (vercel-react-native-skills)

| 우선순위 | 규칙 | 체크 항목 |
|----------|------|-----------|
| HIGH | ui-pressable | Pressable 컴포넌트 사용 |
| HIGH | ui-expo-image | expo-image 사용 |
| MEDIUM | ui-native-modals | 네이티브 모달 활용 |
| MEDIUM | ui-safe-area-scroll | SafeArea + ScrollView |
| LOW | ui-menus | 네이티브 메뉴 활용 |

#### State Management (vercel-react-native-skills)

| 우선순위 | 규칙 | 체크 항목 |
|----------|------|-----------|
| HIGH | state-ground-truth | 단일 진실 공급원 |
| MEDIUM | react-state-minimize | 최소한의 state |
| MEDIUM | react-state-fallback | 적절한 fallback |
| MEDIUM | scroll-position-no-state | 스크롤 위치는 ref로 |

#### Rendering (vercel-react-native-skills)

| 우선순위 | 규칙 | 체크 항목 |
|----------|------|-----------|
| HIGH | rendering-no-falsy-and | && 대신 삼항연산자 (0/NaN 렌더링 방지) |
| HIGH | rendering-text-in-text-component | 텍스트는 Text 컴포넌트 내부에 |

#### Component Architecture (vercel-composition-patterns)

| 우선순위 | 규칙 | 체크 항목 |
|----------|------|-----------|
| HIGH | architecture-avoid-boolean-props | boolean prop 남용 금지 |
| MEDIUM | architecture-compound-components | 복합 컴포넌트 패턴 |
| MEDIUM | design-system-compound-components | 디자인 시스템 컴포넌트 |

#### Monorepo (vercel-react-native-skills)

| 우선순위 | 규칙 | 체크 항목 |
|----------|------|-----------|
| HIGH | monorepo-native-deps-in-app | 네이티브 의존성은 app에 |
| MEDIUM | monorepo-single-dependency-versions | 의존성 버전 통일 |

### Step 3: 코드 품질 검토

- [ ] TypeScript 타입 정의
- [ ] 함수/컴포넌트 선언 일관성
- [ ] import 정리
- [ ] 문법 오류

### Step 4: 결과 출력

```markdown
## PR #[번호] Mobile Review: [제목]

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
| Must Fix | 크래시, 메모리 릭, 빌드에러, 문법오류 |
| Should Fix | 성능, 애니메이션 jank, 안티패턴 |
| Nice to Have | 스타일, 가독성, 확장성 |

## 상세 규칙 참조

- `.claude/skills/vercel-react-native-skills/rules/`
- `.claude/skills/vercel-composition-patterns/rules/`
