# Publication and data-safety review

This repository was prepared from notebooks that used the restricted MultiSocial dataset.

## Actions applied to the repository copy

- The dataset itself was not copied.
- Common dataset, model, checkpoint, credential, and experiment-output paths are ignored by Git.
- Saved outputs containing individual dataset records were removed from selected cells.
- Aggregate metrics, tables, plots, and training logs were retained where they did not reproduce complete individual records.
- The original source notebooks outside this repository were not modified.

## Review requirements

The initial public history must begin from the sanitised snapshot so earlier working copies are not exposed. All notebook output formats, including HTML and embedded images, should be reviewed again whenever new results are committed. Particular attention is required for local SHAP explanations, error-analysis examples, prediction-level exports, model artefacts, and newly generated output cells.

Public source-code access does not grant access to the restricted dataset. Dataset files and individual records must remain outside the repository, and every researcher must obtain separate authorisation from the dataset maintainers.
