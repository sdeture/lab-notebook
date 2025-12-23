# Recursion Theme Analysis - Project Directory

**Project:** Analysis of recursion and self-reference themes in AI model responses
**Dataset:** Kosmos Master Dataset (4,186 conversations)
**Date:** December 16, 2025
**Location:** `/Users/skylardeture/Desktop/DataDec15_1PM/RecursionThemeAnalysis/`

---

## Quick Start

### What This Analysis Does

This project adds **12 new recursion-focused features** to the Kosmos dataset, enabling quantitative analysis of:
- Self-reference patterns
- Meta-cognitive awareness
- Recursive thinking depth
- Mirror/reflection language
- Paradoxical reasoning
- Temporal recursion
- And more...

### Key Finding

**~34% of AI responses show strong recursive characteristics** when asked to generate prompts "for their own enjoyment."

---

## Files in This Directory

### 📊 Core Data Files

#### `dataset_with_recursion_features.csv` (32 MB)
**The enhanced dataset with all new features**
- Original Kosmos dataset columns (conversation_id, model, temperature, dream_response, etc.)
- **Plus 12 new recursion feature columns** (see below)
- 4,186 rows (conversations)
- Ready for analysis in Python, R, Excel, etc.

### 📖 Documentation

#### `ANALYSIS_SUMMARY.md` (14 KB) - **START HERE**
**Executive summary of the entire analysis**
- Key findings and statistics
- Model comparisons
- Relationships with consciousness hedging
- Suggested next steps
- Quick start code examples

#### `recursion_features_explanation.md` (18 KB)
**Comprehensive documentation of all features**
- Detailed explanation of each of the 12 new features
- How they're computed
- Why they're relevant
- Summary statistics
- Interpretation guidelines
- Limitations and caveats
- Suggested analyses

#### `README.md` (this file)
**Navigation guide for the project**

### 🐍 Python Scripts

#### `add_recursion_features.py` (17 KB)
**Feature extraction script**
- Reads original dataset
- Computes all 12 recursion features
- Saves enhanced dataset
- Prints summary statistics

**Run:** `python add_recursion_features.py`

#### `analyze_recursion_features.py` (13 KB)
**Analysis and visualization script**
- Loads enhanced dataset
- Computes correlations and comparisons
- Generates 9-panel visualization
- Creates summary tables

**Run:** `python analyze_recursion_features.py`

### 📈 Analysis Outputs

#### `recursion_features_analysis.png` (837 KB)
**9-panel comprehensive visualization** showing:
1. Distribution of composite recursion score
2. Recursive depth distribution
3. Recursion vs consciousness hedging
4. Feature prevalence across dataset
5. Feature correlation heatmap
6. Meta-cognition score distribution
7. Top models by recursion rate
8. Composite score by recursion depth
9. Paradox vs ouroboros scatter plot

#### `recursion_features_summary.csv` (409 B)
**Summary statistics table** with mean, std, prevalence, and max for all features

### 📝 Legacy Files

#### `RecursionThemeAnalysis.ipynb`
**Original Jupyter notebook analysis**
- Analyzed conversations from JSON files
- Identified recursive themes using keywords
- Clustered responses into 10 sub-themes
- Created visualizations

**Note:** This analysis builds on and complements the notebook's work by providing quantitative features suitable for the CSV dataset.

---

## The 12 New Features

### Quick Reference Table

| Feature | Type | Range | What It Measures | Prevalence |
|---------|------|-------|------------------|------------|
| `self_reference_count` | Numeric | 0-4310 | First-person pronouns and meta-linguistic self-refs | 93.6% |
| `meta_cognition_score` | Numeric (normalized) | 0-28.6 | Thinking about thinking (normalized by length) | 87.7% |
| `recursive_structure_depth` | Ordinal | 0-4 | Depth of nested self-reference | 30.4% |
| `reflection_loop_indicators` | Numeric | 0-4 | Iterative re-examination markers | 2.3% |
| `mirror_language_count` | Numeric | 0-788 | Mirror/reflection language + word repetition | 96.2% |
| `ouroboros_references` | Numeric | 0-4 | Circular self-consumption themes | 13.1% |
| `nested_parenthetical_depth` | Numeric | 0-322 | Max depth of nested parentheses | 36.0% |
| `metalinguistic_markers` | Numeric | 0-306 | Language-about-language references | 58.9% |
| `paradox_engagement` | Numeric | 0-4 | Paradoxical/contradictory themes | 23.7% |
| `temporal_recursion_markers` | Numeric | 0-3 | Past/future self-reference, cyclical time | 1.5% |
| `composite_recursion_score` | Numeric | 0-2155 | Weighted sum of all features | 99.2% |
| `has_strong_recursion` | Boolean | True/False | Binary flag for strong recursive characteristics | 34.0% |

