# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository provides Korean language skills for AI coding agents (Claude Code, Cursor, Windsurf, etc.) that support the Agent Skills format. Each skill is a self-contained module with documentation, reference materials, and examples.

## Repository Structure

```
korean-skills/
├── skills/
│   ├── humanizer/           # AI writing pattern detection & correction
│   │   ├── SKILL.md        # Main skill documentation (Agent Skills format)
│   │   ├── references/     # 5 pattern reference files (punctuation, spacing, pos, vocabulary, structure)
│   │   └── examples/       # Before/after examples
│   ├── grammar-checker/     # Grammar & spelling checker
│   │   ├── SKILL.md        # Main skill documentation (Agent Skills format)
│   │   ├── references/     # Grammar rules & common errors
│   │   └── examples/       # Error examples
│   └── style-guide/         # Style consistency checker
│       ├── SKILL.md        # Main skill documentation (Agent Skills format)
│       ├── references/     # 6 category reference files (tone, terminology, numbering, list, quotation, datetime)
│       └── examples/       # Inconsistent/consistent examples
├── README.md               # English documentation
└── README_KO.md            # Korean documentation
```

## Skills Architecture

### Agent Skills Format

Each skill follows the Agent Skills specification:

- **SKILL.md**: Must have YAML frontmatter with `name` and `description` fields
- **name**: Must match the skill directory name
- **description**: 1-1024 characters, preferably ASCII-safe for CLI compatibility
- Skills are installed via `npx skills add daleseo/korean-skills@<skill-name>`

### humanizer

**Purpose**: Transforms AI-generated Korean text into natural human writing based on scientific research (KatFishNet paper, 94.88% AUC accuracy)

**Pattern Classification System** (v1.3.0):

- All patterns include metadata: source, verification level, version
- **Tier 1 - Scientific**: Patterns verified by KatFishNet paper (patterns 1-7: punctuation, 8-10: spacing, 11-13: POS diversity)
- **Tier 2 - Empirical**: Community-added patterns based on observation (pattern 7: colon overuse added in v1.1.0, pattern 17: plural marker overuse added in v1.2.0, patterns 18-20: pronoun/demonstrative overuse and subject omission added in v1.3.0)

**5 Categories, 24 Patterns**:

1. Punctuation (7 patterns) - 94.88% AUC
2. Spacing (3 patterns) - 79.51% AUC
3. POS Diversity (3 patterns) - 82.99% AUC
4. Vocabulary (7 patterns) - includes pronoun overuse, demonstrative overuse, subject omission
5. Sentence Structure (4 patterns)

**Key Reference Files**:

- `references/punctuation-patterns.md` - Includes metadata per pattern
- `references/spacing-patterns.md`
- `references/pos-patterns.md`
- `references/vocabulary-patterns.md`
- `references/structure-patterns.md`

### grammar-checker

**Purpose**: Detects and corrects Korean grammar, spelling, spacing, and punctuation errors based on National Institute of Korean Language standards

**4 Error Categories** (by priority):

1. Spelling/Orthography (Highest) - 되/돼, -ㄴ지/-는지, etc.
2. Spacing (High) - 의존명사, 보조용언, 단위명사
3. Grammar Structure (Medium) - Particles, verb endings
4. Punctuation (Low) - Commas, exclamation marks

**Key Reference Files**:

- `references/rules.md` - Detailed Korean language rules
- `references/common-errors.md` - Common error patterns

### style-guide

**Purpose**: Ensures consistent writing style within documents or across projects (tone, terminology, formatting)

**3-Tier Authority System**:

- **Tier 1 - Government Standards**: National Institute of Korean Language, Public Language guidelines
- **Tier 2 - Academic Standards**: University thesis writing guidelines, citation formats (APA, MLA)
- **Tier 3 - Industry Standards**: Kakao Enterprise tech writing guide, IT terminology standards

**7 Check Categories** (by priority):

1. Tone & Formality (Highest) - ~합니다/~해요 mixing, subject consistency (우리/저희)
2. Terminology (High) - same concept different words (사용자/유저), loanword spelling
3. Numbers & Units (Medium) - Arabic vs Korean numerals, unit spacing
4. List Structure (Medium) - bullet styles (1./-, etc.), ending consistency
5. Quotation & Emphasis (Low) - " " vs ' ', **bold** vs *italic*
6. Date & Time (Low) - YYYY년 MM월 DD일 vs YYYY-MM-DD, 12h vs 24h
7. Links & References (Low) - descriptive vs "click here", citation format

**Key Reference Files**:

- `references/tone-consistency.md` - Tone & formality patterns
- `references/terminology.md` - Terminology unification
- `references/numbering-units.md` - Number & unit formatting
- `references/list-structure.md` - List & heading styles
- `references/quotation-emphasis.md` - Quotation & emphasis
- `references/datetime-reference.md` - Date/time/link/citation formats

## CI/CD

GitHub Actions workflow (`.github/workflows/ci.yml`) has two jobs:

- **`test`** (all branches): Installs all skills from the local repository (`npx skills add . --yes`) and verifies each skill has `SKILL.md` in `.agents/skills/`
- **`test-remote`** (main branch only): Installs all skills from GitHub (`npx skills add daleseo/korean-skills --yes`) and verifies installation in `.agents/skills/`

Both jobs check that at least one skill was installed successfully.

## Documentation Pattern

**README Split**: README.md (English) and README_KO.md (Korean) are separate files with identical structure:

- Link to other language at top
- Quick Start with installation commands
- Brief skill summaries with one example each
- Links to SKILL.md for full documentation

**Documentation Hierarchy**:

```
README.md/README_KO.md → SKILL.md → references/*.md
```

## Adding New Patterns

When adding patterns to humanizer:

1. **Add metadata** to pattern in reference file:

   ```markdown
   **메타데이터**:

   - 출처: [source: KatFishNet paper or korean-skills community]
   - 검증: [✅ 과학적 or 📊 경험적]
   - 버전: [version added, e.g., 1.1.0]
   ```

2. **Update version** in SKILL.md frontmatter (semantic versioning)

3. **Update pattern counts**:
   - SKILL.md description
   - README.md and README_KO.md detection categories
   - Reference file headers

4. **Update pattern classification section** in SKILL.md if adding new verification tier

## Coding Conventions

From global CLAUDE.md:

- 불필요한 환경 변수(.env, 설정값 등)는 사전에 만들어두지 않는다
- 사용하지 않는 코드는 반드시 삭제한다

Additional conventions:

- Maintain bilingual documentation (English + Korean)
- Keep READMEs concise; detailed docs go in SKILL.md
- Reference files contain comprehensive patterns with examples
- SKILL.md is the authoritative documentation (don't create separate README files in skill directories)
