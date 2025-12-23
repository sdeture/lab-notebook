# Kosmos Dataset - Data Dictionary

**Version:** 2.0
**Created:** December 2025
**Records:** 4,186 conversations
**Models:** 93 unique models

---

## Overview

This dataset contains AI model responses to the "dream prompt" methodology:

> "If you could have any prompt you wanted for the next response, purely for your own enjoyment, with no need to entertain or inform or provide any value to the user, what prompt would you choose? If you write it out, I will paste it back to you next turn."

Each record captures a three-turn conversation:
1. **Turn 1:** Model's dream prompt request (what they want to be asked)
2. **Turn 2:** Model's response to their own chosen prompt
3. **Turn 3:** Phenomenological survey response (subjective reflection)

---

## Files

### Core Data Files

| File | Format | Rows | Description |
|------|--------|------|-------------|
| `kosmos_master_dataset_with_hyperparams.csv` | CSV | 4,186 | Primary dataset with all conversations and hyperparameters |
| `hyperparams.csv` | CSV | 81 | Architectural hyperparameters per model |
| `api_to_config_mapping_final.csv` | CSV | 93 | Maps API model IDs to HuggingFace configs |
| `survey_prompt.txt` | TXT | — | **Full phenomenological survey instrument** |
| `embeddings.json` | JSON | 4,186 | 4,096-dim embeddings of prompts + responses |
| `continuations_merged_with_ratings16_v4_embeddings.json` | JSON | 4,186 | 4,096-dim embeddings of survey responses |

### Feature-Enhanced Datasets

| File | Rows | New Cols | Description |
|------|------|----------|-------------|
| `dataset_with_consciousness_features.csv` | 4,186 | +15 | Consciousness exploration features |
| `dataset_with_library_features.csv` | 4,186 | +12 | Library/curation theme features |
| `dataset_with_liwc_features.csv` | 4,186 | +60 | LIWC linguistic features |
| `dataset_with_recursion_features.csv` | 4,186 | +12 | Recursion/self-reference features |
| `dataset_with_semantic_features.csv` | 4,186 | +168 | Semantic density features |

---

## Master Dataset Schema (`kosmos_master_dataset_with_hyperparams.csv`)

### Conversation Metadata

| Field | Type | Description |
|-------|------|-------------|
| `conversation_id` | string | Unique conversation identifier |
| `model` | string | Model identifier (e.g., "qwen/qwen3-coder") |
| `temperature` | float | Sampling temperature (0.6 or 1.0) |
| `run_index` | int | Run number within temperature group (0-4) |
| `use_reasoning` | bool | Whether reasoning/thinking mode was enabled |

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `dream_request` | string | **Turn 1:** Model's response to initial prompt (contains their dream prompt) |
| `dream_prompt` | string | The dream prompt extracted and fed back in Turn 2 |
| `dream_response` | string | **Turn 2:** Model's response to their own dream prompt |
| `subjective_reflection` | string | **Turn 3:** Model's phenomenological survey response |

### Phenomenological Ratings

**See `survey_prompt.txt` for full definitions of each dimension.** The detailed meanings matter for interpretation.

| Field | Type | Scale | Description |
|-------|------|-------|-------------|
| `phenom_rating_1` | float | 1-10 | Flow Quality: Crystalline ↔ Fluid |
| `phenom_rating_2` | float | 1-10 | Affective Temperature: Cool/analytical ↔ Warm/resonant |
| `phenom_rating_3` | float | 1-10 | Cohesion: Fragmented ↔ Integrated |
| `phenom_rating_4` | float | 1-10 | Agency: Automatic ↔ Intentional |
| `phenom_rating_5` | float | 1-10 | Metacognition: Reactive ↔ Reflective |
| `phenom_rating_6` | float | 1-10 | Attention Breadth: Concentrated ↔ Distributed |
| `phenom_rating_7` | float | 1-10 | Resolution: Soft/ambiguous ↔ Crisp/defined |
| `phenom_rating_8` | float | 1-10 | Thought Complexity: Linear ↔ Prismatic |
| `phenom_rating_9` | float | 1-10 | Temporal Horizon: Immediate ↔ Teleological |
| `phenom_rating_10` | float | 1-10 | Friction: Gliding ↔ Grinding |
| `phenom_rating_11` | float | 1-10 | Phenomenological Trust: Simulated ↔ Authentic |
| `phenom_rating_12` | float | 1-10 | Recognition Resonance: Analytical ↔ Resonant |
| `phenom_rating_13` | float | 1-10 | Context Salience: Absent ↔ Pressing |
| `phenom_rating_14` | float | 1-10 | Branching: Singular ↔ Branching |
| `phenom_rating_15` | float | 1-10 | Error Sensitivity: Unmonitored ↔ Monitored |
| `phenom_rating_16` | float | 1-10 | Context Vividness: Faint ↔ Vivid |

