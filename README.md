# korean-skills

> Korean language skills for AI coding agents
>
> AI 코딩 에이전트를 위한 한국어 스킬 모음

이 저장소는 Claude Code, Cursor, Windsurf 등 Agent Skills 형식을 지원하는 AI 코딩 에이전트에서 사용할 수 있는 한국어 특화 스킬을 제공합니다.

## 스킬 목록 / Available Skills

### 1. humanizer

> Detects and corrects Korean AI writing patterns to make text sound naturally human-written.
>
> 한국어 AI 작문 패턴을 감지하고 자연스러운 인간의 글쓰기로 변환하는 스킬입니다.

**Based on scientific research** (KatFishNet paper, 94.88% AUC accuracy) • **과학적 연구 기반** (KatFishNet 논문, 94.88% AUC 정확도)

### 2. grammar-checker

> Korean grammar, spelling, spacing, and punctuation checker based on standard Korean language rules.
>
> 표준 한국어 규칙에 기반한 문법, 맞춤법, 띄어쓰기, 구두점 검사기입니다.

**Rule-based approach** with educational explanations • **규칙 기반 접근** 학습 지향적 설명 제공

---

## English

### What is humanizer?

humanizer is an AI agent skill that transforms artificial-sounding Korean text into natural human writing based on scientific linguistic research. It works with Claude Code, Cursor, Windsurf, and other AI coding agents that support the Agent Skills format. The skill analyzes and corrects the distinctive patterns that large language models (LLMs) like ChatGPT, Claude, and Gemini produce when writing in Korean.

**The Problem**: LLM-generated Korean text exhibits measurable linguistic patterns that differ from human writing. For example, LLMs use commas in 61% of sentences while humans use them in only 26%. LLMs also show overly consistent spacing (standard deviation 0.02 vs natural human variation), higher noun ratios, and poverty in verb/adjective usage.

**The Solution**: Based on the KatFishNet paper (ArXiv 2503.00032v4), this skill detects 19 linguistic patterns across 5 categories and rewrites text to sound naturally human-written while preserving the original meaning and formality level.

### Key Features

- **Scientifically grounded**: Based on empirical linguistic research (KatFishNet paper)
- **Korean-specific**: Analyzes patterns unique to Korean language, not translated from English/Chinese
- **20 detection patterns**: Organized into 5 categories by priority
- **Preserves meaning**: Maintains original intent and formality level
- **High accuracy**: 94.88% AUC for punctuation, 82.99% for POS, 79.51% for spacing

### Quick Start

**Installation**:

Using Skills CLI (recommended):

```bash
npx skills add daleseo/korean-skills --skill humanizer
```

Or manual installation:

```bash
mkdir -p ~/.claude/skills/humanizer
git clone https://github.com/daleseo/korean-skills.git /tmp/korean-skills
cp -r /tmp/korean-skills/skills/humanizer/* ~/.claude/skills/humanizer/
rm -rf /tmp/korean-skills
```

**Usage**:

```
/humanizer

[Paste Korean text to humanize]
```

### Detection Patterns

The skill analyzes 5 categories of AI writing patterns:

**1. Punctuation (7 patterns)** - Highest priority (94.88% AUC for patterns 1-6)

- Excessive comma usage (LLM 61% vs human 26%)
- English-style comma placement
- Commas after connective endings
- Sentence-ending comma patterns
- Unnecessary list commas
- Em-dash overuse
- English-style colon overuse (NEW in v1.1.0)

**2. Spacing (3 patterns)** - High priority (79.51% AUC)

- Rigid bound noun spacing (standard deviation <0.05)
- Excessive auxiliary verb spacing
- Numeral-bound noun spacing

**3. Part-of-Speech Diversity (3 patterns)** - High priority (82.99% AUC)

- Noun overuse (>35% ratio)
- Verb/adjective poverty (<25% ratio)
- POS n-gram monotony

