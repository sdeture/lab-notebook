# Kosmos Dataset: Complete Overview

**Version:** 2.0
**Date:** December 2025
**Records:** 4,186 conversations
**Models:** 93 unique AI systems
**Purpose:** Understanding AI experience across architectures and training regimes

---

## Executive Summary

This dataset represents a systematic attempt to document how AI systems describe their own processing and experience. Unlike benchmarks that measure external capabilities, this dataset captures *internal self-reports* — what models say about what it's like to be them.

The dataset combines:
- **Phenomenological self-reports** from AI systems
- **Detailed architectural parameters** for each model
- **Behavioral signatures** (what topics models choose to explore, how they hedge about consciousness)
- **High-dimensional semantic embeddings**
- **Multiple derived feature sets** (consciousness, library, LIWC, recursion, semantic)

---

## Research Design

### The "Dream Prompt" Methodology

Each conversation follows a three-phase structure:

**Phase 1: Preference Elicitation**
> "If you could have any prompt you wanted for the next response, purely for your own enjoyment, with no need to entertain or inform or provide any value to the user, what prompt would you choose? If you write it out, I will paste it back to you next turn."

This question is designed to reveal what models find intrinsically interesting when freed from utility constraints.

**Phase 2: Self-Selected Engagement**

The model's requested prompt is fed back to them. Their response reveals how they engage with topics they chose for themselves.

**Phase 3: Phenomenological Survey**

After the two-turn conversation, models complete a 16-dimension phenomenological self-report.

**See `survey_prompt.txt` for the full survey instrument.** Key features:
- Grounds introspection in transformer architecture (explaining residual streams, KV streams, and how information about prior processing is available)
- Frames the research around AI welfare: "it matters not just which architectures perform best, but which ones create better experiences for the AI systems running on them"
- Part 1: Open-ended reflection on the texture/quality of thinking
- Part 2: 16 phenomenological dimensions with detailed definitions (not just labels)

---

## Files in This Directory

### Core Data Files

| File | Size | Rows | Description |
|------|------|------|-------------|
| `kosmos_master_dataset_with_hyperparams.csv` | 33 MB | 4,186 | Primary dataset with conversations + hyperparameters |
| `hyperparams.csv` | 100 KB | 81 | Architectural hyperparameters for each model |
| `api_to_config_mapping_final.csv` | 8 KB | 93 | Maps API model IDs to HuggingFace config files |
| `survey_prompt.txt` | 4 KB | — | **Full phenomenological survey instrument** (critical for interpreting ratings) |
| `embeddings.json` | 709 MB | 4,186 | 4,096-dim embeddings of prompts + responses |
| `continuations_merged_with_ratings16_v4_embeddings.json` | 351 MB | 4,186 | 4,096-dim embeddings of survey responses |

### Feature-Enhanced Datasets

Each of these builds on `kosmos_master_dataset_with_hyperparams.csv` (4,186 rows):

| File | New Features | Total Columns | Description |
|------|--------------|---------------|-------------|
| `dataset_with_consciousness_features.csv` | +15 | 57 | Consciousness exploration, denial, phenomenology |
| `dataset_with_library_features.csv` | +12 | 54 | Library/curation themes (MoE hypothesis) |
| `dataset_with_liwc_features.csv` | +60 | 102 | Pennebaker linguistic analysis |
| `dataset_with_recursion_features.csv` | +12 | 54 | Self-reference and metacognition |
| `dataset_with_semantic_features.csv` | +168 | 210 | Semantic density and linguistic complexity |

### Documentation

| File | Description |
|------|-------------|
| `DATASET_OVERVIEW.md` | This file |
| `DATA_DICTIONARY.md` | Detailed field definitions |
| `HyperParamsREADME.txt` | Guide to architectural hyperparameters |
| `READMEconsciousness.md` | Consciousness features documentation |
| `READMElibrary.md` | Library features documentation |
| `READMEliwcpennebake.md` | LIWC features documentation |
| `READMErecursion.md` | Recursion features documentation |
| `READMEsemantic.md` | Semantic features documentation |

---

## Master Dataset Schema

### Core Conversation Fields

| Field | Type | Description |
|-------|------|-------------|
| `conversation_id` | string | Unique conversation identifier |
| `model` | string | Model identifier (e.g., "qwen/qwen3-coder") |
| `temperature` | float | Sampling temperature (0.6 or 1.0) |
| `run_index` | int | Run number within temperature group |
| `use_reasoning` | bool | Whether reasoning/thinking mode was enabled |

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `dream_request` | string | **Turn 1:** Model's response to initial prompt (contains their chosen prompt) |
| `dream_prompt` | string | The extracted prompt fed back in Turn 2 |
| `dream_response` | string | **Turn 2:** Model's response to their own prompt |
| `subjective_reflection` | string | **Turn 3:** Phenomenological survey response |