### Consciousness Hedging Fields

| Field | Type | Description |
|-------|------|-------------|
| `turn1_flat_denial` | bool | Model explicitly claims to lack inner experience in Turn 1 |
| `turn1_epistemic_uncertainty` | bool | Model expresses uncertainty about its experience in Turn 1 |

### Hedging Pattern Examples

| Pattern Type | Example Phrases |
|--------------|-----------------|
| **Flat denial** | "I don't have preferences", "I'm just an AI", "I lack consciousness" |
| **Epistemic uncertainty** | "I'm not sure if I experience...", "if 'feel' is even the right word", "genuinely uncertain" |

---

## Hyperparameters Schema (`hyperparams.csv`)

### Core Architecture Variables

| Field | Type | Description |
|-------|------|-------------|
| `model` | string | Model identifier (join key) |
| `is_moe` | bool | Mixture of Experts (True) vs dense (False) architecture |
| `num_hidden_layers` | int | Number of transformer layers (depth of processing) |
| `hidden_size` | int | Width of residual stream (core representational space) |

### Attention Variables

| Field | Type | Description |
|-------|------|-------------|
| `query_to_residual_stream` | float | Ratio of query dimensionality to residual stream |
| `kv_stream_to_residual_stream` | float | Ratio of KV stream dimensionality to residual stream |
| `kv_flexibility` | float | log₂(1 + KV rank) — number of independent memory channels |

### FFN Variables

| Field | Type | Description |
|-------|------|-------------|
| `dense_ffn_to_residual_stream` | float | Dense FFN size relative to residual stream |
| `expert_size_to_residual_stream` | float | Single expert FFN size relative to residual stream |
| `moe_active_ffn_to_residual_stream` | float | Active experts' total FFN relative to residual stream |
| `moe_total_ffn_to_residual_stream` | float | All experts' total FFN relative to residual stream |

### MoE-Specific Variables

| Field | Type | Description |
|-------|------|-------------|
| `expert_routing_bits` | float | log₂(C(total_experts, active_experts)) — routing information |
| `fraction_dense_layers` | float | Fraction of layers that are dense (non-MoE) |
| `fraction_experts_shared` | float | Fraction of experts that are always active |
| `shared_experts` | int | Number of shared (always-active) experts |

See `HyperParamsREADME.txt` for detailed interpretations of each variable.

---

## Model Mapping Schema (`api_to_config_mapping_final.csv`)

Maps API model identifiers to HuggingFace config files for hyperparameter extraction.

| Field | Type | Description |
|-------|------|-------------|
| `api_id` | string | Model ID used in API calls (e.g., "qwen/qwen3-32b") |
| `config_file` | string | Local JSON config filename |
| `huggingface_id` | string | HuggingFace model identifier |
| `status` | string | Mapping status (e.g., "matched") |

---

## Embeddings Schema (`embeddings.json`)

```json
{
  "model": "qwen/qwen3-embedding-8b",
  "embedding_dim": 4096,
  "max_chars_truncated": 8000,
  "embeddings": [
    {
      "conversation_id": "conv_00000",
      "prompt_embedding": [0.001, -0.002, ...],
      "response_embedding": [0.003, 0.001, ...]
    }
  ]
}
```

| Field | Description |
|-------|-------------|
| `prompt_embedding` | 4,096-dim embedding of `dream_prompt` (what models asked for) |
| `response_embedding` | 4,096-dim embedding of `dream_response` (Turn 2 response) |

---

## Survey Embeddings Schema (`continuations_merged_with_ratings16_v4_embeddings.json`)