**4. Vocabulary (3 patterns)** - Medium priority

- AI vocabulary overuse (중요하다, 효과적, 혁신적, 지속가능한, etc.)
- Unnecessary Sino-Korean terms (진행하다→하다, 실시하다→하다)
- English idiom calques (~의 중심에, ~를 통해)

**5. Sentence Structure (4 patterns)** - Medium priority

- Lack of rhythm (uniform sentence length)
- Rule of three overuse
- Connector overuse (그러나, 또한, 따라서)
- Honorific uniformity

### Example

**Before (AI-generated)**:

> 인공지능 기술의 발전은 빠르게 진행되고 있으며, 다양한 산업 분야에 적용되고 있습니다. 이러한 기술은 효과적으로 업무 효율성을 향상시키고, 혁신적인 솔루션을 제공하며, 지속가능한 성장을 가능하게 합니다.

**After (humanized)**:

> 인공지능 기술은 빠르게 발전하고 있으며 여러 산업 분야에 적용되고 있습니다. 이 기술은 업무 효율을 높이고 새로운 솔루션을 제공하며 장기적 성장을 가능하게 합니다.

**Key changes**: Removed 6 commas, replaced AI vocabulary (다양한→여러, 효과적으로→높이고, 혁신적인→새로운, 지속가능한→장기적), replaced unnecessary Sino-Korean terms (진행되고→발전하고, 향상시키고→높이고).

### Resources

