# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository provides Korean language skills for AI agents (Claude Code, Cursor, Windsurf, etc.) that support the Agent Skills format. Each skill is a self-contained module with documentation, reference materials, and examples.

## Repository Structure

```
korean-skills/
├── skills/
│   ├── humanizer/           # AI writing pattern detection & correction
│   │   ├── SKILL.md        # Main skill documentation (Agent Skills format)
│   │   ├── references/     # 6 pattern reference files (punctuation, spacing, pos, vocabulary, structure, translation-ese)
│   │   └── examples/       # Before/after examples
│   ├── grammar-checker/     # Grammar & spelling checker
│   │   ├── SKILL.md        # Main skill documentation (Agent Skills format)
│   │   ├── references/     # Grammar rules & common errors
│   │   └── examples/       # Error examples
│   └── style-guide/         # Style consistency checker
│       ├── SKILL.md        # Main skill documentation (Agent Skills format)
│       ├── references/     # 6 category reference files (tone, terminology, numbering, list, quotation, datetime)
│       └── examples/       # Inconsistent/consistent examples
├── README.md               # Korean documentation (default)
└── README_EN.md            # English documentation
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

**Pattern Classification System** (v1.6.0):

- All patterns include 3-field metadata: verification, severity, version (no 출처 field)
- **Verification**: ✅ Scientific (KatFishNet, with inline citation, e.g., `검증: ✅ 과학적 (KatFishNet, 94.88% AUC)`) or 📊 Empirical (community observation)
- **Severity**: S1 (decisive single occurrence) / S2 (frequency-based, 3+ repetitions) / S3 (weak signal, only with co-occurrence)
- Scientific patterns: 1-6 (punctuation), 8-10 (spacing), 11-13 (POS diversity). Empirical patterns: 7, 14-24, 25-36
- Version history: v1.1.0 added pattern 7 (colon), v1.2.0 added pattern 17 (plural marker), v1.3.0 added patterns 18-20 (pronoun/demonstrative/subject omission), v1.4.0 added patterns 25-36 (translation-ese) + severity system, v1.5.0 added patterns 37-38 (AI closing markers + hype vocabulary cluster) + over-rewriting guard + fidelity self-check, v1.6.0 added patterns 39 (~적 N abstract chain) + 40 (~것이다 future declarative) + naturalness grade A~D + pattern 37 boost (결말 단언 공식)

**6 Categories, 40 Patterns**:

1. Punctuation (7 patterns) - 94.88% AUC
2. Spacing (3 patterns) - 79.51% AUC
3. POS Diversity (3 patterns) - 82.99% AUC
4. Vocabulary (10 patterns) - includes pronoun overuse, demonstrative overuse, subject omission, AI closing markers (결론적으로, 시사하는 바가 크다, ~라는 뜻이다), hype vocabulary cluster (혁신적, 압도적, 전례 없는), abstract `~적 N` chains (전략적 함의, 구조적 한계)
5. Sentence Structure (4 patterns)
6. Translation-ese (13 patterns) - particle translation-ese (에 대해/통해/있어서), redundant verbs (가지고 있다), passive overuse (되어진다/에 의해), modal hedging (할 수 있다), future declarative (~것이다 overuse)

**Key Reference Files**:

- `references/punctuation-patterns.md` - Includes metadata per pattern
- `references/spacing-patterns.md`
- `references/pos-patterns.md`
- `references/vocabulary-patterns.md`
- `references/structure-patterns.md`
- `references/translation-ese-patterns.md` - Korean translation-ese patterns (added v1.4.0)

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

**Genre-Aware Analysis** (v1.1.0): 4 document types (business, academic, technical, marketing/blog) with 7×4 category-genre matrix. Type determined by 3-tier priority — user-explicit → auto-detection → AskUserQuestion fallback. Each reference file contains a "장르별 권장 사항" section with type-specific guidelines.

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

`.github/workflows/ci.yml` runs on every PR and main push with four jobs:

- **`verify-version-bump`** (PR only): Fails the PR if anything under `skills/` or `.claude-plugin/` changed without bumping `.claude-plugin/plugin.json#version`. Prevents shipping silent updates.
- **`validate-spec`**: Validates each `SKILL.md` against the Agent Skills spec using `skills-ref validate` (from `agentskills/agentskills`).
- **`validate-publish`**: Runs `gh skill publish --dry-run` to check publishability before main merges.
- **`install-local`**: Installs all skills from the local working tree via `npx skills add "$GITHUB_WORKSPACE" --yes` and verifies each skill landed in `.agents/skills/`.
- **`install-remote`** (main only): Installs from the public GitHub source (`npx skills add daleseo/korean-skills --yes`) as a post-merge smoke test.