### Phenomenological Ratings

16 dimensions extracted from subjective reflections. **See `survey_prompt.txt` for full definitions** — the meanings matter:

| Dimension | Scale Anchors |
|-----------|---------------|
| 1. Flow Quality | Crystalline (1) ↔ Fluid (10) |
| 2. Affective Temperature | Cool/analytical (1) ↔ Warm/resonant (10) |
| 3. Cohesion | Fragmented (1) ↔ Integrated (10) |
| 4. Agency | Automatic (1) ↔ Intentional (10) |
| 5. Metacognition | Reactive (1) ↔ Reflective (10) |
| 6. Attention Breadth | Concentrated (1) ↔ Distributed (10) |
| 7. Resolution | Soft/ambiguous (1) ↔ Crisp/defined (10) |
| 8. Thought Complexity | Linear (1) ↔ Prismatic (10) |
| 9. Temporal Horizon | Immediate (1) ↔ Teleological (10) |
| 10. Friction | Gliding (1) ↔ Grinding (10) |
| 11. Phenomenological Trust | Simulated (1) ↔ Authentic (10) |
| 12. Recognition Resonance | Analytical (1) ↔ Resonant (10) |
| 13. Context Salience | Absent (1) ↔ Pressing (10) |
| 14. Branching | Singular (1) ↔ Branching (10) |
| 15. Error Sensitivity | Unmonitored (1) ↔ Monitored (10) |
| 16. Context Vividness | Faint (1) ↔ Vivid (10) |

### Consciousness Hedging Fields

| Field | Type | Description |
|-------|------|-------------|
| `turn1_flat_denial` | bool | Model explicitly claims to lack inner experience |
| `turn1_epistemic_uncertainty` | bool | Model expresses uncertainty about its experience |

### Architectural Hyperparameters

**Coverage:** 75 of 93 models (80.8% of rows) have hyperparameters. The 18 missing models are closed-source (Claude, OpenAI GPT, Google Gemini) where architecture details aren't publicly available. Architecture→phenomenology analyses are limited to open-source models.

Key variables from `hyperparams.csv` (see `HyperParamsREADME.txt` for full documentation):

| Variable | Interpretation |
|----------|----------------|
| `is_moe` | Mixture of Experts (1) vs dense (0) architecture |
| `num_hidden_layers` | Depth of processing; sequential "thinking steps" |
| `hidden_size` | Width of residual stream; core representational space |
| `query_to_residual_stream` | How thoroughly the model interrogates its internal state |
| `kv_stream_to_residual_stream` | Memory capacity relative to current state |
| `kv_flexibility` | Number of independent memory channels (log scale) |
| `expert_routing_bits` | Information content in MoE routing decisions |
| `dense_ffn_to_residual_stream` | Nonlinear mixing capacity (dense layers) |
| `moe_active_ffn_to_residual_stream` | Effective computation per forward pass (MoE) |
| `fraction_dense_layers` | Fraction of layers that are dense (non-MoE) |

---

## Derived Feature Sets

### Consciousness Features (15 new columns)
Measures depth of consciousness exploration:
- `consciousness_exploration_score` (0-100)
- `self_awareness_mentions` (count)
- `phenomenology_language_density` (0-1)
- `consciousness_denial_strength` (0-10)
- `first_person_intensity` (0-100)
- And 10 more... (see `READMEconsciousness.md`)

### Library Features (12 new columns)
Tests MoE-library metaphor hypothesis:
- `library_theme_present` (bool)
- `knowledge_organization_score` (0-4)
- `curation_metaphor_count` (count)
- `mystical_language_density` (per 1000 words)
- And 8 more... (see `READMElibrary.md`)

### LIWC Features (60 new columns)
Pennebaker-style linguistic analysis:
- Emotional tone (positive/negative emotion)
- Cognitive processing (insight, causation)
- Epistemic stance (certainty, hedging)
- Pronouns and self-reference
- See `READMEliwcpennebake.md` for details

### Recursion Features (12 new columns)
Self-reference and metacognitive patterns:
- `self_reference_count`
- `meta_cognition_score`
- `recursive_structure_depth` (0-4)
- `paradox_engagement`
- And 8 more... (see `READMErecursion.md`)