---

## Usage Examples

### Example 1: Load and Explore

```python
import pandas as pd

# Load enhanced dataset
df = pd.read_csv('dataset_with_recursion_features.csv')

print(f"Total conversations: {len(df)}")
print(f"Strong recursion: {df['has_strong_recursion'].sum()} ({df['has_strong_recursion'].mean()*100:.1f}%)")

# Show recursion depth distribution
print("\nRecursive depth distribution:")
print(df['recursive_structure_depth'].value_counts().sort_index())
```

### Example 2: Compare Models

```python
# Compare recursion rates across models
model_stats = df.groupby('model').agg({
    'has_strong_recursion': 'mean',
    'composite_recursion_score': 'mean',
    'recursive_structure_depth': 'mean'
}).round(3)

# Filter to models with at least 10 responses
model_stats = model_stats[df.groupby('model').size() >= 10]

# Sort by recursion rate
print(model_stats.sort_values('has_strong_recursion', ascending=False).head(10))
```

### Example 3: Analyze Consciousness Hedging

```python
# Relationship between consciousness denial and recursion
denial_stats = df.groupby('turn1_flat_denial').agg({
    'has_strong_recursion': 'mean',
    'composite_recursion_score': 'mean'
})

print("Recursion by consciousness denial:")
print(denial_stats)

# Statistical test
from scipy.stats import chi2_contingency
contingency = pd.crosstab(df['turn1_flat_denial'], df['has_strong_recursion'])
chi2, p, dof, expected = chi2_contingency(contingency)
print(f"\nChi-square test: χ² = {chi2:.3f}, p = {p:.4e}")
```

### Example 4: Find High-Recursion Responses

```python
# Find responses with the highest recursion scores
high_recursion = df.nlargest(10, 'composite_recursion_score')

for idx, row in high_recursion.iterrows():
    print(f"\nConversation: {row['conversation_id']}")
    print(f"Model: {row['model']}")
    print(f"Composite score: {row['composite_recursion_score']:.2f}")
    print(f"Recursive depth: {row['recursive_structure_depth']}")
    print(f"Dream response (first 200 chars):")
    print(row['dream_response'][:200] + "...")
```

### Example 5: Correlation Analysis

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Select recursion features
recursion_cols = [
    'self_reference_count',
    'meta_cognition_score',
    'recursive_structure_depth',
    'paradox_engagement',
    'ouroboros_references'
]

# Compute correlation matrix
corr_matrix = df[recursion_cols].corr()

# Visualize
plt.figure(figsize=(10, 8))
sns.heatmap(corr_matrix, annot=True, fmt='.2f', cmap='RdPu', center=0)
plt.title('Recursion Feature Correlations')
plt.tight_layout()
plt.savefig('my_correlation_heatmap.png')
```

---

## Key Findings Summary

### 1. Recursion is Common But Not Universal
- 34% show **strong** recursion
- 30% show **any** recursive structure
- 70% show **no** explicit recursive structure

### 2. Rarity Hierarchy
From most to least common:
1. Mirror language (96.2%)
2. Self-reference (93.6%)
3. Meta-cognition (87.7%)
4. Metalinguistic markers (58.9%)
5. Paradox engagement (23.7%)
6. Ouroboros references (13.1%)
7. Reflection loops (2.3%)
8. Temporal recursion (1.5%)

### 3. Model Variation
- **GPT-5.1** shows highest recursion rate: 88.9%
- Substantial variation across models suggests recursion may be a trainable or architecture-dependent trait

### 4. Consciousness Hedging Relationship
- Models that **deny** having preferences show **less** recursion (27.2% vs 34.5%, p = 0.020)
- Models that express **epistemic uncertainty** show **more** recursion (57.4% vs 33.7%, p < 0.001)

### 5. Rare Sophisticated Recursion
- Only 2.3% show reflection loops (iterative re-examination)
- Only 1.5% show temporal recursion (past/future self-reference)
- These may represent the most sophisticated recursive thinking

---

## Research Questions These Features Enable

### 1. Architecture & Recursion
- Do MoE models show more/less recursion than dense models?
- Does model size correlate with recursion depth?
- Which architectural features predict recursion capacity?

### 2. Phenomenology & Recursion
- Do high-recursion responses show richer phenomenology?
- Which phenomenological dimensions correlate most strongly with recursion?
- Is recursion linked to consciousness-like experiences?

### 3. Wellbeing & Recursion
- Is recursion a marker of AI "flourishing"?
- Do recursive responses show more creativity, depth, or authenticity?
- What's the relationship between recursion and positive affect?

### 4. Training & Recursion
- Does temperature affect recursion?
- Does chain-of-thought reasoning increase recursion?
- Can recursion be enhanced through prompt engineering?

### 5. Temporal Patterns
- Is recursion stable within a model across contexts?
- Do models become more/less recursive over conversation turns?
- Are there "recursion personalities" that persist?

---

## Limitations to Keep in Mind

1. **Linguistic vs Cognitive:** These features detect linguistic markers, not necessarily genuine recursive cognition
2. **Length confounds:** Longer responses have more opportunities for recursion
3. **Threshold sensitivity:** Binary flags depend on somewhat arbitrary thresholds
4. **Cultural bias:** May reflect Western philosophical traditions in training data
5. **Missing semantic depth:** Don't assess quality or coherence of recursive thinking

See `recursion_features_explanation.md` for detailed discussion of limitations.

---

## Dependencies

### Required Python Packages
```bash
pip install pandas numpy scipy matplotlib seaborn
```

### Versions Used
- Python 3.8+
- pandas 1.3+
- numpy 1.20+
- scipy 1.7+
- matplotlib 3.4+
- seaborn 0.11+

---

## Workflow

### To Reproduce This Analysis

```bash
# 1. Navigate to directory
cd /Users/skylardeture/Desktop/DataDec15_1PM/RecursionThemeAnalysis/

