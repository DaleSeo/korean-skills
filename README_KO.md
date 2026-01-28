# korean-skills

> AI 코딩 에이전트를 위한 한국어 스킬 모음

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/skills-2-green.svg)](#스킬)

**[English](./README.md)** 🇺🇸

이 저장소는 Claude Code, Cursor, Windsurf 등 Agent Skills 형식을 지원하는 AI 코딩 에이전트에서 사용할 수 있는 한국어 특화 스킬을 제공합니다.

---

## 빠른 시작

```bash
# 모든 스킬 설치
npx skills add daleseo/korean-skills

# 또는 특정 스킬만 설치
npx skills add daleseo/korean-skills@humanizer
npx skills add daleseo/korean-skills@grammar-checker
```

---

## 스킬

### humanizer

> AI가 생성한 한국어 텍스트를 자연스러운 인간의 글쓰기로 변환합니다.

**기반:** KatFishNet 논문 (ArXiv 2503.00032v4), 94.88% AUC 정확도

**주요 특징:**
- 5개 카테고리 20가지 검출 패턴
- 과학적 연구 기반 (실증적 언어학 분석)
- 의미와 격식 수준 보존

**예시:**
```
수정 전 (AI): 인공지능 기술의 발전은 빠르게 진행되고 있으며, 다양한 산업 분야에 적용되고 있습니다.
수정 후:      인공지능 기술은 빠르게 발전하고 있으며 여러 산업 분야에 적용되고 있습니다.
```

**검출 카테고리:**
- 문장부호 (7가지) - 94.88% AUC
- 띄어쓰기 (3가지) - 79.51% AUC
- 품사 다양성 (3가지) - 82.99% AUC
- 어휘 (3가지)
- 문장 구조 (4가지)

**사용법:**
```
/humanizer

[자연스럽게 만들 한국어 텍스트 붙여넣기]
```

📖 **[전체 문서 → SKILL.md](./skills/humanizer/SKILL.md)**

**참고 자료:**
- 📄 [KatFishNet 논문](https://arxiv.org/abs/2503.00032v4)
- 📁 [패턴 참조 문서](./skills/humanizer/references/)
- 🌐 [영어 버전](https://github.com/blader/humanizer) | [중국어 버전](https://github.com/op7418/Humanizer-zh)

---

### grammar-checker

> 표준 한국어 규칙에 기반한 문법, 맞춤법, 띄어쓰기, 구두점 검사기입니다.

**기반:** 국립국어원 표준 한국어 규정

**주요 특징:**
- 우선순위가 있는 4가지 오류 카테고리
- 각 오류에 대한 교육적 설명
- 문맥을 고려한 교정 (격식체/비격식체)
- 확신도 표시 (확실한 오류 vs 권장 사항)

**예시:**
```
수정 전: 이 프로젝트는 사용자들에게 더나은 경험을 제공하기위해 시작되요.
수정 후: 이 프로젝트는 사용자들에게 더 나은 경험을 제공하기 위해 시작됐어요.
```

**오류 카테고리:**
1. 맞춤법/철자 (최고 우선순위) - 되/돼, -ㄴ지/-는지 등
2. 띄어쓰기 (높은 우선순위) - 의존명사, 보조용언, 단위명사
3. 문법 구조 (중간 우선순위) - 조사, 어미 사용
4. 구두점 (낮은 우선순위) - 쉼표, 느낌표

**사용법:**
```
/grammar-checker

[검사할 한국어 텍스트 붙여넣기]
```

📖 **[전체 문서 → SKILL.md](./skills/grammar-checker/SKILL.md)**

**참고 자료:**
- 📁 [문법 규칙 참조](./skills/grammar-checker/references/rules.md)
- 📁 [흔한 오류 참조](./skills/grammar-checker/references/common-errors.md)
- 📋 [예시 파일](./skills/grammar-checker/examples/)

---

## 라이선스

MIT 라이선스 - 자유롭게 사용, 수정, 배포할 수 있습니다.

## 기여하기

기여를 환영합니다! 이슈나 풀 리퀘스트를 자유롭게 제출해주세요.
