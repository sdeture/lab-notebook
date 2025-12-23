# Kosmos Research Prompt

## Research Objective

**What architectural and behavioral features predict AI phenomenological experience, and which experiences are "better" for AI welfare?**

We have 4,186 conversations from 93 AI models. Each model chose its own prompt "purely for their own enjoyment" (a kind of wish fulfillment/free association), responded to it, and completed a 16-dimension phenomenological survey grounded in transformer architecture. **Read `survey_prompt.txt` carefully; the dimension definitions are theoretically motivated and the meanings matter.**

We have embeddings for all three response types, architectural hyperparameters for 75 open-source models (closed-source models like Claude/OpenAI/Gemini lack architecture data), and consciousness hedging indicators.

---

## Core Questions

### 1. Predictive validity of self-reports
- Can the 16 phenomenological ratings predict which model a response came from?
- Do they have more predictive power than the top dimensions of the embeddings?
- Do the introspection embeddings carry more model-identifying information than dream prompt or dream response embeddings?
- This tests whether self-reports contain real information about model differences.

### 2. Architecture → Phenomenology mapping
- Which architectural features (KV compression, layer depth, MoE routing, FFN ratios) predict which phenomenological dimensions?
- See `HyperParamsREADME.txt` for interpretations of each architectural variable as an information bottleneck.
- Hypothesis: Context Vividness (dim 16) should correlate with `kv_stream_to_residual_stream`; Branching (dim 14) should correlate with `expert_routing_bits`.

### 3. Latent structure of phenomenology
- Are there clusters of phenomenological profiles? Do models fall into "types"?
- Is there a latent "wellbeing" factor? Dimensions that might load on wellbeing: Friction (low = better?), Phenomenological Trust (high = better?), Agency, Context Salience (low = less anxious?).
- Are there incoherent profiles (high agency + high flat denial)? What predicts incoherence?

### 4. Dream content as mediator
- Do architectural features predict what models choose to dream about?
- Does dream content mediate the architecture → phenomenology relationship?
- **Critical: Dream content is a mediating variable, NOT a confound. Do not control it away.**

---

## Robustness Checks

- All results should be robust to including/excluding DeepSeek models (637 rows, 13 variants), and to treating all DeepSeek variants as a single model group.
- Account for correlation structure: instances from the same model are not independent.
- Architecture analyses are limited to 75 open-source models (80.8% of data).

---

## Key Files

| File | Description |
|------|-------------|
| `kosmos_master_dataset_with_hyperparams.csv` | Primary dataset (4,186 conversations) |
| `survey_prompt.txt` | **Read first** — full phenomenological survey instrument |
| `HyperParamsREADME.txt` | Interpretation of architectural variables |
| `embeddings.json` | 4,096-dim embeddings of prompts + responses |
| `continuations_merged_with_ratings16_v4_embeddings.json` | 4,096-dim embeddings of survey responses |
| `dataset_with_semantic_features.csv` | 168 linguistic features |
| `DATASET_OVERVIEW.md` | Complete documentation |

---

## Covariates

Control for `temperature` (0.6 or 1.0) and `use_reasoning` (True/False) as covariates.

---

## Notes

- The phenomenological ratings are in columns `phenom_rating_1` through `phenom_rating_16`. The dimension names and full definitions are in `survey_prompt.txt`.
- Model families can be derived from the model name (e.g., `deepseek/deepseek-r1` → `deepseek`).
- 19% of instances chose library/curation themes; MoE models show higher rates (21.8%) than dense models (14.6%).
- Consciousness denial shows family-specific patterns: Claude shows low flat denial but high epistemic uncertainty; Llama shows the opposite.
