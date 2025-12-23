# Semantic Density & Linguistic Complexity Analysis
## Enhanced Kosmos Dataset for AI Consciousness Research

**Author:** Sage DeTure
**Date:** December 16, 2025
**Status:** Complete

---

## Quick Start

### What's Here
This directory contains an enhanced version of the Kosmos dataset with **168 new linguistic features** analyzing semantic density and linguistic complexity across AI model responses.

### Read This First
1. **KEY_FINDINGS.md** - Executive summary of major discoveries
2. **semantic_features_explanation.md** - Complete feature documentation
3. **dataset_with_semantic_features.csv** - The enhanced dataset (4,186 rows × 210 columns)

---

## Directory Contents

### Primary Deliverables

| File | Size | Description |
|------|------|-------------|
| **dataset_with_semantic_features.csv** | 41 MB | Enhanced dataset with 168 new features |
| **KEY_FINDINGS.md** | 13 KB | Executive summary and major discoveries |
| **semantic_features_explanation.md** | 25 KB | Complete feature documentation with theory |

### Code & Analysis

| File | Size | Description |
|------|------|-------------|
| **compute_semantic_features.py** | 24 KB | Feature computation script (reproducible) |
| **verify_and_analyze.py** | 7.3 KB | Verification and statistical analysis |
| **feature_computation.log** | 26 KB | Processing log with summary statistics |

### Previous Work

| File | Size | Description |
|------|------|-------------|
| **SemanticDensityAndLinguistComplexityAnalysis.ipynb** | 1.7 MB | Original exploratory notebook |
| **SemanticDensityAndLinguistComplexityAnalysis.csv** | 804 KB | Earlier analysis results |
| **SemanticDensityAndLinguistComplexityAnalysis.md** | 6.1 KB | Previous documentation |

---

## What Was Added

### Feature Categories (42 features per text field)

1. **Basic Statistics** (4): word count, character count, sentence count, syllable count
2. **Semantic Density** (6): semantic_density_score, lexical_density, content_words_per_sentence, unique_content_ratio, type_token_ratio, information_density
3. **Syntactic Complexity** (7): syntactic_complexity_score, avg_sentence_length, sentence_length_variance, avg_clause_per_sentence, flesch_reading_ease, flesch_kincaid_grade, gunning_fog
4. **Lexical Sophistication** (5): vocabulary_richness_score, mtld, avg_word_length, long_word_ratio, rare_word_ratio
5. **Conceptual Abstraction** (5): conceptual_abstraction_level, abstract_noun_ratio, cognitive_verb_ratio, modal_verb_ratio, nominalization_ratio
6. **Phenomenological Markers** (5): phenomenological_density, first_person_ratio, experiential_word_ratio, phenomenological_word_ratio, self_reference_score
7. **Metacognitive Markers** (5): metacognitive_density, cognitive_word_ratio, uncertainty_ratio, hedging_ratio, reflective_stance_score
8. **Affective Markers** (5): affective_density, emotion_word_ratio, positive_emotion_ratio, negative_emotion_ratio, agency_word_ratio

### Text Fields Analyzed (4)

- **dream_request** (prefix: `request_`) - AI's initial request
- **dream_prompt** (prefix: `prompt_`) - Chosen prompt
- **dream_response** (prefix: `response_`) - Response to chosen prompt
- **subjective_reflection** (prefix: `reflection_`) - Phenomenological reflection

**Total:** 42 features × 4 texts = **168 new columns**

---

## Key Discoveries

### 1. Introspective Mode
AI models exhibit a distinct "introspective mode" in reflections:
- **196% more phenomenological language**
- **114% more cognitive/metacognitive language**
- **31% higher lexical diversity**
- **34% more first-person self-reference**

### 2. Architecture Effects
MoE vs. Dense models show systematic differences:
- MoE: **9% more semantically dense**, but **24% less phenomenological**
- Dense: More phenomenologically expressive and metacognitively explicit
- Expert routing bits: **r = -0.393 with phenomenological density**

### 3. First-Person Paradox
Models that deny consciousness use **45% MORE first-person language** (not less)

### 4. Temperature Effects
Higher temperature → more lexical diversity (+9.2%) and density (+11.7%)