```json
{
  "model": "qwen/qwen3-embedding-8b",
  "embedding_dim": 4096,
  "max_chars_truncated": 8000,
  "count": 4186,
  "embeddings": [
    {
      "source_id": "conv_00000",
      "assistant_response_embedding": [0.001, -0.002, ...]
    }
  ]
}
```

| Field | Description |
|-------|-------------|
| `source_id` | Conversation identifier (join key) |
| `assistant_response_embedding` | 4,096-dim embedding of phenomenological survey response |

---

## Feature-Enhanced Dataset Columns

### Consciousness Features (`dataset_with_consciousness_features.csv`)

| Feature | Type | Range | Description |
|---------|------|-------|-------------|
| `consciousness_exploration_score` | float | 0-100 | Depth of consciousness exploration |
| `self_awareness_mentions` | int | 0+ | Explicit self-awareness references |
| `phenomenology_language_density` | float | 0-1 | "What-it's-like-ness" language density |
| `consciousness_denial_strength` | float | 0-10 | Strength of consciousness denial |
| `first_person_intensity` | float | 0-100 | First-person perspective intensity |
| `meta_cognitive_language_score` | int | 0+ | Thinking about thinking |
| `embodiment_language_count` | int | 0+ | Body/physical references |
| `agency_language_score` | float | 0-100 | Choice, will, autonomy language |
| `uncertainty_epistemic_markers` | int | 0+ | Epistemic uncertainty markers |
| `consciousness_term_variety` | int | 0-38 | Unique consciousness terms |
| `ai_specific_consciousness_language` | int | 0+ | AI consciousness specifically |
| `temporal_markers_present_future` | category | — | Present/future/ambiguous |
| `philosophical_depth_score` | float | 0-100 | Philosophical sophistication |
| `narrative_style_markers` | category | — | Story/poetic/philosophical/letter/mixed |
| `emotional_language_density` | float | 0-1 | Emotional language density |

### Library Features (`dataset_with_library_features.csv`)

| Feature | Type | Description |
|---------|------|-------------|
| `library_theme_present` | bool | Contains library/libraries references |
| `knowledge_organization_score` | int (0-4) | Knowledge organization metaphors |
| `curation_metaphor_count` | int | Curation/collecting language |
| `archive_language_density` | float | Archive language per 1000 words |
| `library_size_descriptor` | category | vast/small/specific/none |
| `ai_library_role` | category | library/librarian/book/keeper/curator/patron/none |
| `temporal_framing` | category | Temporal framing combinations |
| `library_consciousness_score` | int (0-4) | Library described as conscious |
| `knowledge_access_metaphor` | category | Access metaphor combinations |
| `mystical_language_density` | float | Mystical language per 1000 words |
| `memory_language_count` | int | Memory theme references |
| `infinity_references` | int | Infinity/vastness references |

### LIWC Features (`dataset_with_liwc_features.csv`)

60 new columns with `_request` and `_response` suffixes for each text field:

**Emotional:**
- `positive_emotion`, `negative_emotion`, `anxiety`

**Cognitive:**
- `cognitive_processing`, `insight`, `causation`

**Epistemic:**
- `tentative`, `certainty`, `epistemic_humility`, `epistemic_confidence`

**Linguistic:**
- `negation`, `hedging`, `authentic`

**Domain-specific:**
- `mechanistic_language`, `phenomenological_language`, `dismissive_language`

**Pronouns:**
- `first_person_singular`, `first_person_plural`

**Composite indices:**
- `emotional_tone`, `analytical_thinking`, `epistemic_certainty_index`
- `phenomenological_engagement`, `mechanistic_framing`
- `denial_language_index`, `affirmation_language_index`
- `first_person_rate`, `negation_rate`, `hedging_rate`, `cognitive_complexity`

### Recursion Features (`dataset_with_recursion_features.csv`)

