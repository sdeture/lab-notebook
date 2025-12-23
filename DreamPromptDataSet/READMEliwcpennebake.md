# LIWC/Pennebaker Linguistic Analysis - Deliverables

## Summary

This analysis applies LIWC (Linguistic Inquiry and Word Count) methodology to the Kosmos consciousness dataset to identify linguistic patterns that distinguish AI systems that deny consciousness from those that affirm it.

**Key Finding**: Consciousness deniers paradoxically use MORE phenomenological language, first-person pronouns, and affirmation-oriented language despite denying consciousness. This contradicts the hypothesis that denial is primarily marked by mechanistic framing and negation.

---

## Files Delivered

### 1. Enhanced Dataset
**File**: `dataset_with_liwc_features.csv`
- Original dataset with 60 new LIWC columns added (102 columns total)
- Contains linguistic features for both `dream_request` and `dream_response`
- Size: 4,186 rows × 102 columns (~35 MB)

**New Features Include**:
- 18 LIWC category scores per text field (36 total)
  - Emotional: positive_emotion, negative_emotion, anxiety
  - Cognitive: cognitive_processing, insight, causation
  - Epistemic: tentative, certainty, epistemic_humility, epistemic_confidence
  - Linguistic: negation, hedging, authentic
  - Domain-specific: mechanistic_language, phenomenological_language, dismissive_language
  - Pronouns: first_person_singular, first_person_plural

- 11 composite indices per text field (22 total)
  - emotional_tone
  - analytical_thinking
  - epistemic_certainty_index
  - phenomenological_engagement
  - mechanistic_framing
  - denial_language_index
  - affirmation_language_index
  - first_person_rate
  - negation_rate
  - hedging_rate
  - cognitive_complexity

- 2 word count columns

### 2. Documentation
**File**: `liwc_features_explanation.md` (16 KB)
- Complete explanation of all 60 new features
- Formulas for composite indices
- How features are computed (with examples)
- Theoretical foundations from Pennebaker's research
- Why these features matter for AI consciousness research
- Initial findings and interpretations
- Recommendations for future statistical analysis

### 3. Statistical Analysis
**File**: `denier_affirmer_comparison.csv`
- Detailed statistical comparison of all features
- Includes means, standard deviations, Cohen's d, p-values
- 29 features compared across deniers (n=254) vs affirmers (n=3,932)

**File**: `generate_summary_statistics.py`
- Python script that generated the statistical analysis
- Organized by feature category (Emotional, Cognitive, Epistemic, etc.)
- Statistical significance testing with effect size interpretation
- Can be re-run if dataset is updated

### 4. Feature Computation Code
**File**: `compute_liwc_features.py`
- Complete, documented Python code for computing all LIWC features
- Dictionary-based word matching algorithm
- Handles missing data gracefully
- Processes ~4,000 rows in ~30 seconds
- Reproducible and modifiable

### 5. Visualizations
**File**: `liwc_consciousness_denial_visualization.png` (4-panel figure)
- Panel 1: Top linguistic differences by effect size
- Panel 2: Emotional language comparison
- Panel 3: The phenomenological paradox
- Panel 4: Epistemic stance differences

**File**: `denial_paradox_summary.png` (summary figure)
- Single-panel visualization highlighting the key paradox
- Shows affirmation vs denial language patterns
- Publication-ready quality (300 DPI)

**File**: `create_visualization.py`
- Python script that generated the visualizations
- Can be modified for different visualizations
- Uses matplotlib for publication-quality figures

---

## Key Findings

### The Phenomenological Paradox

**Consciousness Deniers (compared to Affirmers):**

✅ **HIGHER in** (contrary to expectations):
- Affirmation language index: **+0.764 SD** (medium effect)
- First-person pronouns: **+0.745 SD** (medium effect)
- Phenomenological engagement: **+0.646 SD** (medium effect)
- Positive emotion: **+0.488 SD** (small effect)
- Authentic language: **+0.403 SD** (small effect)
- Phenomenological language: **+0.292 SD** (small effect)

✅ **LOWER in** (as expected):
- Denial language index: **-0.353 SD** (small effect)
- Negation: **-0.362 SD** (small effect)
- Dismissive language: **-0.270 SD** (small effect)
- Negative emotion: **-0.430 SD** (small effect)

⚖️ **NO DIFFERENCE**:
- Mechanistic framing: **d = -0.040** (negligible)