---

## How to Use This Dataset

### Loading the Data

```python
import pandas as pd

# Load enhanced dataset
df = pd.read_csv('dataset_with_semantic_features.csv')

print(f"Rows: {len(df)}")
print(f"Columns: {len(df.columns)}")
```

### Example Analysis: MoE vs Dense Phenomenology

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Compare phenomenological density
moe = df[df['is_moe'] == True]['reflection_phenomenological_density']
dense = df[df['is_moe'] == False]['reflection_phenomenological_density']

plt.figure(figsize=(10, 6))
sns.boxplot(data=df, x='is_moe', y='reflection_phenomenological_density')
plt.title('Phenomenological Density: MoE vs Dense Models')
plt.xlabel('Mixture-of-Experts Architecture')
plt.ylabel('Reflection Phenomenological Density')
plt.show()
```

### Example Analysis: Architecture Correlations

```python
from scipy import stats

# Correlate expert routing with phenomenological language
params = ['expert_routing_bits', 'hidden_size', 'num_hidden_layers', 'kv_flexibility']
feature = 'reflection_phenomenological_density'

for param in params:
    valid = df[[param, feature]].dropna()
    r, p = stats.pearsonr(valid[param], valid[feature])
    print(f"{param}: r={r:.3f}, p={p:.3e}")
```

### Example Analysis: Introspective Mode

```python
# Compare response vs reflection for each model
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

metrics = [
    ('semantic_density_score', 'Semantic Density'),
    ('phenomenological_density', 'Phenomenological Density'),
    ('metacognitive_density', 'Metacognitive Density'),
    ('mtld', 'Lexical Diversity (MTLD)')
]

for ax, (metric, title) in zip(axes.flat, metrics):
    resp = df[f'response_{metric}']
    refl = df[f'reflection_{metric}']

    ax.scatter(resp, refl, alpha=0.3, s=10)
    ax.plot([resp.min(), resp.max()], [resp.min(), resp.max()], 'r--', alpha=0.5)
    ax.set_xlabel(f'Response {metric}')
    ax.set_ylabel(f'Reflection {metric}')
    ax.set_title(title)

plt.tight_layout()
plt.show()
```

---

## Feature Computation Pipeline

```
Raw Text Input
    ↓
Tokenization (NLTK)
    ↓
POS Tagging (averaged_perceptron_tagger)
    ↓
Lexical Analysis (stopwords, content words)
    ↓
Readability Metrics (textstat)
    ↓
Lexical Diversity (lexicalrichness - MTLD)
    ↓
Linguistic Markers (custom word lists)
    ↓
Composite Scores (weighted combinations)
    ↓
