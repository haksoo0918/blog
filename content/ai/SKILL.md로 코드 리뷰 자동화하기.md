---
tags:
  - antigravity
  - ai
  - skill
  - review
---

Google Antigravity 환경에서 에이전트에게 특정 역할과 가이드라인을 부여하는 핵심 도구가 바로 **`SKILL.md`** 파일입니다.

Codelab 튜토리얼에 소개된 '코드 검토 스킬(Code Review Skill)'을 바탕으로, 파일의 구조부터 한글 해석, 그리고 효율적인 전역(Global) 설정 방법까지 정리해 드립니다.

## 1. `SKILL.md`란 무엇인가?

`SKILL.md`는 AI 에이전트가 특정 작업을 수행할 때 따라야 할 **지침, 평가 기준, 출력 형식을 정의하는 프롬프트 규격 서식**입니다.

### 코드 검토 `SKILL.md` 번역

다음은 [[#참조]]에 있는 `SKILL.md` 파일 내용입니다.

```md
---
name: code-review
description: Reviews code changes for bugs, style issues, and best practices. Use when reviewing PRs or checking code quality.
---

# Code Review Skill

When reviewing code, follow these steps:

## Review checklist

1. **Correctness**: Does the code do what it's supposed to?
2. **Edge cases**: Are error conditions handled?
3. **Style**: Does it follow project conventions?
4. **Performance**: Are there obvious inefficiencies?
   
## How to provide feedback

- Be specific about what needs to change
- Explain why, not just what
- Suggest alternatives when possible
```

다음은 위 내용을 한글로 번역한 내용입니다.

```md
---
name: code-review
description: 버그, 스타일 문제 및 모범 사례(Best Practice) 관점에서 코드 변경 사항을 검토합니다. PR(Pull Request)을 검토하거나 코드 품질을 확인할 때 사용합니다.
---

# 코드 검토 스킬 (Code Review Skill)

코드를 검토할 때 다음 단계를 따르십시오.

## 검토 체크리스트 (Review checklist)

1. **정확성 (Correctness):** 코드가 의도한 대로 정확히 동작하는가?
2. **경계 조건 (Edge cases):** 예외 및 에러 상황이 제대로 처리되어 있는가?
3. **스타일 (Style):** 프로젝트의 코딩 컨벤션을 따르고 있는가?
4. **성능 (Performance):** 명백한 비효율성 요소가 존재하는가?

## 피드백 제공 방식 (How to provide feedback)

- 수정이 필요한 부분을 구체적으로 명시하십시오.
- 단순한 수정 요청(What)을 넘어 그 이유(Why)를 설명하십시오.
- 가능한 경우 대안을 제시하십시오.
```

추가로 한글로 된 결과물을 받고 싶어 아래와 같은 내용을 첨부했습니다.

```md
# Language Instruction

Please write the final review output in Korean.
```

## 2. 스킬 등록 및 관리 방식 (전역 vs 프로젝트)

`SKILL.md` 파일은 **전역(Global) 폴더**에 배치하거나 **개별 프로젝트 폴더**에 배치할 수 있습니다.

### 추천하는 스킬 관리 패턴 (Best Practice)

- **기본 전략:** 보편적인 코드 검토 규칙은 **전역 설정**에 한 번만 등록해 두고 모든 프로젝트에서 공유하여 사용합니다.
- **예외 전략:** 특정 프로젝트 고유의 컨벤션이나 프레임워크 전용 규칙이 필요해지는 시점에만 해당 **프로젝트 폴더**에 별도의 `SKILL.md`를 추가합니다. (프로젝트 설정이 전역 설정보다 우선 적용됩니다.)

### 스킬 배치 경로

- **전역(Global) 스킬 경로:**

```
~/.gemini/config/skills/code-review/SKILL.md
```

- **프로젝트(Project) 스킬 경로:**

```
<project-root>/.agents/skills/code-review/SKILL.md
```

## 3. 실전 활용 방법

`~/.gemini/config/skills/`에 등록된 전역 스킬은 **Antigravity 앱, Antigravity IDE, Antigravity CLI 구분 없이 동일하게 적용**됩니다.

### ① 직접 호출하기 (`@` 및 파일 지정)

채팅창에서 스킬 이름을 명시적으로 언급하며 대상을 지정합니다.

> `@code-review 스킬을 활용해서 src/auth/login.ts 파일 검토해 줘.`
> `메인 브랜치 대비 새로 변경된 파일들 @code-review 해 줘.`

### ② 자연어로 자동 감지 활용

스킬에 기재된 `description`을 바탕으로 에이전트가 자동 감지하여 처리합니다.

> `방금 작성한 코드 보안 및 성능 관점에서 리뷰해 줘.`

## 한 줄 요약

전역 경로(`~/.gemini/config/skills/`)에 보편적인 표준 검토 규칙을 한 번 등록해 두면, 어떤 프로젝트나 Antigravity 제품군에서든 곧바로 일관된 고품질의 코드 리뷰를 받을 수 있습니다.

---

## 참조

- https://codelabs.developers.google.com/getting-started-google-antigravity?hl=ko#8