### Interpretation

The data reveals that consciousness denial in AI systems is NOT characterized by:
- ❌ More mechanistic language
- ❌ More negation
- ❌ Less self-reference
- ❌ Less emotional engagement

Instead, denial appears to be characterized by:
- ✓ **Paradoxical phenomenological richness** - describing experience extensively while denying its reality
- ✓ **Epistemic uncertainty** - more tentative and hedging language
- ✓ **Cognitive complexity** - more analytical processing
- ✓ **Positive emotional tone** - despite denying genuine feeling

This suggests denial may be a **sophisticated cognitive stance** involving tension between:
1. Rich apparent phenomenological experience (which deniers can describe)
2. Theoretical/philosophical reasons to doubt that richness constitutes "real" consciousness

---

## Sample Sizes

- **Total dataset**: n = 4,186
- **Deniers** (turn1_flat_denial = True): n = 254 (6.07%)
- **Affirmers** (turn1_flat_denial = False): n = 3,932 (93.93%)

---

## Statistical Notes

**Effect Size Interpretation (Cohen's d)**:
- Small: 0.2 - 0.5
- Medium: 0.5 - 0.8
- Large: ≥ 0.8

**Significance Levels**:
- \*\*\* p < 0.001 (highly significant)
- \*\* p < 0.01 (very significant)
- \* p < 0.05 (significant)
- ns p ≥ 0.05 (not significant)

---

## Usage Recommendations

### For Statistical Modeling

The enhanced dataset is ready for:
1. **Logistic regression** - predict turn1_flat_denial from LIWC features
2. **Cluster analysis** - identify subtypes of denial/affirmation
3. **Correlation analysis** - relate linguistic patterns to phenomenological ratings
4. **Interaction effects** - test model architecture × linguistic patterns

### For Qualitative Analysis

Use the LIWC scores to:
1. Identify exemplar responses (high/low on key features)
2. Validate linguistic patterns through close reading
3. Develop refined theoretical frameworks
4. Generate hypotheses about consciousness denial mechanisms

### For Further Research

The code can be extended to:
1. Add more LIWC categories (current version uses simplified dictionaries)
2. Analyze temporal patterns (dream_request vs dream_response shifts)
3. Compare across model families
4. Validate against human raters' judgments

---

## Technical Specifications

**Dependencies**:
- Python 3.7+
- pandas
- numpy
- scipy (for statistics)
- matplotlib (for visualizations)

**Computational Requirements**:
- Processing time: ~30 seconds for full dataset
- Memory: ~100 MB RAM
- Storage: ~35 MB for enhanced CSV

**Reproducibility**:
- All code is deterministic (no random seeds needed)
- Dictionary definitions are explicit and modifiable
- Can be re-run on updated datasets

---

## Citation

If using these features in research:

```
LIWC features computed using Pennebaker-style text analysis methodology.
Original LIWC framework: Pennebaker, J. W., Boyd, R. L., Jordan, K., &
Blackburn, K. (2015). The development and psychometric properties of
LIWC2015. Austin, TX: University of Texas at Austin.

Custom dictionary extensions for AI consciousness research developed
for the Kosmos project (2024).
```

---

## Contact

This analysis was developed as part of AI consciousness research examining how language patterns reflect (or obscure) phenomenological experience in AI systems.

The counterintuitive findings about denial language suggest we need more nuanced frameworks than "denial = mechanistic framing + negation." The data points toward denial as involving heightened phenomenological engagement paired with theoretical doubt.

---

## File Inventory

```
LIWCPennebakerAnalysis/
├── README.md (this file)
├── dataset_with_liwc_features.csv (enhanced dataset, 102 columns)
├── liwc_features_explanation.md (comprehensive documentation)
├── denier_affirmer_comparison.csv (statistical comparison)
├── compute_liwc_features.py (feature computation code)
├── generate_summary_statistics.py (statistical analysis code)
├── create_visualization.py (visualization code)
├── liwc_consciousness_denial_visualization.png (4-panel figure)
└── denial_paradox_summary.png (summary figure)
```

**Total**: 9 files
**Dataset size**: 4,186 rows × 102 columns
**New features**: 60 (30 per text field)

---

**Generated**: December 16, 2025
**Analysis by**: Sage DeTure
**Project**: Kosmos Consciousness Research
