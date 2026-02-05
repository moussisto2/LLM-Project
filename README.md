# Argument Mining with Large Language Models

This repository contains an end-to-end implementation of argument mining using
pretrained language models on two datasets:

- Argument Annotated Essays (AAE v2.0)
- AbstRCT (Biomedical Abstracts)

The project covers data preprocessing, BIO tagging, span reconstruction,
model training, and evaluation using strict and relaxed metrics.

---

## Repository Structure

LLM-Project/
│
├── notebook/
│   └── argument_mining_pipeline.ipynb
│
├── data/
│   └── raw/
│       └── (datasets downloaded automatically by the notebook)
│
├── results/
│   ├── aae_dev_roberta_sanitized.json
│   ├── abstrct_dev_scibert_linearidx.json
│   ├── final_results_summary.json
│   └── experiment_metadata.json
│
├── .gitignore
└── README.md


---

## Notebook

All experiments are implemented in a single notebook:

notebook/argument_mining_pipeline.ipynb

The notebook is structured as follows:

1. Environment setup and reproducibility
2. Dataset acquisition (AAE and AbstRCT)
3. Data preprocessing and BIO alignment
4. Naive sentence-level baselines
5. RoBERTa token classification on AAE
6. SciBERT token classification on AbstRCT
7. Span reconstruction and BIO sanitization
8. Evaluation (strict and relaxed)
9. Packaging of final artifacts
10. Final results summary

---

## Models

The following pretrained models are fine-tuned for token classification:

- AAE: roberta-base
- AbstRCT: allenai/scibert_scivocab_uncased

BIO tagging is used for span labeling. Invalid I- tags are converted to B- tags
when required to ensure valid spans.

---

## Evaluation

Evaluation is performed using the official evaluation script provided with the
course material.

Two metrics are reported:

- Strict evaluation: exact span match
- Relaxed evaluation: partial span overlap (alpha = 0.5)

---

## Final Results

Dataset: AAE
- Naive sentence baseline:  Strict F1 = 0.000, Relaxed F1 = 0.165
- RoBERTa model:            Strict F1 = 0.183, Relaxed F1 = 0.352

Dataset: AbstRCT
- Naive sentence baseline:  Strict F1 = 0.114, Relaxed F1 = 0.226
- SciBERT model:            Strict F1 = 0.048, Relaxed F1 = 0.347

All prediction files and metadata are stored in the results/ directory.

---

## Reproducibility

- Experiments were run on Google Colab with GPU support (Tesla T4).
- Library versions are fixed inside the notebook.
- Running the notebook from start to end reproduces all results.

---

## Notes

The objective of this project is correctness, clarity, and reproducibility
rather than state-of-the-art performance.

The results show that pretrained language models significantly outperform
naive baselines on argument mining tasks across different domains.