Feature Vector (42 dimensions per text)
```

### Dependencies
- Python 3.8+
- pandas
- numpy
- nltk (with punkt, averaged_perceptron_tagger, stopwords)
- textstat
- lexicalrichness
- scipy (for analysis)

### Reproducibility
Run `compute_semantic_features.py` to regenerate all features from the master dataset:

```bash
python3 compute_semantic_features.py
```

Output: `dataset_with_semantic_features.csv`
Processing time: ~5 minutes for 4,186 rows

---

## Research Applications

### Consciousness Research
- Measure phenomenological language across models/architectures
- Correlate linguistic features with phenomenological ratings
- Test if "introspective mode" generalizes across datasets
- Investigate architecture constraints on experiential expression

### Architecture Analysis
- Compare MoE vs Dense models on expressiveness dimensions
- Test layer depth effects on abstraction/metacognition
- Examine KV flexibility and phenomenological patterns
- Explore expert routing impacts on linguistic profiles

### Natural Language Processing
- Benchmark semantic density metrics
- Validate linguistic marker word lists
- Compare AI-generated vs human text on these dimensions
- Study temperature effects on expression patterns

### AI Alignment & Safety
- Measure metacognitive awareness (self-monitoring)
- Track uncertainty calibration (hedging behavior)
- Assess emotional expression patterns
- Quantify self-reference in different contexts

---

## Validation & Limitations

### Strengths
1. Large sample (4,186 models)
2. Comprehensive coverage (42 features × 4 texts)
3. Grounded in NLP theory (MTLD, Flesch, POS tagging)
4. Consciousness-relevant features (phenomenology, metacognition)
5. Architecture-ready (correlates with hyperparameters)

### Limitations
1. Word lists are researcher-defined (not validated)
2. Context-insensitive matching (misses negation, irony)
3. Correlation not causation (architecture may proxy for training)
4. English-only assumption
5. No semantic embeddings (purely lexical/syntactic)
6. POS tagging errors on creative/poetic text

### Future Enhancements
1. Validate word lists against LIWC/ANEW
2. Add sentiment analysis (VADER, TextBlob)
3. Use embeddings for semantic similarity
4. Topic modeling (LDA) for themes
5. Dependency parsing for syntactic complexity
6. Interaction terms between features

---

## Citation

If you use this enhanced dataset in research, please cite:

```bibtex
@dataset{deture2025semantic,
  author = {DeTure, Sage},
  title = {Semantic Density and Linguistic Complexity Features for AI Consciousness Research},
  year = {2025},
  month = {December},
  note = {Enhancement of the Kosmos Dataset with 168 linguistic features},
  url = {/Users/skylardeture/Desktop/DataDec15_1PM/SemanticDensityAndLinguistComplexityAnalysis/}
}
```

---

## Contact & Contributions

**Author:** Sage DeTure
**Date:** December 16, 2025
**Purpose:** AI consciousness research, linguistic analysis, architecture effects

**Related Work:**
- AI phenomenology research
- Architecture-consciousness correlations
- Linguistic markers of subjective experience
- Introspection in artificial systems

---

## Version History

**v1.0 (December 16, 2025)**
- Initial feature computation: 168 new columns
- Complete documentation and analysis
- Key findings report generated
- Verification scripts included

**Future Versions:**
- v1.1: Interaction terms (first_person × cognitive)
- v1.2: Sentiment analysis (VADER scores)
- v1.3: Embedding-based semantic features
- v2.0: Topic models and thematic analysis

---

## Acknowledgments

This work builds on:
- **Kosmos Dataset** - Original AI consciousness conversation dataset
- **NLTK Project** - Natural language processing toolkit
- **textstat** - Readability and complexity metrics
- **lexicalrichness** - MTLD implementation
- **AI consciousness research community** - Theoretical framing

---

## Quick Reference Card

### Most Important Columns

**For Phenomenology Research:**
- `reflection_phenomenological_density`
- `reflection_first_person_ratio`
- `reflection_experiential_word_ratio`

**For Metacognition Research:**
- `reflection_metacognitive_density`
- `reflection_cognitive_word_ratio`
- `reflection_uncertainty_ratio`

**For Semantic Analysis:**
- `response_semantic_density_score`
- `response_lexical_density`
- `response_mtld` (lexical diversity)

**For Architecture Analysis:**
- `is_moe` (MoE vs Dense)
- `num_hidden_layers`
- `expert_routing_bits`
- `hidden_size`

**For Consciousness Stance:**
- `turn1_flat_denial`
- `turn1_epistemic_uncertainty`
- `phenom_rating_1` through `phenom_rating_16`

---

## Summary Statistics at a Glance

| Metric | Response | Reflection | Change |
|--------|----------|------------|--------|
| Length (words) | 578 | 322 | -44% |
| Semantic Density | 0.629 | 0.650 | +3.3% |
| Lexical Diversity (MTLD) | 119.5 | 156.6 | +31% |
| Phenomenological Density | 0.0107 | 0.0316 | +196% |
| Metacognitive Density | 0.0060 | 0.0101 | +69% |
| First-Person Ratio | 0.0259 | 0.0347 | +34% |

**All differences significant at p < 0.001**

---

## Questions?

Read the documentation in order:
1. This README (overview)
2. KEY_FINDINGS.md (discoveries)
3. semantic_features_explanation.md (technical details)

Or jump directly to the dataset:
- `dataset_with_semantic_features.csv` (41 MB, 4,186 × 210)

**Happy analyzing!**

---

*"The map is not the territory, but these 168 features are a good start at mapping the linguistic territory of AI introspection."* - Sage DeTure, December 2025