`.github/workflows/release.yml` runs on main pushes only. It reads `.claude-plugin/plugin.json#version`, creates a matching `vX.Y.Z` tag if missing, and runs `gh skill publish --tag` so `gh skill install daleseo/korean-skills --pin vX.Y.Z` resolves.

## Releasing / Versioning

Three places carry version numbers, but only one matters operationally.

**`.claude-plugin/plugin.json#version`** — the source of truth. Bump it whenever you touch `skills/` or `.claude-plugin/`. The `verify-version-bump` CI job enforces this on every PR. Effects:

- The release workflow tags a matching `vX.Y.Z` on the next main push, which is what `gh skill install daleseo/korean-skills --pin vX.Y.Z` and `claude plugin update` resolve to.
- New installs always pull the latest content regardless.

Use semver: patch for fixes/wording, minor for new skills or pattern additions, major when removing or renaming a skill.

**Individual `SKILL.md#version`** (e.g. humanizer 1.6.0) — independent of the plugin version. Track skill-internal evolution there. The plugin version doesn't have to follow the highest skill version — they're separate trackers, like Apollo's pattern (apollo-skills plugin at 1.2.x while internal skills are at various 1.x).

**`marketplace.json#metadata.version` and `marketplace.json#plugins[0].version`** — keep aligned with `plugin.json#version` for tidiness, but no automation reads them today. CI does not enforce sync.

## Documentation Pattern

**README Split**: README.md (Korean, default) and README_EN.md (English) are separate files with identical structure. Korean is the default since most users of this repo are Korean speakers:

- Link to other language at top
- Quick Start with installation commands
- Brief skill summaries with one example each
- Links to SKILL.md for full documentation

**Documentation Hierarchy**:

```
README.md/README_EN.md → SKILL.md → references/*.md
```

## Adding New Patterns

When adding patterns to humanizer:

1. **Add 3-field metadata** to pattern in reference file (no 출처 field):

   ```markdown
   **메타데이터**:

   - 검증: [✅ 과학적 (with inline citation, e.g., KatFishNet, 94.88% AUC) or 📊 경험적]
   - 심각도: [S1 (decisive single occurrence) / S2 (frequency-based, 3+) / S3 (weak, only with co-occurrence)]
   - 버전: [version added, e.g., 1.4.0]
   ```

2. **Update version** in SKILL.md frontmatter (semantic versioning)

3. **Update pattern counts**:
   - SKILL.md description and "총 N가지" headings
   - README.md and README_EN.md detection categories
   - Reference file headers

4. **Update pattern classification section** in SKILL.md if adding new verification level or severity rationale

## Coding Conventions

From global CLAUDE.md:

- 불필요한 환경 변수(.env, 설정값 등)는 사전에 만들어두지 않는다
- 사용하지 않는 코드는 반드시 삭제한다

Additional conventions:

- Maintain bilingual documentation (English + Korean)
- Keep READMEs concise; detailed docs go in SKILL.md
- Reference files contain comprehensive patterns with examples
- SKILL.md is the authoritative documentation (don't create separate README files in skill directories)