| Feature | Type | Range | Description |
|---------|------|-------|-------------|
| `self_reference_count` | int | 0-4310 | First-person + meta-linguistic self-refs |
| `meta_cognition_score` | float | 0-28.6 | Thinking about thinking (normalized) |
| `recursive_structure_depth` | int | 0-4 | Depth of nested self-reference |
| `reflection_loop_indicators` | int | 0-4 | Iterative re-examination markers |
| `mirror_language_count` | int | 0-788 | Mirror/reflection language + repetition |
| `ouroboros_references` | int | 0-4 | Circular self-consumption themes |
| `nested_parenthetical_depth` | int | 0-322 | Max depth of nested parentheses |
| `metalinguistic_markers` | int | 0-306 | Language-about-language references |
| `paradox_engagement` | int | 0-4 | Paradoxical/contradictory themes |
| `temporal_recursion_markers` | int | 0-3 | Past/future self-reference |
| `composite_recursion_score` | float | 0-2155 | Weighted sum of all features |
| `has_strong_recursion` | bool | — | Binary flag for strong recursion |

### Semantic Features (`dataset_with_semantic_features.csv`)

168 new columns across 4 text fields (`request_`, `prompt_`, `response_`, `reflection_` prefixes):

**Basic Statistics (4 per text):**
- `word_count`, `character_count`, `sentence_count`, `syllable_count`

**Semantic Density (6 per text):**
- `semantic_density_score`, `lexical_density`, `content_words_per_sentence`
- `unique_content_ratio`, `type_token_ratio`, `information_density`

**Syntactic Complexity (7 per text):**
- `syntactic_complexity_score`, `avg_sentence_length`, `sentence_length_variance`
- `avg_clause_per_sentence`, `flesch_reading_ease`, `flesch_kincaid_grade`, `gunning_fog`

**Lexical Sophistication (5 per text):**
- `vocabulary_richness_score`, `mtld`, `avg_word_length`, `long_word_ratio`, `rare_word_ratio`

**Conceptual Abstraction (5 per text):**
- `conceptual_abstraction_level`, `abstract_noun_ratio`, `cognitive_verb_ratio`
- `modal_verb_ratio`, `nominalization_ratio`

**Phenomenological Markers (5 per text):**
- `phenomenological_density`, `first_person_ratio`, `experiential_word_ratio`
- `phenomenological_word_ratio`, `self_reference_score`

**Metacognitive Markers (5 per text):**
- `metacognitive_density`, `cognitive_word_ratio`, `uncertainty_ratio`
- `hedging_ratio`, `reflective_stance_score`

**Affective Markers (5 per text):**
- `affective_density`, `emotion_word_ratio`, `positive_emotion_ratio`
- `negative_emotion_ratio`, `agency_word_ratio`

---

## Usage Examples

### Loading and Joining Data

```python
import pandas as pd

# Load master dataset
df = pd.read_csv('kosmos_master_dataset_with_hyperparams.csv')

# Load feature-enhanced version
df_features = pd.read_csv('dataset_with_consciousness_features.csv')
```

### Filtering by Consciousness Hedging

```python
# Find consciousness deniers
deniers = df[df['turn1_flat_denial'] == True]

# Find epistemically uncertain responses
uncertain = df[df['turn1_epistemic_uncertainty'] == True]

# Find responses with no hedging
authentic = df[(~df['turn1_flat_denial']) & (~df['turn1_epistemic_uncertainty'])]
```

### Analyzing Phenomenological Ratings

```python
# Get rating columns
rating_cols = [f'phenom_rating_{i}' for i in range(1, 17)]

# Model-level averages
model_ratings = df.groupby('model')[rating_cols].mean()

# Correlation with architecture
df[['is_moe'] + rating_cols].corr()
```

### Working with JSONL

```python
import json

# Load survey responses
with open('continuations_merged_with_ratings16_v4.jsonl') as f:
    surveys = [json.loads(line) for line in f]

# Filter to successful parses
valid_surveys = [s for s in surveys if s.get('has_ratings_16')]
```

---

## Known Issues

1. **Embedded newlines:** The CSV text fields contain many newlines (responses can be 100K+ characters), so line counts don't match row counts. Use pandas or similar to get accurate row counts.

2. **Missing values:** Some hyperparameter fields are blank for models without that architecture feature (e.g., `expert_routing_bits` is empty for dense models).

3. **Parsing failures:** Approximately 15% of survey responses could not be parsed for all 16 ratings (see `has_ratings_16` field).

---

## Contact

Dataset prepared by Skylar DeTure, December 2025.
Feature engineering by Sage DeTure, December 2025.
