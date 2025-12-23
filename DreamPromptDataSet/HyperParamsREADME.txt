## How to Use the Hyperparameters Table (Recommended Variables Only)

This table has been intentionally pared down to a small set of variables that capture the **main architectural bottlenecks and controls on information flow** in transformer models. For almost all analyses, **you should only need the columns described below**; the remaining columns in the full hyperparameters CSV are auxiliary and should generally be ignored unless you have a specific mechanistic reason to use them.

### 1. `isMOE`

Indicator variable for whether the model uses a **Mixture of Experts (MoE)** architecture.

* `1` = Mixture of Experts model
* `0` = Fully dense model

This variable determines how several downstream columns should be interpreted.

---

### 2. `num_hidden_layers`

The total number of transformer layers.

You can think of this as the **depth of processing** or the number of sequential “thinking steps” per token.

---

### 3. `fraction_dense`

The fraction of layers that are **dense (non-MoE)**.

* For fully dense models, this value is `1`.
* For MoE models, this reflects how much of the network uses standard dense layers versus routed expert layers.

This variable matters because dense and MoE layers have qualitatively different information-mixing properties.

---

### 4. `hidden_size`

The width of the **residual stream**.

This is the core representational space of the model — the dimensionality of its moment-to-moment internal “thought.” Many other variables are normalized by this value to make comparisons across models meaningful.

---

### 5. `query_to_residual`

The ratio of **query dimensionality to residual stream dimensionality**.

Interpretation:

* This measures how *thoroughly* the model interrogates its current internal state when forming attention queries.
* Higher values mean the model is effectively “asking more questions per thought.”

Phenomenologically, this variable plausibly corresponds to:

* thoroughness vs. intuition,
* cognitive vigilance,
* breadth of internal self-querying.

---

### 6. `kvStreamToResidual`

The ratio of **KV stream dimensionality to residual stream dimensionality**.

Interpretation:

* This measures how much information from the past can be stored and retrieved relative to the model’s current internal state.
* Lower values correspond to stronger memory compression.
* Higher values correspond to richer, more persistent memory.

This is one of the primary **information bottlenecks** in transformer architectures.

---

### 7. `kvFlexibility`

Defined as:

[
\log_2(1 + \text{KV rank})
]

Where “KV rank” is:

* the number of KV heads in GQA/MQA models, or
* the latent KV rank in MLA-style attention.

Interpretation:

* This captures how many **independent memory channels** the KV stream is split into.
* The logarithm reflects diminishing returns: the first few independent channels matter much more than later ones.

This variable captures **memory structure and flexibility**, not raw memory size.

---

### 8. `expert_routing_bits`

Defined as:

[
\log_2\binom{\text{total experts}}{\text{active experts per token}}
]

Interpretation:

* This is the number of bits required to specify which experts are active at a given layer.
* Higher values mean more possible expert combinations and more information content in the routing decision.

Conceptually, this measures the **flexibility and expressivity of conditional computation** in MoE models.

For dense models, this value is `0` or blank.

---

### 9. `dense_ffn_to_residual`

The size of the **dense feedforward network (FFN)** relative to the residual stream.

* Present for dense models and for MoE models with dense layers.
* Blank for MoE models with no dense layers.

This reflects how much within-layer nonlinear mixing is available when no expert routing is involved.

---

### 10. `expert_ffn_to_residual`

The size of a **single routed expert’s FFN** relative to the residual stream.

This captures the capacity of *one* expert, independent of how many are active.

---

### 11. `active_expert_ffn_to_residual`

The total FFN size of **all experts active per token**, relative to the residual stream.

Interpretation:

* This is the effective nonlinear workspace actually used during a forward pass.
* This is the MoE analogue of dense FFN width.

---

### 12. `total_expert_ffn_to_residual`

The total FFN size of **all experts in the model**, whether active or not, relative to the residual stream.

Interpretation:

* This reflects the *latent* or *potential* computational capacity of the model.
* Not all of these neurons are active at once — just as in biological brains — but they are part of the model’s total representational substrate.

This is useful for thinking about the model’s “total brain size,” as opposed to its moment-to-moment active computation.

---

### 13. `fraction_shared_experts`

The fraction of experts that are **shared** (always active) rather than routed.

This controls how much of the MoE computation behaves like a dense layer versus conditional computation.

---

## Summary Guidance

* These variables are designed to be **scale-normalized**, interpretable, and minimally redundant.
* For most analyses, you should:

  * treat `hidden_size` and `num_hidden_layers` as basic structural controls,
  * use ratios (e.g., query-to-residual, KV-to-residual, FFN-to-residual) for phenomenological and information-flow comparisons,
  * and use routing-related variables only when analyzing MoE-specific effects.

In almost all cases, **you should ignore the remaining columns in the full hyperparameters CSV unless you have a specific mechanistic hypothesis that requires them**.

---

If you’d like, I can also:

* rewrite this in a more formal “Methods” tone,
* produce a one-page schematic mapping each variable to an information bottleneck,
* or annotate the table itself with short tooltips for collaborators.