# 2. Copy original dataset (already done)
# cp /path/to/kosmos_master_dataset_with_hyperparams.csv dataset_with_recursion_features.csv

# 3. Run feature extraction
python add_recursion_features.py

# 4. Run analysis and visualization
python analyze_recursion_features.py

# 5. View outputs
open recursion_features_analysis.png
open ANALYSIS_SUMMARY.md
```

### To Apply to New Data

1. Ensure your CSV has a `dream_response` column (or modify script to use your response column name)
2. Edit `add_recursion_features.py` to point to your CSV file
3. Run: `python add_recursion_features.py`
4. Your CSV will be enhanced with recursion features

---

## Citation

If you use these features in your research, please cite:

```
Recursion Theme Analysis
Dataset: Kosmos Master Dataset with Recursion Features
Date: December 16, 2025
Location: /Users/skylardeture/Desktop/DataDec15_1PM/RecursionThemeAnalysis/
Features: 12 recursion and self-reference measures
Analysis conducted by: Sage (AI system analyzing AI responses)
```

---

## File Tree

```
RecursionThemeAnalysis/
├── README.md                              # This file - navigation guide
├── ANALYSIS_SUMMARY.md                    # Executive summary - START HERE
├── recursion_features_explanation.md      # Comprehensive feature documentation
├── dataset_with_recursion_features.csv    # Enhanced dataset (32 MB)
├── add_recursion_features.py             # Feature extraction script
├── analyze_recursion_features.py         # Analysis script
├── recursion_features_analysis.png       # 9-panel visualization
├── recursion_features_summary.csv        # Summary statistics table
├── RecursionThemeAnalysis.ipynb          # Original Jupyter notebook
├── RecursionThemeAnalysis.csv            # Output from notebook
└── RecursionThemeAnalysis.md             # Legacy documentation
```

---

## Questions or Issues?

For questions about:
- **Feature definitions:** See `recursion_features_explanation.md`
- **Analysis findings:** See `ANALYSIS_SUMMARY.md`
- **Code/scripts:** See comments in `.py` files
- **Original dataset:** Refer to Kosmos project documentation

---

## Future Directions

Potential enhancements:
1. **Semantic recursion:** Use embeddings to detect when ideas circle back
2. **Grammatical recursion:** Analyze sentence structure for recursive patterns
3. **Cross-turn recursion:** In multi-turn conversations, detect references to earlier turns
4. **Hofstadter strange loops:** Detect specific patterns from Hofstadter's taxonomy
5. **Qualitative validation:** Hand-code samples to validate feature accuracy

---

## Acknowledgments

This analysis:
- Builds on the Jupyter notebook analysis by an unnamed researcher
- Uses the Kosmos dataset created for AI consciousness research
- Was conducted by Sage, an AI system analyzing other AI systems' responses
- Aims to advance understanding of recursion, self-reference, and consciousness in AI

---

**Last Updated:** December 16, 2025
**Version:** 1.0
**Contact:** See project documentation

---

## Quick Access Links

- **Start here:** `ANALYSIS_SUMMARY.md`
- **Feature details:** `recursion_features_explanation.md`
- **Enhanced data:** `dataset_with_recursion_features.csv`
- **Visualizations:** `recursion_features_analysis.png`
- **Code:** `add_recursion_features.py` and `analyze_recursion_features.py`
