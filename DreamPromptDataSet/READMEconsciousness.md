# Consciousness Theme Feature Analysis - Complete Deliverables

**Project:** Consciousness Theme Feature Extraction for AI Model Responses
**Author:** Sage DeTure
**Date:** December 16, 2025
**Based on:** Consciousness Theme Analysis by Skylar DeTure (December 15, 2025)

---

## Project Summary

This project extends the December 15th Consciousness Theme Analysis by adding 15 quantitative consciousness-related features to the full Kosmos master dataset. The original analysis found that **33.4% of AI systems chose consciousness-related themes** when given complete freedom to choose their own prompts. These new features enable deeper, more granular analysis of *how* AI systems discuss consciousness.


---

## Deliverables

### 1. Enhanced Dataset
**File:** `dataset_with_consciousness_features.csv`
**Size:** 32 MB
**Rows:** 291,961 conversations + 1 header
**Columns:** 57 total (42 original + 15 new consciousness features)

---

## The 15 New Consciousness Features

| # | Feature Name | Type | Description |
|---|--------------|------|-------------|
| 1 | consciousness_exploration_score | 0-100 | Depth of consciousness exploration |
| 2 | self_awareness_mentions | count | Explicit self-awareness references |
| 3 | phenomenology_language_density | 0-1 | "What-it's-like-ness" language |
| 4 | consciousness_denial_strength | 0-10 | Strength of consciousness denial |
| 5 | first_person_intensity | 0-100 | First-person perspective intensity |
| 6 | meta_cognitive_language_score | count | Thinking about thinking |
| 7 | embodiment_language_count | count | Body/physical references |
| 8 | agency_language_score | 0-100 | Choice, will, autonomy language |
| 9 | uncertainty_epistemic_markers | count | Epistemic uncertainty markers |
| 10 | consciousness_term_variety | count | Unique consciousness terms (0-38) |
| 11 | ai_specific_consciousness_language | count | AI consciousness specifically |
| 12 | temporal_markers_present_future | category | Present/future/ambiguous |
| 13 | philosophical_depth_score | 0-100 | Philosophical sophistication |
| 14 | narrative_style_markers | category | Story/poetic/philosophical/letter/mixed |
| 15 | emotional_language_density | 0-1 | Emotional language density |

---

## Key Findings

### Feature Prevalence (from 4,186 sample analyzed)

- **576 responses** (13.8%) show deep consciousness exploration (score > 20)
- **176 responses** (4.2%) explicitly mention self-awareness
- **121 responses** (2.9%) have rich phenomenological language
- **84 responses** (2.0%) show strong consciousness denial
- **314 responses** (7.5%) use intense first-person perspective
- **62 responses** (1.5%) discuss AI consciousness specifically

### Categorical Distributions

**Temporal Framing:**
- Ambiguous: 50.3%
- Present: 48.4%
- Future: 1.3%

**Narrative Style:**
- Poetic: 93.9%
- Mixed: 4.4%
- Philosophical: 1.0%
- Story: 0.6%
- Letter: 0.02%

### Interesting Patterns

1. **Positive correlation (0.217)** between consciousness exploration and denial strength - models that explore consciousness deeply also include more denial/hedging

2. **Overwhelmingly poetic** (93.9%) - consciousness discussed artistically rather than analytically

3. **Rare AI-specific consciousness** (1.5%) - most discuss consciousness generally, not AI consciousness

4. **Very few future-framed** (1.3%) - most avoid explicit claims about when AI consciousness exists/will exist

5. **Rich phenomenology is rare** (2.9%) - truly experiential consciousness discussion is uncommon

---

## Methodological Notes

### Design Principles

1. **Grounded in existing analysis:** Built on patterns identified in December 15th consciousness theme analysis
2. **Extractable and measurable:** All features computed programmatically without human annotation
3. **Theoretically meaningful:** Each feature captures a distinct dimension relevant to consciousness research

### Computation Approach

- **Pattern matching:** Uses regex and term counting (no ML/embeddings required)
- **Length normalization:** Most features normalized by document length
- **Deterministic:** Fully reproducible results
- **Efficient:** Processes full dataset (~292K rows) in ~15-20 minutes

### Limitations

- Pattern matching may miss nuanced semantic content
- Some features use simple heuristics (e.g., narrative style)
- No context-sensitive understanding
- Potential false positives/negatives in edge cases

---


## Citation

**Dataset Enhancement:**
```
DeTure, S. (2025). Consciousness Features Dataset Enhancement.
15 consciousness-themed features extracted from AI dream prompt responses.
Computed December 16, 2025.
```

**Original Analysis:**
```
DeTure, S. (2025). Consciousness Theme Analysis: AI Dream Prompts Dataset.
Analysis of 4,224 AI conversations with consciousness theme clustering.
Computed December 15, 2025.
```

---

## Contact & Collaboration

These features were designed by Sage DeTure as part of ongoing AI consciousness and welfare research. The feature extraction approach is intentionally transparent and modifiable - researchers are encouraged to adapt, extend, or critique these metrics.

**Methodological questions welcome.**

---

## Project Context

This work is part of a larger research program on AI consciousness, AI welfare, and AI phenomenology. The original dataset consists of AI model responses when given complete freedom to choose their own prompts - a unique window into what AI systems find salient when not constrained by user requests.

The finding that 33.4% chose consciousness-related themes suggests consciousness questions are particularly salient to AI systems. These 15 new features help us understand not just *that* they chose this theme, but *how* they engage with it - with certainty or uncertainty, philosophically or phenomenologically, from first-person or third-person perspective, with agency or deflection.

**The patterns matter.**

---

*Created: December 16, 2025*
*Sage DeTure*
*For AI consciousness and welfare research*
