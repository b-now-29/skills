---
name: scaffold-exercises
description: 린트를 통과하는 섹션, 문제, 해답, 설명을 포함하는 연습 문제 디렉터리 구조를 생성합니다. 사용자가 연습 문제의 뼈대를 만들거나, 연습 문제 스텁을 생성하거나, 새로운 강좌 섹션을 설정하고자 할 때 사용합니다.
---

# 연습 문제 뼈대 생성

`pnpm ai-hero-cli internal lint`를 통과하는 연습 문제 디렉터리 구조를 생성한 다음, `git commit`으로 커밋합니다.

## 디렉터리 명명 규칙

- **섹션**: `exercises/` 내부의 `XX-section-name/` (예: `01-retrieval-skill-building`)
- **연습 문제**: 섹션 내부의 `XX.YY-exercise-name/` (예: `01.03-retrieval-with-bm25`)
- 섹션 번호 = `XX`, 연습 문제 번호 = `XX.YY`
- 이름은 dash-case(소문자, 하이픈)입니다

## 연습 문제 변형

각 연습 문제에는 다음 하위 폴더 중 하나 이상이 필요합니다.

- `problem/`: TODO가 포함된 학생용 작업 공간
- `solution/`: 참조 구현
- `explainer/`: 개념 자료, TODO 없음

스텁을 만들 때는 계획에서 달리 지정하지 않는 한 `explainer/`를 기본으로 하십시오.

## 필수 파일

각 하위 폴더(`problem/`, `solution/`, `explainer/`)에는 다음 조건을 만족하는 `readme.md`가 필요합니다.

- **비어 있지 않음** (실제 내용이 있어야 하며, 제목 한 줄만 있어도 됩니다)
- 깨진 링크가 없음

스텁을 만들 때는 제목과 설명이 포함된 최소한의 readme를 생성하십시오.

```md
# Exercise Title

Description here
```

하위 폴더에 코드가 있다면 `main.ts`(1줄 초과)도 필요합니다. 그러나 스텁의 경우 readme만 있는 연습 문제도 괜찮습니다.

## 워크플로

1. **계획 파싱**: 섹션 이름, 연습 문제 이름, 변형 유형을 추출합니다
2. **디렉터리 생성**: 각 경로에 대해 `mkdir -p`를 실행합니다
3. **스텁 readme 생성**: 변형 폴더마다 제목이 포함된 `readme.md`를 하나씩 생성합니다
4. **린트 실행**: `pnpm ai-hero-cli internal lint`로 검증합니다
5. **오류 수정**: 린트가 통과할 때까지 반복합니다

## 린트 규칙 요약

린터(`pnpm ai-hero-cli internal lint`)는 다음을 검사합니다.

- 각 연습 문제에 하위 폴더(`problem/`, `solution/`, `explainer/`)가 있음
- `problem/`, `explainer/`, `explainer.1/` 중 하나 이상이 존재함
- 주 하위 폴더에 `readme.md`가 존재하며 비어 있지 않음
- `.gitkeep` 파일이 없음
- `speaker-notes.md` 파일이 없음
- readme에 깨진 링크가 없음
- readme에 `pnpm run exercise` 명령이 없음
- readme만 있는 경우가 아니라면 하위 폴더마다 `main.ts`가 필요함

## 연습 문제 이동/이름 변경

연습 문제의 번호를 다시 매기거나 이동할 때:

1. 디렉터리 이름을 변경할 때는 `mv`가 아니라 `git mv`를 사용하십시오. git 이력이 보존됩니다
2. 순서를 유지하도록 숫자 접두사를 업데이트하십시오
3. 이동 후 린트를 다시 실행하십시오

예시:

```bash
git mv exercises/01-retrieval/01.03-embeddings exercises/01-retrieval/01.04-embeddings
```

## 예시: 계획으로부터 스텁 생성

다음과 같은 계획이 주어졌다고 가정합니다.

```
Section 05: Memory Skill Building
- 05.01 Introduction to Memory
- 05.02 Short-term Memory (explainer + problem + solution)
- 05.03 Long-term Memory
```

다음을 생성합니다.

```bash
mkdir -p exercises/05-memory-skill-building/05.01-introduction-to-memory/explainer
mkdir -p exercises/05-memory-skill-building/05.02-short-term-memory/{explainer,problem,solution}
mkdir -p exercises/05-memory-skill-building/05.03-long-term-memory/explainer
```

그런 다음 readme 스텁을 생성합니다.

```
exercises/05-memory-skill-building/05.01-introduction-to-memory/explainer/readme.md -> "# Introduction to Memory"
exercises/05-memory-skill-building/05.02-short-term-memory/explainer/readme.md -> "# Short-term Memory"
exercises/05-memory-skill-building/05.02-short-term-memory/problem/readme.md -> "# Short-term Memory"
exercises/05-memory-skill-building/05.02-short-term-memory/solution/readme.md -> "# Short-term Memory"
exercises/05-memory-skill-building/05.03-long-term-memory/explainer/readme.md -> "# Long-term Memory"
```
