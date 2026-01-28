# Korean Skills

> Korean language skills for AI coding agents

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/skills-3-green.svg)](#skills)

**[한국어 문서](./README_KO.md)** 🇰🇷

This repository provides Korean language skills for AI coding agents (Claude Code, Cursor, Windsurf, etc.) supporting the Agent Skills format.

## Quick Start

### Install all skills

```bash
npx skills add daleseo/korean-skills
```

### Install specific skill

```bash
npx skills add daleseo/korean-skills@humanizer
npx skills add daleseo/korean-skills@grammar-checker
npx skills add daleseo/korean-skills@style-guide
```

## Skills

### [humanizer](skills/humanizer)

Detects and corrects Korean AI writing patterns to transform text into natural human writing

**Key features:**

- 20 detection patterns across 5 categories
- Based on KatFishNet paper (94.88% AUC accuracy)
- Preserves meaning and formality level

**Detection categories:**

- Punctuation (7 patterns) - 94.88% AUC
- Spacing (3 patterns) - 79.51% AUC
- POS Diversity (3 patterns) - 82.99% AUC
- Vocabulary (3 patterns)
- Sentence Structure (4 patterns)

**When does it activate?**

- When you paste Korean text for humanization
- When using `/humanizer` command
- When working with AI-generated Korean content

**Example:**

```
Before (AI): 인공지능 기술의 발전은 빠르게 진행되고 있으며, 다양한 산업 분야에 적용되고 있습니다.
After:       인공지능 기술은 빠르게 발전하고 있으며 여러 산업 분야에 적용되고 있습니다.
```

**Usage:**

```
/humanizer

[Paste Korean text to humanize]
```

```bash
npx skills add daleseo/korean-skills@humanizer
```

📖 **[Full documentation → SKILL.md](./skills/humanizer/SKILL.md)**

**Resources:**

- 📄 [KatFishNet Paper](https://arxiv.org/abs/2503.00032v4)
- 📁 [Pattern references](./skills/humanizer/references/)
- 🌐 [English version](https://github.com/blader/humanizer) | [Chinese version](https://github.com/op7418/Humanizer-zh)

---

### [grammar-checker](skills/grammar-checker)

Korean grammar, spelling, spacing, and punctuation checker based on standard Korean language rules

**Key features:**

- 4 error categories with priority levels
- Educational explanations for each error
- Context-aware corrections (formal vs informal)
- Confidence levels (certain errors vs recommendations)

**Error categories:**

1. Spelling/Orthography (Highest priority) - 되/돼, -ㄴ지/-는지, etc.
2. Spacing (High priority) - 의존명사, 보조용언, 단위명사
3. Grammar Structure (Medium priority) - Particles, verb endings
4. Punctuation (Low priority) - Commas, exclamation marks

**When does it activate?**

- When you paste Korean text for grammar checking
- When using `/grammar-checker` command
- When reviewing Korean documents

**Example:**

```
Before: 이 프로젝트는 사용자들에게 더나은 경험을 제공하기위해 시작되요.
After:  이 프로젝트는 사용자들에게 더 나은 경험을 제공하기 위해 시작됐어요.
```

**Usage:**

```
/grammar-checker

[Paste Korean text to check]
```

```bash
npx skills add daleseo/korean-skills@grammar-checker
```

📖 **[Full documentation → SKILL.md](./skills/grammar-checker/SKILL.md)**

**Resources:**

- 📁 [Grammar rules reference](./skills/grammar-checker/references/rules.md)
- 📁 [Common errors reference](./skills/grammar-checker/references/common-errors.md)
- 📋 [Examples](./skills/grammar-checker/examples/)

---

### [style-guide](skills/style-guide)

Korean document style consistency checker for uniform writing across documents

**Key features:**

- 7 consistency check categories
- Multi-layered authority sources (government, academic, industry standards)
- Context-aware suggestions (document type: business/academic/technical/marketing)
- Majority-rule principle for conflicting styles

**Check categories:**

1. Tone & Formality (Highest priority) - formal vs informal speech, subject consistency
2. Terminology (High priority) - same concept different words, loanword spelling
3. Numbers & Units (Medium priority) - Arabic vs Korean numerals, unit spacing
4. List Structure (Medium priority) - bullet styles, ending consistency
5. Quotation & Emphasis (Low priority) - quotation marks, bold/italic
6. Date & Time (Low priority) - date formats, 12h/24h time
7. Links & References (Low priority) - link text, citation formats

**When does it activate?**

- When reviewing multi-author documents
- When using `/style-guide` command
- When maintaining project-wide terminology standards
- When preparing formal documents for brand consistency

**Example:**

```
Inconsistent: 사용자는 화면을 확인합니다. 유저가 페이지 설정을 변경해요.
Consistent:   사용자는 화면을 확인합니다. 사용자가 화면 설정을 변경합니다.
```

**Usage:**

```
/style-guide

[Paste Korean document to check for style consistency]
```

```bash
npx skills add daleseo/korean-skills@style-guide
```

📖 **[Full documentation → SKILL.md](./skills/style-guide/SKILL.md)**

**Resources:**

- 📁 [Authority standards](./skills/style-guide/references/)
  - Government: National Institute of Korean Language guidelines
  - Academic: University thesis writing standards
  - Industry: Kakao Enterprise tech writing guide
- 📋 [Examples](./skills/style-guide/examples/)

## How to Use

After installation, skills activate automatically in each AI tool:

| Tool           | Activation Method                    | Example                                      |
| -------------- | ------------------------------------ | -------------------------------------------- |
| Claude Code    | Auto (keyword detection) or `/skill` | "Humanize this Korean text"                  |
| Cursor         | File pattern matching                | Auto-activates when working with Korean text |
| GitHub Copilot | `@workspace` mention                 | `@workspace Check Korean grammar`            |

---

## License

MIT License - Free to use, modify, and distribute.

## Contributing

Contributions are welcome! Feel free to submit issues or pull requests.
