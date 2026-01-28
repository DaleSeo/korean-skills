# korean-skills

> Korean language skills for AI coding agents

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/skills-2-green.svg)](#skills)

**[한국어 문서](./README_KO.md)** 🇰🇷

This repository provides Korean language skills for AI coding agents (Claude Code, Cursor, Windsurf, etc.) supporting the Agent Skills format.

---

## Quick Start

**Installation:**

```bash
# Install specific skill
npx skills add daleseo/korean-skills --skill humanizer
npx skills add daleseo/korean-skills --skill grammar-checker

# Install all skills
npx skills add daleseo/korean-skills
```

<details>
<summary>Manual installation</summary>

```bash
mkdir -p ~/.claude/skills/humanizer
git clone https://github.com/daleseo/korean-skills.git /tmp/korean-skills
cp -r /tmp/korean-skills/skills/humanizer/* ~/.claude/skills/humanizer/
rm -rf /tmp/korean-skills
```
</details>

---

## Skills

### humanizer

> Detects and corrects Korean AI writing patterns to transform text into natural human writing.

**Based on:** KatFishNet paper (ArXiv 2503.00032v4) with 94.88% AUC accuracy

**Key features:**
- 20 detection patterns across 5 categories
- Scientifically grounded (empirical linguistic research)
- Preserves meaning and formality level

**Example:**
```
Before (AI): 인공지능 기술의 발전은 빠르게 진행되고 있으며, 다양한 산업 분야에 적용되고 있습니다.
After:       인공지능 기술은 빠르게 발전하고 있으며 여러 산업 분야에 적용되고 있습니다.
```

**Detection categories:**
- Punctuation (7 patterns) - 94.88% AUC
- Spacing (3 patterns) - 79.51% AUC
- POS Diversity (3 patterns) - 82.99% AUC
- Vocabulary (3 patterns)
- Sentence Structure (4 patterns)

**Usage:**
```
/humanizer

[Paste Korean text to humanize]
```

📖 **[Full documentation → SKILL.md](./skills/humanizer/SKILL.md)**

**Resources:**
- 📄 [KatFishNet Paper](https://arxiv.org/abs/2503.00032v4)
- 📁 [Pattern references](./skills/humanizer/references/)
- 🌐 [English version](https://github.com/blader/humanizer) | [Chinese version](https://github.com/op7418/Humanizer-zh)

---

### grammar-checker

> Korean grammar, spelling, spacing, and punctuation checker based on standard Korean language rules.

**Based on:** National Institute of Korean Language standards

**Key features:**
- 4 error categories with priority levels
- Educational explanations for each error
- Context-aware corrections (formal vs informal)
- Confidence levels (certain errors vs recommendations)

**Example:**
```
Before: 이 프로젝트는 사용자들에게 더나은 경험을 제공하기위해 시작되요.
After:  이 프로젝트는 사용자들에게 더 나은 경험을 제공하기 위해 시작됐어요.
```

**Error categories:**
1. Spelling/Orthography (Highest priority) - 되/돼, -ㄴ지/-는지, etc.
2. Spacing (High priority) - 의존명사, 보조용언, 단위명사
3. Grammar Structure (Medium priority) - Particles, verb endings
4. Punctuation (Low priority) - Commas, exclamation marks

**Usage:**
```
/grammar-checker

[Paste Korean text to check]
```

📖 **[Full documentation → SKILL.md](./skills/grammar-checker/SKILL.md)**

**Resources:**
- 📁 [Grammar rules reference](./skills/grammar-checker/references/rules.md)
- 📁 [Common errors reference](./skills/grammar-checker/references/common-errors.md)
- 📋 [Examples](./skills/grammar-checker/examples/)

---

## License

MIT License - Free to use, modify, and distribute.

## Contributing

Contributions are welcome! Feel free to submit issues or pull requests.
