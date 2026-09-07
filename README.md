# An ISO-Grounded Framework for Evaluating Data-Quality Robustness in Arabic NLP

This repository contains the code, perturbation scripts, experimental configurations, and output files associated with the study:

**An ISO-Grounded Framework for Evaluating Data-Quality Robustness in Arabic NLP**

## Study Overview

The study evaluates the robustness of Arabic NLP models to controlled test-time degradation in five data-quality dimensions:

- **Textual Accuracy** — character-level typographical corruption
- **Instance-Level Completeness** — random word removal
- **Representation Consistency** — controlled Arabic orthographic substitutions
- **Input Validity** — insertion of artificial out-of-policy tokens
- **Textual Understandability** — partial word-order disruption

Each dimension is evaluated independently at target severity levels of **10%, 20%, and 30%**.

The experiments cover:

- **Sentiment Analysis**
- **Sarcasm Detection**
- **Arabic Dialect Identification**

using multiple Arabic-specific and multilingual pretrained transformer models.

## Experimental Protocol

Models are fine-tuned once on clean training data and then kept fixed during robustness evaluation.

The evaluation pipeline is:

```text
raw test text
→ controlled perturbation
→ model-specific preprocessing
→ tokenization
→ fixed fine-tuned model
→ evaluation
```

Five perturbation seeds are used:

```text
42, 43, 44, 45, 46
```

The same raw perturbation realization is reused across models evaluated on the same dataset.

Gold labels are unchanged throughout the perturbation experiments.

## Evaluation

The primary metric is **Macro-F1**. Accuracy is reported as a complementary metric.

Performance degradation is defined as:

```text
ΔF1 = F1_clean - F1_perturbed
```

Results are reported as **mean ± standard deviation** across the five perturbation realizations. The reported standard deviation reflects perturbation variability, not repeated model training.

Realized perturbation severity is also recorded for each condition.

## Repository Contents

The repository provides:

- experiment scripts,
- perturbation implementations,
- model and dataset configurations,
- clean evaluation results,
- per-seed perturbed results,
- aggregated Macro-F1, accuracy, and ΔF1 outputs,
- realized-severity results,
- task-level and cross-task summaries.

Dataset files are not redistributed where restricted by the original dataset license or terms of use.

## Main Reproducibility Notes

- Training seed: `42`
- Perturbation seeds: `42–46`
- Maximum sequence length: `128`
- Optimizer: AdamW
- Learning rate: `2e-5`
- Training batch size: `16`
- Evaluation batch size: `32`
- Weight decay: `0.01`
- Maximum epochs: `3`

Official train/test splits are retained where available; otherwise, a stratified 80/20 split with seed 42 is used.

## Reproducing the Experiments

1. Install the required dependencies.
2. Obtain the datasets from their original sources.
3. Configure dataset paths.
4. Fine-tune the selected model on clean training data.
5. Evaluate the clean test set.
6. Generate perturbations for each quality dimension, severity, and seed.
7. Evaluate the same fixed model on each perturbed test set.
8. Aggregate results across the five perturbation realizations.

If provided, dependencies can be installed with:

```bash
pip install -r requirements.txt
```