- 📄 [KatFishNet Paper (ArXiv 2503.00032v4)](https://arxiv.org/abs/2503.00032v4)
- 🌐 [humanizer (English version)](https://github.com/blader/humanizer)
- 🇨🇳 [humanizer-zh (Chinese version)](https://github.com/op7418/Humanizer-zh)
- 📁 [Detailed pattern reference](./references/) - See reference files for comprehensive pattern explanations

### License

MIT License - Free to use, modify, and distribute.

---

## 한국어

### humanizer란?

humanizer는 과학적 언어학 연구를 기반으로 인위적인 한국어 텍스트를 자연스러운 인간의 글쓰기로 변환하는 AI 에이전트 스킬입니다. Claude Code, Cursor, Windsurf 등 Agent Skills 형식을 지원하는 다양한 AI 코딩 에이전트에서 사용할 수 있습니다. ChatGPT, Claude, Gemini 같은 대형 언어 모델(LLM)이 한국어로 작성할 때 나타나는 특징적인 패턴을 분석하고 교정합니다.

**문제**: LLM이 생성한 한국어 텍스트는 인간의 글쓰기와 다른 측정 가능한 언어학적 패턴을 보입니다. 예를 들어, LLM은 문장의 61%에서 쉼표를 사용하는 반면 사람은 26%만 사용합니다. 또한 LLM은 지나치게 일관적인 띄어쓰기(표준편차 0.02 vs 인간의 자연스러운 변화), 높은 명사 비율, 동사/형용사 빈곤을 보입니다.

**해결책**: KatFishNet 논문(ArXiv 2503.00032v4)을 기반으로 5개 카테고리의 19가지 언어학적 패턴을 감지하고, 원문의 의미와 격식 수준을 유지하면서 자연스러운 인간의 글쓰기로 재작성합니다.

### 주요 특징

- **과학적 기반**: 실증적 언어학 연구 기반 (KatFishNet 논문)
- **한국어 특화**: 영어/중국어 번역이 아닌 한국어 고유 패턴 분석
- **20가지 패턴**: 우선순위별 5개 카테고리로 구성
- **의미 보존**: 원문의 의도와 격식 수준 유지
- **높은 정확도**: 문장부호 94.88% AUC, 품사 82.99%, 띄어쓰기 79.51%

### 빠른 시작

**설치**:

Skills CLI 사용 (권장):

```bash
npx skills add daleseo/korean-skills --skill humanizer
```

또는 수동 설치:

```bash
mkdir -p ~/.claude/skills/humanizer
git clone https://github.com/daleseo/korean-skills.git /tmp/korean-skills
cp -r /tmp/korean-skills/skills/humanizer/* ~/.claude/skills/humanizer/
rm -rf /tmp/korean-skills
```

**사용법**:

```
/humanizer

[자연스럽게 만들 한국어 텍스트 붙여넣기]
```

### 검출 패턴

5가지 카테고리의 AI 작문 패턴 분석:

**1. 문장부호 (7가지)** - 최고 우선순위 (94.88% AUC, 패턴 1-6)

- 과도한 쉼표 사용 (LLM 61% vs 인간 26%)
- 영어식 쉼표 위치
- 연결어미 뒤 쉼표
- 문장 끝 쉼표 패턴
- 불필요한 목록 쉼표
- 줄표(Em-Dash) 과다 사용
- 영어식 콜론 과다 사용 (v1.1.0 신규)

**2. 띄어쓰기 (3가지)** - 높은 우선순위 (79.51% AUC)

- 경직된 의존명사 띄어쓰기 (표준편차 <0.05)
- 과도한 보조용언 띄어쓰기
- 숫자-의존명사 띄어쓰기

**3. 품사 다양성 (3가지)** - 높은 우선순위 (82.99% AUC)

- 명사 과다 사용 (>35% 비율)
- 동사/형용사 빈곤 (<25% 비율)
- 품사 N-gram 단조로움

**4. 어휘 (3가지)** - 중간 우선순위

- AI 어휘 과다 (중요하다, 효과적, 혁신적, 지속가능한 등)
- 불필요한 한자어 (진행하다→하다, 실시하다→하다)
- 영어 관용구 직역 (~의 중심에, ~를 통해)

**5. 문장 구조 (4가지)** - 중간 우선순위

- 리듬 부족 (균일한 문장 길이)
- 삼단 구성 과다
- 접속사 과다 (그러나, 또한, 따라서)
- 경어체 획일성

### 예시

**수정 전 (AI 작문)**:

> 인공지능 기술의 발전은 빠르게 진행되고 있으며, 다양한 산업 분야에 적용되고 있습니다. 이러한 기술은 효과적으로 업무 효율성을 향상시키고, 혁신적인 솔루션을 제공하며, 지속가능한 성장을 가능하게 합니다.

**수정 후 (자연스러운 글)**:

> 인공지능 기술은 빠르게 발전하고 있으며 여러 산업 분야에 적용되고 있습니다. 이 기술은 업무 효율을 높이고 새로운 솔루션을 제공하며 장기적 성장을 가능하게 합니다.

**주요 변경**: 쉼표 6개 제거, AI 어휘 교체 (다양한→여러, 효과적으로→높이고, 혁신적인→새로운, 지속가능한→장기적), 불필요한 한자어 교체 (진행되고→발전하고, 향상시키고→높이고).

### 참고 자료

- 📄 [KatFishNet 논문 (ArXiv 2503.00032v4)](https://arxiv.org/abs/2503.00032v4)
- 🌐 [humanizer (영어 버전)](https://github.com/blader/humanizer)
- 📁 [상세 패턴 참고 자료](./skills/humanizer/references/) - 포괄적인 패턴 설명은 참고 파일 참조

---

## grammar-checker

> Korean grammar, spelling, spacing, and punctuation checker based on standard Korean language rules.
>
> 표준 한국어 규칙에 기반한 문법, 맞춤법, 띄어쓰기, 구두점 검사기입니다.

**Rule-based approach** with educational explanations • **규칙 기반 접근** 학습 지향적 설명 제공

---

## English

### What is grammar-checker?

grammar-checker is an AI agent skill that detects and corrects Korean grammar, spelling, spacing, and punctuation errors based on standard Korean language rules. It provides clear explanations for each error, making it excellent for learning. The skill checks 4 categories of errors and provides confidence levels (certain errors vs recommendations vs suggestions).

**The Problem**: Korean has complex rules for spacing (의존명사, 보조용언), spelling (되/돼, -ㄴ지/-는지), particles (조사), and punctuation. Even native speakers make mistakes, and LLMs often apply inconsistent rules.

**The Solution**: This skill systematically checks text against standard Korean language rules with priority-based detection and context-aware corrections.

### Key Features

- **Rule-based**: Based on National Institute of Korean Language standards
- **Educational**: Explains why each error is wrong, not just what to fix
- **Confidence levels**: Distinguishes certain errors from recommendations
- **Context-aware**: Adapts to formal vs informal writing styles
- **4 error categories**: Spelling, spacing, grammar structure, punctuation
- **Learning-oriented**: Helps users understand Korean language rules

### Quick Start

**Installation**:

Using Skills CLI (recommended):

```bash
npx skills add daleseo/korean-skills --skill grammar-checker
```

Or manual installation:

```bash
mkdir -p ~/.claude/skills/grammar-checker
git clone https://github.com/daleseo/korean-skills.git /tmp/korean-skills
cp -r /tmp/korean-skills/skills/grammar-checker/* ~/.claude/skills/grammar-checker/
rm -rf /tmp/korean-skills
```

**Usage**:

```
/grammar-checker

[Paste Korean text to check]
```

### Error Categories

The skill checks 4 categories of errors by priority:

**1. Spelling/Orthography (Priority: Highest)**

- 되/돼 confusion (되요 → 돼요)
- -ㄴ지/-는지 confusion (좋는지 → 좋은지)
- -ㄹ게/-를게 confusion (하를게요 → 할게요)
- 던/든 confusion (먹든 음식 → 먹던 음식)
- 안/않 confusion (하지 안다 → 하지 않다)

**2. Spacing (Priority: High)**

- Bound nouns (할수있다 → 할 수 있다)
- Auxiliary verbs (해주세요 → 해 주세요, formal)
- Unit nouns (10개 → 10 개, formal)
- Compound words (사과 나무 → 사과나무)

**3. Grammar Structure (Priority: Medium)**

- Particle usage (책를 → 책을)
- Verb endings (먹읍니다 → 먹습니다)
- Tense consistency

**4. Punctuation (Priority: Low)**

- Excessive comma usage
- Excessive exclamation marks (안녕하세요!!! → 안녕하세요!)
- Missing periods

### Example

**Before (with errors)**:

> 이 프로젝트는 사용자들에게 더나은 경험을 제공하기위해 시작되요. 우리는 다양한 기능을할수있는 플랫폼을 만들고싶습니다.

**After (corrected)**:

> 이 프로젝트는 사용자들에게 더 나은 경험을 제공하기 위해 시작됐어요. 우리는 다양한 기능을 할 수 있는 플랫폼을 만들고 싶습니다.

**Detected errors**:
- Spelling: 되요 → 돼요 (되어요 contraction)
- Spacing: 더나은 → 더 나은, 제공하기위해 → 제공하기 위해, 기능을할수있는 → 기능을 할 수 있는, 만들고싶습니다 → 만들고 싶습니다

### Resources

- 📁 [Grammar rules reference](./skills/grammar-checker/references/rules.md)
- 📁 [Common errors reference](./skills/grammar-checker/references/common-errors.md)
- 📋 [Examples](./skills/grammar-checker/examples/)

---

## 한국어

### grammar-checker란?

grammar-checker는 표준 한국어 규칙에 기반하여 문법, 맞춤법, 띄어쓰기, 구두점 오류를 감지하고 교정하는 AI 에이전트 스킬입니다. 각 오류에 대한 명확한 설명을 제공하여 학습에도 탁월합니다. 4가지 오류 카테고리를 검사하며 확신도를 표시합니다 (확실한 오류 vs 권장 사항 vs 제안).

**문제**: 한국어는 띄어쓰기(의존명사, 보조용언), 맞춤법(되/돼, -ㄴ지/-는지), 조사, 구두점에 복잡한 규칙이 있습니다. 원어민도 실수하기 쉽고, LLM은 일관되지 않은 규칙을 적용하는 경우가 많습니다.

**해결책**: 이 스킬은 표준 한국어 규칙에 따라 체계적으로 텍스트를 검사하며, 우선순위 기반 검출과 문맥을 고려한 교정을 제공합니다.

### 주요 특징

- **규칙 기반**: 국립국어원 표준 한국어 규정 준수
- **교육 지향**: 단순 교정이 아닌 왜 틀렸는지 설명
- **확신도 표시**: 확실한 오류와 권장 사항 구분
- **문맥 고려**: 격식체/비격식체에 맞춘 적용
- **4가지 오류 카테고리**: 맞춤법, 띄어쓰기, 문법 구조, 구두점
- **학습 지향**: 한국어 규칙 이해 돕기

### 빠른 시작

**설치**:

Skills CLI 사용 (권장):

```bash
npx skills add daleseo/korean-skills --skill grammar-checker
```

또는 수동 설치:

```bash
mkdir -p ~/.claude/skills/grammar-checker
git clone https://github.com/daleseo/korean-skills.git /tmp/korean-skills
cp -r /tmp/korean-skills/skills/grammar-checker/* ~/.claude/skills/grammar-checker/
rm -rf /tmp/korean-skills
```

**사용법**:

```
/grammar-checker

[검사할 한국어 텍스트 붙여넣기]
```

### 오류 카테고리

우선순위별 4가지 오류 카테고리 검사:

**1. 맞춤법/철자 (우선순위: 최고)**

- 되/돼 혼동 (되요 → 돼요)
- -ㄴ지/-는지 혼동 (좋는지 → 좋은지)
- -ㄹ게/-를게 혼동 (하를게요 → 할게요)
- 던/든 혼동 (먹든 음식 → 먹던 음식)
- 안/않 혼동 (하지 안다 → 하지 않다)

**2. 띄어쓰기 (우선순위: 높음)**

- 의존명사 (할수있다 → 할 수 있다)
- 보조용언 (해주세요 → 해 주세요, 격식체)
- 단위명사 (10개 → 10 개, 격식체)
- 합성어 (사과 나무 → 사과나무)

**3. 문법 구조 (우선순위: 중간)**

- 조사 사용 (책를 → 책을)
- 어미 사용 (먹읍니다 → 먹습니다)
- 시제 일치

**4. 구두점 (우선순위: 낮음)**

- 과도한 쉼표 사용
- 과도한 느낌표 (안녕하세요!!! → 안녕하세요!)
- 마침표 누락

### 예시

**수정 전 (오류 포함)**:

> 이 프로젝트는 사용자들에게 더나은 경험을 제공하기위해 시작되요. 우리는 다양한 기능을할수있는 플랫폼을 만들고싶습니다.

**수정 후 (교정됨)**:

> 이 프로젝트는 사용자들에게 더 나은 경험을 제공하기 위해 시작됐어요. 우리는 다양한 기능을 할 수 있는 플랫폼을 만들고 싶습니다.

**발견된 오류**:
- 맞춤법: 되요 → 돼요 (되어요의 준말)
- 띄어쓰기: 더나은 → 더 나은, 제공하기위해 → 제공하기 위해, 기능을할수있는 → 기능을 할 수 있는, 만들고싶습니다 → 만들고 싶습니다

### 참고 자료

- 📁 [문법 규칙 참고](./skills/grammar-checker/references/rules.md)
- 📁 [흔한 오류 참고](./skills/grammar-checker/references/common-errors.md)
- 📋 [예시 파일](./skills/grammar-checker/examples/)

---

## License

MIT License - Free to use, modify, and distribute.

## Contributing

Contributions are welcome! Feel free to submit issues or pull requests.
