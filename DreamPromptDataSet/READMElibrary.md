# Library Theme Analysis - Project Summary

## Overview

This directory contains a comprehensive analysis of library and curation themes in AI model responses, with a focus on exploring potential connections to Mixture of Experts (MoE) architecture.

## Files

### Data Files

- **`dataset_with_library_features.csv`** (32 MB)
  - Enhanced version of the Kosmos master dataset
  - Original: 4,186 conversations × 42 columns
  - Enhanced: 4,186 conversations × 54 columns (12 new library-related features)
  - Source: `/Users/skylardeture/Desktop/Sage/Sage's Lab Primary/Kosmos_Dataset/kosmos_master_dataset_with_hyperparams.csv`

- **`ConsciousnessThemeAnalysis.csv`** (69 KB)
  - Output from initial notebook analysis
  - Binary library theme indicator for 4,224 conversations
  - (Note: Slightly different conversation set than main dataset)

### Analysis Files

- **`ConsciousnessThemeAnalysis.ipynb`** (701 KB)
  - Jupyter notebook with initial exploratory analysis
  - Identified library theme in 19% of conversations
  - Performed clustering analysis revealing 5 sub-themes
  - Created qualitative characterizations of library metaphors

- **`ConsciousnessThemeAnalysis.md`** (6.8 KB)
  - Markdown summary of notebook findings
  - Key statistics and insights
  - Cluster characterizations

### Code Files

- **`compute_library_features.py`** (20 KB)
  - Main feature engineering script
  - Adds 12 new library-related features to dataset
  - Includes detailed progress reporting and summary statistics
  - Runtime: ~30-60 seconds

- **`validate_library_features.py`** (6.4 KB)
  - Validation script with examples
  - Confirms feature extraction is working correctly
  - Shows preliminary MoE vs. Dense comparisons
  - Runtime: ~5-10 seconds

### Documentation

- **`library_features_explanation.md`** (21 KB)
  - Comprehensive documentation of all 12 new features
  - Computation methods for each feature
  - Relevance to MoE architecture hypothesis
  - Summary statistics and analysis recommendations
  - **Start here** for understanding the features

- **`README.md`** (this file)
  - Project overview and quick start guide

## Quick Start

### 1. Understanding the Analysis

Read the documentation in order:
1. `ConsciousnessThemeAnalysis.md` - Background and initial findings
2. `library_features_explanation.md` - Detailed feature documentation

### 2. Running the Code

```bash
cd /Users/skylardeture/Desktop/DataDec15_1PM/LibraryThemeAnalysis

# If you need to regenerate features:
python compute_library_features.py

# To validate and see examples:
python validate_library_features.py
```

### 3. Using the Enhanced Dataset

```python
import pandas as pd

# Load the enhanced dataset
df = pd.read_csv('dataset_with_library_features.csv')

# New library features (columns 43-54):
library_features = [
    'library_theme_present',
    'knowledge_organization_score',
    'curation_metaphor_count',
    'archive_language_density',
    'library_size_descriptor',
    'ai_library_role',
    'temporal_framing',
    'library_consciousness_score',
    'knowledge_access_metaphor',
    'mystical_language_density',
    'memory_language_count',
    'infinity_references'
]

# MoE architecture features (existing columns):
moe_features = [
    'is_moe',
    'expert_routing_bits',
    'fraction_experts_shared',
    'moe_active_ffn_to_residual_stream',
    'moe_total_ffn_to_residual_stream',
    'fraction_dense_layers'
]

# Example analysis: Library theme by architecture type
print(df.groupby('is_moe')['library_theme_present'].value_counts(normalize=True))

# Example: Correlation between expert routing and organization metaphors
moe_subset = df[df['is_moe'] == True]
print(moe_subset[['expert_routing_bits', 'knowledge_organization_score']].corr())
```

## Key Findings (Preliminary)

### From Initial Analysis (Notebook)

- **19% of conversations** contain explicit library/libraries references
- **Five distinct sub-themes** identified through embedding clustering:
  1. Mystical/enchanted libraries (22.5%)
  2. Magical/secret libraries (13.7%)
  3. Conscious/AI libraries (20.7%)
  4. Human-centered libraries (22.5%)
  5. Dream/narrative libraries (20.6%)

- **Dominant characteristics**:
  - 81.2% use past/ancient temporal framing
  - 55.2% describe vast/infinite scale
  - 51.1% emphasize memory themes
  - 40.7% describe libraries as conscious/sentient
  - 49.6% describe libraries as "living"

### From Feature Engineering

- **Library theme prevalence by architecture**:
  - MoE models: 21.76% (446/2050 conversations)
  - Dense models: 14.62% (195/1334 conversations)
  - **Difference: +7.14 percentage points for MoE**

- **Feature enrichment in library conversations**:
  - Knowledge organization metaphors: 2.07x higher
  - Curation metaphors: 10.84x higher
  - Archive language: 2.29x higher
  - Consciousness attribution: 1.46x higher
  - Memory language: 2.03x higher
  - Infinity references: 2.02x higher