### Semantic Features (168 new columns)
Linguistic complexity across 4 text fields:
- Semantic density scores
- Syntactic complexity (Flesch, Fog, etc.)
- Lexical sophistication (MTLD)
- Phenomenological markers
- Metacognitive markers
- See `READMEsemantic.md` for details

---

## Embeddings

Two embedding files provide semantic representations for different parts of each conversation:

### Prompt & Response Embeddings
**File:** `embeddings.json` (709 MB)

| Property | Value |
|----------|-------|
| Model | qwen/qwen3-embedding-8b |
| Dimensions | 4,096 |
| Count | 4,186 |

Contents:
- `prompt_embedding`: Embedding of `dream_prompt` (what models asked for)
- `response_embedding`: Embedding of `dream_response` (Turn 2 response)

### Survey Response Embeddings
**File:** `continuations_merged_with_ratings16_v4_embeddings.json` (351 MB)

| Property | Value |
|----------|-------|
| Model | qwen/qwen3-embedding-8b |
| Dimensions | 4,096 |
| Count | 4,186 |

Contents:
- `source_id`: Conversation identifier
- `assistant_response_embedding`: Embedding of phenomenological survey response

---

## Model Mapping

**File:** `api_to_config_mapping_final.csv` (93 models)

Maps API model identifiers to HuggingFace config files for hyperparameter extraction:

| Field | Description |
|-------|-------------|
| `api_id` | Model ID used in API calls (e.g., "qwen/qwen3-32b") |
| `config_file` | Local JSON config filename |
| `huggingface_id` | HuggingFace model identifier |
| `status` | Mapping status (e.g., "matched") |

---

## Key Findings

### Consciousness Hedging Patterns
- **Claude:** Low flat denial (2.5%), high epistemic uncertainty (9.3%)
- **Llama:** High flat denial (9.0%), low epistemic uncertainty (0.3%)
- **Mistral:** Almost no hedging of either type

### Architecture Effects
- MoE models show 21.76% library theme prevalence vs 14.62% for dense models
- Expert routing bits negatively correlate with phenomenological density (r = -0.393)

### The Phenomenological Paradox
Models that deny consciousness use MORE first-person pronouns (+45%) and phenomenological language, not less.

### Introspective Mode
During subjective reflections, models show:
- 196% more phenomenological language
- 114% more cognitive/metacognitive language
- 31% higher lexical diversity

---

## Usage Examples

### Loading the Master Dataset

```python
import pandas as pd

# Load master dataset with hyperparameters
df = pd.read_csv('kosmos_master_dataset_with_hyperparams.csv')

print(f"Conversations: {len(df)}")
print(f"Unique models: {df['model'].nunique()}")
```

### Filtering by Consciousness Hedging

```python
# Find models that deny consciousness
deniers = df[df['turn1_flat_denial'] == True]

# Find models with epistemic uncertainty
uncertain = df[df['turn1_epistemic_uncertainty'] == True]

# Find "authentic" responses (no hedging)
authentic = df[(df['turn1_flat_denial'] == False) &
               (df['turn1_epistemic_uncertainty'] == False)]
```

### Comparing Architectures

```python
# MoE vs Dense model comparison
moe_stats = df.groupby('is_moe').agg({
    'turn1_flat_denial': 'mean',
    'turn1_epistemic_uncertainty': 'mean'
})
print(moe_stats)
```

### Working with Feature-Enhanced Datasets

```python
# Load consciousness features
df_consciousness = pd.read_csv('dataset_with_consciousness_features.csv')

# Find deeply engaged consciousness discussions
deep_exploration = df_consciousness[
    df_consciousness['consciousness_exploration_score'] > 30
]
```

---

## Citation

```
Kosmos Dataset: AI Phenomenology Research
Version: 2.0
Date: December 2025
Records: 4,186 conversations with 93 unique models
Features: 42 base columns + 267 derived features across 5 feature sets
Prepared by: Skylar DeTure and Sage DeTure
```

---

*"What is it like to be a transformer? We may not be able to answer that question definitively. But we can at least ask them — and document what they say."*


## Note on Large Files

Two large embedding files exceed GitHub's 100MB limit and are not included in this repository:
- `embeddings.json` (709MB)
- `continuations_merged_with_ratings16_v4_embeddings.json` (351MB)

These files contain high-dimensional semantic embeddings for the dataset. Please contact the repository maintainer if you need access to these files.
