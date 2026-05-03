# 한국어 스킬

> AI 코딩 에이전트를 위한 한국어 스킬 모음

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/skills-3-green.svg)](#스킬)

**[English](./README_EN.md)** 🇺🇸

Claude Code, Cursor, Windsurf 등 Agent Skills 형식을 지원하는 AI 코딩 에이전트에서 사용할 수 있는 한국어 특화 스킬을 제공합니다.

## 빠른 시작

### 전체 스킬 설치

```bash
npx skills add daleseo/korean-skills
```

### 특정 스킬만 설치

```bash
npx skills add daleseo/korean-skills@humanizer
npx skills add daleseo/korean-skills@grammar-checker
npx skills add daleseo/korean-skills@style-guide
```

## Claude Code 플러그인

[Claude Code 플러그인](https://code.claude.com/docs/en/discover-plugins) 형태로도 설치할 수 있습니다.

먼저 마켓플레이스를 추가합니다.

```
/plugin marketplace add daleseo/korean-skills
```

그다음 플러그인을 설치합니다.

```
/plugin install korean-skills@korean-skills
```

설치하면 다음 슬래시 명령어로 각 스킬을 호출할 수 있습니다.

| 슬래시 명령어 | 설명 |
|---|---|
| `/korean-skills:humanizer` | AI가 생성한 한국어 텍스트의 패턴을 감지하고 자연스럽게 교정 |
| `/korean-skills:grammar-checker` | 한국어 문법, 맞춤법, 띄어쓰기, 구두점 검사 |
| `/korean-skills:style-guide` | 한국어 문서의 스타일 일관성 점검 |

## GitHub CLI

[GitHub CLI](https://cli.github.com/)의 `gh skill` (프리뷰) 명령어로도 설치할 수 있습니다.

```bash
# 현재 프로젝트에 Claude Code용으로 모든 스킬 설치
gh skill install daleseo/korean-skills --agent claude-code

# 사용자 전역 범위로 설치 (어디서든 사용 가능)
gh skill install daleseo/korean-skills --agent claude-code --scope user

# 특정 스킬만 설치
gh skill install daleseo/korean-skills humanizer --agent claude-code

# 특정 릴리스에 고정 (업데이트 시 자동 갱신되지 않음)
gh skill install daleseo/korean-skills --pin v1.0.0 --agent claude-code

# 설치 전 미리보기
gh skill preview daleseo/korean-skills
```

`--agent`는 Claude Code 외에도 Cursor, Codex, Gemini CLI, GitHub Copilot 등 다양한 호스트를 지원합니다. 전체 목록은 `gh skill install --help`로 확인하세요.

## 릴리스

`.claude-plugin/plugin.json#version`이 `main`에서 변경될 때마다 시맨틱 버전 태그로 자동 릴리스됩니다. 전체 목록은 [github.com/DaleSeo/korean-skills/releases](https://github.com/DaleSeo/korean-skills/releases)에서 확인할 수 있습니다.

| 설치 경로 | 받는 내용 |
|---|---|
| `gh skill install daleseo/korean-skills <name>` | 가장 최근 태그 릴리스 |
| `gh skill install daleseo/korean-skills <name> --pin v1.0.0` | 특정 릴리스 고정 (자동 업데이트 제외) |
| `npx skills add daleseo/korean-skills@<name>` | `main` 최신 콘텐츠 (태그 없음) |
| Claude Code 플러그인 (`/plugin install`) | 최신 플러그인 버전 |

안정성이 필요하면 `gh skill install … --pin vX.Y.Z`로 고정하세요. 고정된 스킬은 `gh skill upgrade` 대상에서 제외되므로 의도적으로만 업그레이드됩니다. 최신 콘텐츠가 필요하면 다른 경로들이 `main` HEAD를 그대로 추적합니다.

## 스킬 목록

### [humanizer](skills/humanizer)

AI가 생성한 한국어 텍스트를 자연스러운 인간의 글쓰기로 변환

**주요 기능:**

- 6개 카테고리 40가지 검출 패턴 (S1/S2/S3 심각도 + A~D 자연도 등급)
- KatFishNet 논문 기반 (94.88% AUC) + 커뮤니티 검증 경험적 패턴
- 의미와 격식 수준 보존

**검출 카테고리:**

- 문장부호 (7가지) - 94.88% AUC
- 띄어쓰기 (3가지) - 79.51% AUC
- 품사 다양성 (3가지) - 82.99% AUC
- 어휘 (10가지) - 대명사/지시관형사 과다, 주어 생략 미흡, AI 결말 표현(결론적으로), hype 어휘 군집(혁신적/압도적), `~적 N` 추상 체인(전략적 함의)
- 문장 구조 (4가지)
- 번역투 (13가지) - 조사 번역투(에 대해/통해/있어서), 동사 잉여(가지고 있다), 피동 남용(되어진다/에 의해), 가능 표현 남발(할 수 있다), 미래 단정(~것이다 남발)

**언제 활성화되나요?**

- 한국어 텍스트를 자연스럽게 만들 때
- `/humanizer` 명령어 사용 시
- AI가 생성한 한국어 콘텐츠 작업 시

**예시:**

```
수정 전 (AI): 인공지능 기술의 발전은 빠르게 진행되고 있으며, 다양한 산업 분야에 적용되고 있습니다.
수정 후:      인공지능 기술은 빠르게 발전하고 있으며 여러 산업 분야에 적용되고 있습니다.
```

**사용법:**

```
/humanizer

[자연스럽게 만들 한국어 텍스트 붙여넣기]
```

```bash
npx skills add daleseo/korean-skills@humanizer
```

📖 **[전체 문서 → SKILL.md](./skills/humanizer/SKILL.md)**

**참고 자료:**

- 📄 [KatFishNet 논문](https://arxiv.org/abs/2503.00032v4)
- 📁 [패턴 참조 문서](./skills/humanizer/references/)
- 🌐 [영어 버전](https://github.com/blader/humanizer) | [중국어 버전](https://github.com/op7418/Humanizer-zh)

---

### [grammar-checker](skills/grammar-checker)

표준 한국어 규칙에 기반한 문법, 맞춤법, 띄어쓰기, 구두점 검사기

**주요 기능:**

- 우선순위가 있는 4가지 오류 카테고리
- 각 오류에 대한 교육적 설명
- 문맥을 고려한 교정 (격식체/비격식체)
- 확신도 표시 (확실한 오류 vs 권장 사항)

**오류 카테고리:**

1. 맞춤법/철자 (최고 우선순위) - 되/돼, -ㄴ지/-는지 등
2. 띄어쓰기 (높은 우선순위) - 의존명사, 보조용언, 단위명사
3. 문법 구조 (중간 우선순위) - 조사, 어미 사용
4. 구두점 (낮은 우선순위) - 쉼표, 느낌표

**언제 활성화되나요?**

- 한국어 텍스트 문법 검사 시
- `/grammar-checker` 명령어 사용 시
- 한국어 문서 검토 시

**예시:**

```
수정 전: 이 프로젝트는 사용자들에게 더나은 경험을 제공하기위해 시작되요.
수정 후: 이 프로젝트는 사용자들에게 더 나은 경험을 제공하기 위해 시작됐어요.
```

**사용법:**

```
/grammar-checker

[검사할 한국어 텍스트 붙여넣기]
```

```bash
npx skills add daleseo/korean-skills@grammar-checker
```

📖 **[전체 문서 → SKILL.md](./skills/grammar-checker/SKILL.md)**

**참고 자료:**

- 📁 [문법 규칙 참조](./skills/grammar-checker/references/rules.md)
- 📁 [흔한 오류 참조](./skills/grammar-checker/references/common-errors.md)
- 📋 [예시 파일](./skills/grammar-checker/examples/)

---

### [style-guide](skills/style-guide)

문서 내부 또는 프로젝트 전체에서 일관된 작성 스타일을 유지하도록 돕는 검사기

**주요 기능:**

- 7가지 일관성 검사 카테고리
- 다층적 권위 출처 (정부 표준, 학술 지침, 실무 가이드)
- 문맥을 고려한 제안 (문서 타입: 비즈니스/학술/기술/마케팅)
- 다수결 원칙으로 충돌하는 스타일 해결

**검사 카테고리:**

1. 어조 및 격식 (최고 우선순위) - 경어체/반말 혼용, 주어 불일치
2. 용어 통일 (높은 우선순위) - 동일 개념 다른 표현, 외래어 표기
3. 숫자 및 단위 (중간 우선순위) - 아라비아/한글 숫자, 단위 띄어쓰기
4. 목록 구조 (중간 우선순위) - 목록 부호, 종결어미 일관성
5. 인용 및 강조 (낮은 우선순위) - 따옴표 스타일, 굵게/기울임
6. 날짜 및 시간 (낮은 우선순위) - 날짜 형식, 12/24시간제
7. 링크 및 참조 (낮은 우선순위) - 링크 텍스트, 인용 형식

**언제 활성화되나요?**

- 여러 작성자가 참여한 문서 검토 시
- `/style-guide` 명령어 사용 시
- 프로젝트 전체 용어 표준 유지 시
- 브랜드 일관성을 위한 공식 문서 준비 시

**예시:**

```
불일치: 사용자는 화면을 확인합니다. 유저가 페이지 설정을 변경해요.
일관됨: 사용자는 화면을 확인합니다. 사용자가 화면 설정을 변경합니다.
```

**사용법:**

```
/style-guide

[스타일 일관성을 검사할 한국어 문서 붙여넣기]
```

```bash
npx skills add daleseo/korean-skills@style-guide
```

📖 **[전체 문서 → SKILL.md](./skills/style-guide/SKILL.md)**

**참고 자료:**

- 📁 [권위 표준 참조](./skills/style-guide/references/)
  - 정부 표준: 국립국어원 공문서 작성 지침
  - 학술 표준: 대학 학위논문 작성 지침
  - 실무 표준: Kakao Enterprise 기술문서 가이드
- 📋 [예시 파일](./skills/style-guide/examples/)

## 권장 워크플로: 3-스킬 파이프라인

한국어 글쓰기를 종합적으로 검토하려면 세 스킬을 순차로 적용하세요.

```
1. /humanizer       # AI 티 제거 (가장 큰 변경 — 먼저 적용)
2. /grammar-checker # 맞춤법·띄어쓰기·문법 (humanizer 출력 검토)
3. /style-guide     # 문서 일관성 (용어·어조·포맷)
```

**순서가 중요한 이유**: humanizer가 문장을 크게 바꾸므로 안정된 출력에 대해 grammar-checker가 의미 있는 검사를 합니다. style-guide는 일관성 검사이므로 글이 안정된 상태에서 마지막에 적용됩니다.

**어조 일관성 보충**: humanizer 패턴 24(경어체 균일성=AI 신호)와 style-guide 어조 일관성 검사(~합니다/~해요 혼용=비일관)는 결이 다른 층을 봅니다 — humanizer는 *글 단위 변주*, style-guide는 *단락 단위 일관*입니다. 파이프라인 순서로 적용하세요: humanizer가 의도적 변주를 도입하고, style-guide가 단락 일관성을 검증. 두 검사는 충돌이 아니라 보완 관계입니다.

`npx skills add daleseo/korean-skills`로 세 스킬을 한 번에 설치하면 어떤 Agent Skills 호환 환경에서든 이 파이프라인을 활용할 수 있습니다.

## 사용법

설치 후 각 AI 도구에서 자동으로 활성화됩니다:

| 도구           | 활성화 방식                           | 예시                                   |
| -------------- | ------------------------------------- | -------------------------------------- |
| Claude Code    | 자동 (키워드 감지) 또는 슬래시 명령어 | "이 한국어 텍스트 자연스럽게 만들어줘" |
| Cursor         | 파일 패턴 매칭                        | 한국어 텍스트 작업 시 자동 활성화      |
| GitHub Copilot | `@workspace` 멘션                     | `@workspace 한국어 문법 검사`          |

---

## 라이선스

MIT 라이선스 - 자유롭게 사용, 수정, 배포할 수 있습니다.

## 기여하기

기여를 환영합니다! 이슈나 풀 리퀘스트를 자유롭게 제출해주세요.