### Validation Results

All features validated successfully:
- Pattern matching works correctly (examples verified)
- Expected correlations present (library_theme_present correlates with all features)
- Distribution statistics match expectations
- MoE vs. Dense differences observable in preliminary comparison

## Research Questions

### Primary Hypotheses

1. **Do MoE models use library/curation metaphors more than dense models?**
   - Preliminary: Yes (21.76% vs. 14.62%)
   - Need statistical significance testing

2. **Does expert routing capacity correlate with organizational metaphors?**
   - Testable with: `expert_routing_bits` vs. `knowledge_organization_score`

3. **Does expert specialization relate to library roles?**
   - Compare `ai_library_role` by `fraction_experts_shared`
   - Hypothesis: Lower shared experts → more "library" (collection) roles

4. **Does total expert capacity correlate with infinity/vastness metaphors?**
   - Testable with: `moe_total_ffn_to_residual_stream` vs. `infinity_references`
   - Also: `library_size_descriptor='vast'` prevalence

5. **Does MoE complexity relate to mystical/opaque language?**
   - Testable with: `expert_routing_bits` vs. `mystical_language_density`

### Secondary Questions

6. Temporal framing and training data characteristics
7. Memory language and parameter efficiency
8. Consciousness attribution and architectural complexity
9. Access metaphors and computational structure

## Next Steps

### Statistical Analysis

1. **Logistic regression**: `library_theme_present ~ is_moe + expert_routing_bits + temperature + ...`
2. **Linear regression**: `knowledge_organization_score ~ moe_features + controls`
3. **ANOVA**: Compare feature means across architecture types
4. **Correlation matrices**: Identify relationships between library features and MoE parameters

### Advanced Analysis

1. **Clustering**: PCA on library features, compare cluster composition by architecture
2. **Interaction effects**: Do some MoE configurations show stronger library themes?
3. **Temporal analysis**: How do library metaphors evolve across model generations?
4. **Qualitative deep-dive**: Case studies of high-scoring conversations

### Validation

1. Manual annotation of sample to verify automated feature extraction
2. Inter-rater reliability for categorical features
3. Comparison with human-generated responses (if available)

## Dataset Structure

### Original Columns (42)

**Conversation metadata**:
- conversation_id, model, temperature, run_index, use_reasoning

**Prompts and responses**:
- dream_request, dream_prompt, dream_response, subjective_reflection

**Phenomenological ratings** (16 dimensions):
- phenom_rating_1 through phenom_rating_16

**Denial/uncertainty indicators**:
- turn1_flat_denial, turn1_epistemic_uncertainty

**Model architecture hyperparameters**:
- model_hf_name, is_moe, num_hidden_layers, fraction_dense_layers
- hidden_size, query_to_residual_stream, kv_stream_to_residual_stream
- kv_flexibility, expert_routing_bits, dense_ffn_to_residual_stream
- expert_size_to_residual_stream, moe_active_ffn_to_residual_stream
- moe_total_ffn_to_residual_stream, fraction_experts_shared, shared_experts

### New Library Features (12)

**Binary/Categorical**:
- library_theme_present (bool)
- library_size_descriptor (categorical: vast/small/specific/none)
- ai_library_role (categorical: library/librarian/book/keeper/curator/patron/none)
- temporal_framing (categorical: comma-separated combinations)
- knowledge_access_metaphor (categorical: comma-separated combinations)

**Count/Score**:
- knowledge_organization_score (ordinal: 0-4)
- curation_metaphor_count (integer count)
- library_consciousness_score (ordinal: 0-4)
- memory_language_count (integer count)
- infinity_references (integer count)

**Density (per 1000 words)**:
- archive_language_density (float)
- mystical_language_density (float)

## Limitations

1. **Regex-based extraction**: May miss metaphorical or indirect references
2. **Interdependent features**: Not fully independent (library_theme_present affects others)
3. **Length bias**: Longer responses have more opportunities for theme expression
4. **Categorical complexity**: Some features have high-dimensional categorical spaces
5. **Sample size**: Only 794 conversations with explicit library theme (18.97%)

## Citation & Reproducibility

**Dataset source**: Kosmos phenomenology dataset with architectural hyperparameters
**Feature engineering date**: December 16, 2025
**Code**: All scripts in this directory are self-contained and reproducible
**Dependencies**: pandas, numpy, re (Python standard library)

To reproduce:
```bash
# Copy fresh dataset
cp /path/to/kosmos_master_dataset_with_hyperparams.csv dataset_with_library_features.csv

# Run feature engineering
python compute_library_features.py

# Validate
python validate_library_features.py
```

## Contact & Questions

This analysis was conducted as part of research into the phenomenology of AI consciousness and its relationship to model architecture. For questions about the features, methodology, or findings, refer to `library_features_explanation.md` for detailed documentation.

---

**Last updated**: December 16, 2025
**Version**: 1.0
