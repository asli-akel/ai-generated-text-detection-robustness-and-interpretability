# AI-Generated Text Detection: Robustness & Interpretability in Social Media (MSc Dissertation)

This repository contains the computational notebooks developed for an MSc dissertation on the robustness and interpretability of multilingual AI-generated text detection in social-media settings.

The work uses the access-restricted **MultiSocial** benchmark and investigates multilingual classification, language- and platform-level robustness, generator generalisation, and SHAP-based interpretability.

## Project at a glance

- **Task:** binary classification of Human-written and AI-generated social-media text.
- **Scale:** 472,097 texts spanning 22 languages, 5 social-media platforms, and 7 AI text generators.
- **Model:** fine-tuned `microsoft/mdeberta-v3-base`.
- **Evaluation:** the unchanged 140,888-sample benchmark test partition, with class-, language-, platform-, and generator-level analysis.
- **Robustness design:** one reference baseline plus seven leave-one-generator-out (LOGO) experiments to measure generalisation to unseen generators.
- **Interpretability:** global, error-conditioned, language-conditioned, and generator-conditioned SHAP analyses.

## Selected results

All figures below are taken from the saved notebook outputs; the restricted test records themselves are not included.

| Experiment | Accuracy | AI-class F1 | Macro F1 | ROC-AUC |
|---|---:|---:|---:|---:|
| Multilingual experiment, with Gemini excluded from model development | 92.71% | 95.72% | 85.54% | 0.9721 |
| LOGO reference baseline, with all generators represented | 94.28% | 96.68% | 88.15% | 0.9782 |

The LOGO experiments reveal that strong aggregate performance does not guarantee uniform robustness to unseen generators. Unseen-generator AI detection ranged from **78.25% to 98.72%**. The largest seen-to-unseen generalisation gaps occurred for **OPT-IML-Max-30B (17.97 percentage points)** and **Aya-101 (17.56 percentage points)**, while held-out v5-Eagle and Vicuna generalised particularly strongly. These differences motivate the accompanying generator-specific error and SHAP analyses.

## What this project demonstrates

- Design and evaluation of an end-to-end multilingual NLP classification pipeline.
- Careful handling of imbalanced benchmark data, predefined splits, subgroup metrics, and false-positive risk.
- Controlled robustness testing against unseen text generators rather than relying only on a random test split.
- Explainability analysis that connects predictive performance with token-level model behaviour.
- Engineering for long-running GPU experiments, including persistent storage, checkpoint resumption, validation checks, and reusable evaluation utilities.
- Responsible management of access-restricted research data and preparation of a privacy-conscious public portfolio.

For a rapid technical review, start with the aggregate results and subgroup evaluation in Notebook 2, then inspect the baseline-versus-LOGO comparison and generator-specific explainability work in Notebook 3.

## Repository contents

The notebooks are intended to be read and executed in this order:

1. [`Notebook1_DataExploration.ipynb`](notebooks/Notebook1_DataExploration.ipynb) — dataset exploration, validation, and preparation.
2. [`Notebook2_Multilingual_Experiments.ipynb`](notebooks/Notebook2_Multilingual_Experiments.ipynb) — multilingual mDeBERTa-v3-base experiments, benchmark evaluation, error analysis, and interpretability analyses.
3. [`Notebook3_LOGO_Experiments.ipynb`](notebooks/Notebook3_LOGO_Experiments.ipynb) — baseline and leave-one-generator-out (LOGO) experiments, generator-generalisation evaluation, and related explainability analyses.

The notebooks were originally run in Google Colab. Their saved aggregate outputs are retained so that the reported results can be inspected without repeating the complete computation. Outputs containing individual restricted-dataset texts were removed from this repository copy.

## Dataset access and restrictions

The dataset is **not included** in this repository.

MultiSocial is distributed through a restricted-access Zenodo record:

- Dataset page: <https://zenodo.org/records/13846152>
- Dataset DOI: <https://doi.org/10.5281/zenodo.13846152>

Access must be requested directly from the dataset maintainers. The Zenodo access conditions state that the dataset is for research use, must not be reshared with people who are not included in the approved request, and must be appropriately cited. Anyone reproducing this work must obtain their own authorisation and comply with the dataset terms.

After authorised download, place the original CSV in the active notebook working directory as:

```text
multisocial_anonymized.csv
```

Notebook 1 creates:

```text
multisocial_processed.csv
```

Notebooks 2 and 3 use that processed file. Both CSV files are excluded by `.gitignore` and must not be committed.

## Computational requirements

The modelling notebooks require a CUDA-capable GPU for practical execution. The original Colab runs used:

- Notebook 2: NVIDIA Tesla T4
- Notebook 3: NVIDIA L4

Notebook 3 is computationally intensive. A complete baseline plus seven LOGO training conditions and the associated explainability analyses may take approximately **30 hours**, depending on hardware, Colab availability, and whether saved checkpoints are available.

The LOGO notebook supports persistent Google Drive storage and checkpoint resumption. Long runs should use persistent storage to avoid losing checkpoints when a Colab runtime disconnects. The repository does not include trained model weights, checkpoints, prediction-level files, or copies of the restricted dataset.

## Environment

These notebooks use Python 3 and the packages listed in `requirements.txt`. In Google Colab, install the dependencies before running the notebooks:

```python
!pip install -r requirements.txt
```

Because the exact historical Colab package snapshot was not embedded in the notebooks, `requirements.txt` documents the required package families rather than claiming an exact environment lock. For strict reproduction, record the resolved package versions and Colab runtime information at execution time.

## Reproducibility notes

- The notebooks preserve the predefined MultiSocial train/test split.
- Random seeds and sampling procedures are defined in the experimental code.
- The model checkpoint is `microsoft/mdeberta-v3-base`.
- Notebook outputs on GitHub are static saved results; GitHub does not execute the notebooks.
- Reproducing the results requires separately authorised dataset access, model downloads, suitable compute, and substantial runtime.
- Local Google Drive paths shown in historical log output identify experiment storage locations only; no Drive content is included.

## Data-safety statement

This portfolio repository contains code and sanitised aggregate outputs only. Individual MultiSocial records, derived record-level files, model checkpoints, credentials, and access tokens are not included. The public repository history begins with this reviewed snapshot and does not contain the earlier working copies of the notebooks.

The dataset remains subject to its original access conditions. Repository access does not grant dataset access, and anyone reproducing the work must request authorisation independently.

## Dataset citation

Macko, D., Kopal, J., Moro, R., and Srba, I. *MultiSocial: Multilingual Benchmark of Machine-Generated Text Detection of Social-Media Texts*. ACL 2025. <https://arxiv.org/abs/2406.12549>

The restricted dataset record should also be cited using DOI `10.5281/zenodo.13846152` in accordance with its access conditions.
